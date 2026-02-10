# Linux Luminarium
# Module 6: Practicing Piping

## Filtering with sed
grep is not the only way to match patterns. Sometimes the real data and the garbage data are mixed in the same line, and we want to filter out the garbage. For that, we have sed. sed provides an easy way to substitute patterns in text with a different word. The syntax for matching and replacing is simple:

sed "s/oldword/newword/g"
s/ - substitute
oldword - the word to replace
newword - the replacement for oldword
/g - global (search for all occurrences of the pattern)

In this challenge, /challenge/run will print out the flag, but between each character there will be the string "FAKEFLAG". Your job is to filter out the garbage data from the flag. Good luck!


### Solve
**Flag:** `pwn.college{4BsjpQZOmN8DMbrnDV6WsdMQCQw.01NxQTMywiNyUDN0EzW}`

This challenge was solved by piping the output of /challenge/run into sed and using substitution to remove unwanted text within a line. The command sed "s/FAKEFLAG//g" replaced every occurrence of the string FAKEFLAG with an empty string, effectively stripping the garbage data and revealing the original flag.

```bash
hacker@piping~filtering-with-sed:~$ /challenge/run | sed "s/FAKEFLAG//g"
pwn.college{4BsjpQZOmN8DMbrnDV6WsdMQCQw.01NxQTMywiNyUDN0EzW}
```

### New Learnings
Learned how sed performs in-place pattern substitution on streamed text, making it ideal for cleaning or transforming data when useful and unwanted content are mixed within the same line. This reinforced the power of combining pipes with stream editors to modify output in real time without creating intermediate files.