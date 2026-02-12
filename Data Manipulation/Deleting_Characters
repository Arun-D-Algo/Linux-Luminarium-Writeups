# Linux Luminarium
# Module 8: Data Manipulation

## Deleting Characters
tr can also translate characters to nothing (i.e., delete them). This is done via a -d flag and an argument of what characters to delete:

hacker@dojo:~$ echo PAWN | tr -d A
PWN
hacker@dojo:~$
Pretty simple! Now you give it a try. In the output of /challenge/run, I'll intersperse some decoy characters (specifically: ^ and %) among the flag characters. Use tr -d to remove them!


### Solve
**Flag:** `pwn.college{cdWleMoln5gQsZSMTjiNdldYpdd.0FNxEzNxwiNyUDN0EzW}`

This challenge built on the previous use of tr, but instead of translating characters, it focused on deleting unwanted ones. The /challenge/run program printed the flag with extra decoy characters (^ and %) scattered throughout it. By piping the output into tr -d ^%, those specific characters were removed from the stream entirely. Since tr -d deletes every occurrence of the listed characters, the noisy output was cleaned in real time, leaving behind the properly formatted flag.

```bash
hacker@data~deleting-characters:~$ /challenge/run | tr -d ^%
Your character-stuffed flag:
pwn.college{cdWleMoln5gQsZSMTjiNdldYpdd.0FNxEzNxwiNyUDN0EzW}
```

### New Learnings
Learned that tr is not limited to translating characters — it can also delete specific characters using the -d option. Reinforced how stream editing works directly on standard input without modifying files. Also strengthened understanding of how small Unix tools can be combined in pipelines to progressively clean, transform, and refine data efficiently.