# Linux Luminarium
# Module 5: File Globbing

## Matching with []
Next, we will cover []. The square brackets are, essentially, a limited form of ?, in that instead of matching any character, [] is a wildcard for some subset of potential characters, specified within the brackets. For example, [pwn] will match the character p, w, or n. For example:

hacker@dojo:~$ touch file_a
hacker@dojo:~$ touch file_b
hacker@dojo:~$ touch file_c
hacker@dojo:~$ ls
file_a	file_b	file_c
hacker@dojo:~$ echo Look: file_[ab]
Look: file_a file_b
Try it here! We've placed a bunch of files in /challenge/files. Change your working directory to /challenge/files and run /challenge/run with a single argument that bracket-globs into file_b, file_a, file_s, and file_h!

### Solve
**Flag:** `pwn.college{0op9QTpqpyF-VdbOO4mmZkuUhhe.QXzIDO0wiNyUDN0EzW}`

The challenge required running the challenge binary with a single argument that expands to multiple specific filenames. This was achieved using bracket globbing ([]), which allows matching one character from a defined set. The pattern file_[bash] expanded to the required files, and passing it to /challenge/run successfully retrieved the flag.

```bash
hacker@globbing~matching-with-:~$ cd /challenge/files
hacker@globbing~matching-with-:/challenge/files$ /challenge/run file_[bash]
You got it! Here is your flag!
pwn.college{0op9QTpqpyF-VdbOO4mmZkuUhhe.QXzIDO0wiNyUDN0EzW}
```

### New Learnings
Learned how bracket globbing ([]) matches exactly one character from a specified set, allowing fine-grained control over which filenames are expanded. This demonstrated how [] provides more precise matching than * or ? during shell expansion.