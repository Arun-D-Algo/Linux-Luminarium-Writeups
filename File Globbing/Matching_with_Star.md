# Linux Luminarium
# Module 5: File Globbing

## Matching with *
The first glob we'll learn is *. When it encounters a * character in any argument, the shell will treat it as a "wildcard" and try to replace that argument with any files that match the pattern. It's easier to show you than explain:

hacker@dojo:~$ touch file_a
hacker@dojo:~$ touch file_b
hacker@dojo:~$ touch file_c
hacker@dojo:~$ ls
file_a	file_b	file_c
hacker@dojo:~$ echo Look: file_*
Look: file_a file_b file_c
Of course, though in this case, the glob resulted in multiple arguments, it can just as simply match only one. For example:

hacker@dojo:~$ touch file_a
hacker@dojo:~$ ls
file_a
hacker@dojo:~$ echo Look: file_*
Look: file_a
When zero files are matched, by default, the shell leaves the glob unchanged:

hacker@dojo:~$ touch file_a
hacker@dojo:~$ ls
file_a
hacker@dojo:~$ echo Look: nope_*
Look: nope_*
The * matches any part of the filename except for / or a leading . character. For example:

hacker@dojo:~$ echo ONE: /ho*/*ck*
ONE: /home/hacker
hacker@dojo:~$ echo TWO: /*/hacker
TWO: /home/hacker
hacker@dojo:~$ echo THREE: ../*
THREE: ../hacker
Now, practice this yourself! Starting from your home directory, change your directory to /challenge, but use globbing to keep the argument you pass to cd to at most four characters! Once you're there, run /challenge/run for the flag!

### Solve
**Flag:** `pwn.college{ciFdmpHPOwKQ3K4339cHmS7FrkQ.QXxIDO0wiNyUDN0EzW}`

The challenge required changing into the /challenge directory while limiting the argument length passed to cd. This was achieved using globbing with star, allowing the shell to expand /ch* into /challenge. Once inside the directory, the challenge binary was executed to retrieve the flag.

```bash
hacker@globbing~matching-with-:~$ cd /ch*
hacker@globbing~matching-with-:/challenge$ /challenge/run
You ran me with the working directory of /challenge! Here is your flag:
pwn.college{ciFdmpHPOwKQ3K4339cHmS7FrkQ.QXxIDO0wiNyUDN0EzW}
```

### New Learnings
Learned how the * glob acts as a wildcard during shell expansion, allowing abbreviated path patterns to match full directory names. Also reinforced how globbing is processed by the shell before the command is executed.
