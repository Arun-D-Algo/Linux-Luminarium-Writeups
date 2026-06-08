# Linux Luminarium
# Module 2: Pondering Paths

## The root
Alright, so the filesystem starts at /. Under that, there are a whole mess of other directories, configuration files, programs, and, most importantly, flags. In this level, we've added a program right in /, called pwn, that will give you the flag. All you need to do for this level is to invoke this program!

You can invoke a program by providing its path on the command line. In this case, you'll be giving the exact path, starting from /, so the path would be /pwn. This style of path, one that starts with the root directory, is referred to as an "absolute path".

Start the challenge, launch a terminal, invoke the pwn program using its absolute path, and Capture that Flag! Good luck!

### Solve
**Flag:** `pwn.college{Ee_7rhAJzU4Yxv0gI1ZkoqgRy3O.QX4cTO0wiNyUDN0EzW}`

Just did what the question asked, typed in /pwn absolute path, to get the flag.

```bash
hacker@paths~the-root:~$ /pwn
BOOM!!!
Here is your flag:
pwn.college{Ee_7rhAJzU4Yxv0gI1ZkoqgRy3O.QX4cTO0wiNyUDN0EzW}
```

### New Learnings
Learnt about absolute paths.
