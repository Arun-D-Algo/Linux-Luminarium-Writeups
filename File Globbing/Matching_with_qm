# Linux Luminarium
# Module 5: File Globbing

## Matching with ?
Next, let's learn about ?. When it encounters a ? character in any argument, the shell will treat it as a single-character wildcard. This works like *, but only matches one character. For example:

hacker@dojo:~$ touch file_a
hacker@dojo:~$ touch file_b
hacker@dojo:~$ touch file_cc
hacker@dojo:~$ ls
file_a	file_b	file_cc
hacker@dojo:~$ echo Look: file_?
Look: file_a file_b
hacker@dojo:~$ echo Look: file_??
Look: file_cc
Now, practice this yourself! Starting from your home directory, change your directory to /challenge, but use the ? character instead of c and l in the argument to cd! Once you're there, run /challenge/run for the flag!

### Solve
**Flag:** `pwn.college{8Y2JKShFH4GQcYwmjJua9naT5ik.QXyIDO0wiNyUDN0EzW}`

The challenge required navigating to the /challenge directory while replacing specific characters in the path using the ? wildcard. The ? glob was used to substitute exactly one character per position, allowing /challenge to be matched without typing the full directory name. After changing into the directory, the challenge binary was executed to obtain the flag.

```bash
hacker@globbing~matching-with-:~$ cd /?ha??enge
hacker@globbing~matching-with-:/challenge$ /challenge/run
You ran me with the working directory of /challenge! Here is your flag:
pwn.college{8Y2JKShFH4GQcYwmjJua9naT5ik.QXyIDO0wiNyUDN0EzW}
```

### New Learnings
Learned how the ? glob matches exactly one character during shell expansion, enabling precise control over which parts of a filename or path are substituted. This reinforced the difference between ? and * when performing glob-based path matching.
