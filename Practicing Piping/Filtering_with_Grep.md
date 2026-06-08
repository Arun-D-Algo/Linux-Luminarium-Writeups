# Linux Luminarium
# Module 6: Practicing Piping

## Filtering with grep -v 
The grep command has a very useful option: -v (invert match). While normal grep shows lines that MATCH a pattern, grep -v shows lines that do NOT match a pattern:

hacker@dojo:~$ cat data.txt
hello hackers!
hello world!
hacker@dojo:~$ cat data.txt | grep -v world
hello hackers!
hacker@dojo:~$
Sometimes, the only way to filter to just the data you want is to filter out the data you don't want. In this challenge, /challenge/run will output the flag to stdout, but it will also output over 1000 decoy flags (containing the word DECOY somewhere in the flag) mixed in with the real flag. You'll need to filter out the decoys while keeping the real flag!

Use grep -v to filter out all the lines containing "DECOY" and reveal the real flag!


### Solve
**Flag:** `pwn.college{U9pktG9iRdYw5A-I_9F0684H9Q9.0FOxEzNxwiNyUDN0EzW}`

This challenge was solved by using grep -v to invert the match and filter out unwanted lines. By piping the output of /challenge/run into grep -v DECOY, all decoy flags containing the word DECOY were removed, leaving only the real flag printed to standard output.

```bash
hacker@piping~filtering-with-grep-v:~$ /challenge/run | grep -v DECOY
pwn.college{U9pktG9iRdYw5A-I_9F0684H9Q9.0FOxEzNxwiNyUDN0EzW}
```

### New Learnings
Learned how grep -v inverts pattern matching, allowing lines that do not match a given pattern to be selected. This reinforced how exclusion-based filtering is often necessary when relevant data is surrounded by large amounts of misleading or noisy output.