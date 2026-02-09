# Linux Luminarium
# Module 5: File Globbing

## Multiple Globs
So far, you've specified one glob at a time, but you can do more! Bash supports the expansion of multiple globs in a single word. For example:

hacker@dojo:~$ cat /*fl*
pwn.college{YEAH}
hacker@dojo:~$
What happens above is that the shell looks for all files in / that start with anything (including nothing), then have an f and an l, and end in anything (including ag, which makes flag).

Now you try it. We put a few happy, but diversely-named files in /challenge/files. Go cd there and run /challenge/run, providing a single argument: a short (3 characters or less) globbed word with two * globs in it that covers every word that contains the letter p.

### Solve
**Flag:** `pwn.college{sokr3vWuPh87PlgQRseyj79-rAJ.0lM3kjNxwiNyUDN0EzW}`

This challenge focused on using multiple * globs in a single word. By running the binary with *p*, the shell expanded the argument to include all filenames containing the letter p, satisfying the condition in one short globbed input.

```bash
hacker@globbing~multiple-globs:~$ cd /challenge/files
hacker@globbing~multiple-globs:/challenge/files$ /challenge/run *p*
You got it! Here is your flag!
pwn.college{sokr3vWuPh87PlgQRseyj79-rAJ.0lM3kjNxwiNyUDN0EzW}
```

### New Learnings
Understood that Bash allows multiple glob patterns within the same word, not just one at a time. Also reinforced that * matches any number of characters (including none), making it ideal for broadly capturing filenames based on a shared character.
