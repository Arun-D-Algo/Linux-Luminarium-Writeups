# Linux Luminarium
# Module 5: File Globbing

## Exclusionary Globbing
Sometimes, you want to filter out files in a glob! Luckily, [] helps you do just this. If the first character in the brackets is a ! or (in newer versions of bash) a ^, the glob inverts, and that bracket instance matches characters that aren't listed. For example:

hacker@dojo:~$ touch file_a
hacker@dojo:~$ touch file_b
hacker@dojo:~$ touch file_c
hacker@dojo:~$ ls
file_a	file_b	file_c
hacker@dojo:~$ echo Look: file_[!ab]
Look: file_c
hacker@dojo:~$ echo Look: file_[^ab]
Look: file_c
hacker@dojo:~$ echo Look: file_[ab]
Look: file_a file_b
Armed with this knowledge, go forth to /challenge/files and run /challenge/run with all files that don't start with p, w, or n!

NOTE: The ! character has a different special meaning in bash when it's not the first character of a [] glob, so keep that in mind if things stop making sense! ^ does not have this problem, but is also not compatible with older shells.

### Solve
**Flag:** `pwn.college{wIhDWi6WVqmOvCwKZU72pJtsGGm.QX2IDO0wiNyUDN0EzW}`

The challenge was solved by using exclusionary bracket globbing to filter filenames at expansion time. The pattern [^pwn]* matched all files whose first character was not p, w, or n, and passing this expanded list to /challenge/run returned the flag.

```bash
hacker@globbing~exclusionary-globbing:~$ cd /challenge/files
hacker@globbing~exclusionary-globbing:/challenge/files$ /challenge/run [^pwn]*
You got it! Here is your flag!
pwn.college{wIhDWi6WVqmOvCwKZU72pJtsGGm.QX2IDO0wiNyUDN0EzW}
```

### New Learnings
Learned that placing ^ (or !) as the first character inside [] inverts the match, allowing unwanted filenames to be excluded. This reinforced how bracket globbing matches exactly one character, and how combining it with * enables precise yet flexible filename selection during shell expansion.