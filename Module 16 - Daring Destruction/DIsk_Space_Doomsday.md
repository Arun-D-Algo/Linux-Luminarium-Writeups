# Linux Luminarium
# Module 15: Daring Destruction

## Disk Space Doomsday
The available space in /home/hacker in this container is a measly 1 gigabyte. In this level you will clog up /home/hacker with so much junk that even a tiny 1 megabyte file can't be created. When this happens, your workspace becomes unusable. We'll practice inducing this in this challenge, and then expand on it a bit later.

How to fill the disk? There are so many ways. Here, we'll teach you the yes command!

```
hacker@dojo:~$ yes | head
y
y
y
y
y
y
y
y
y
y
hacker@dojo:~$
```
The yes outputs y over and over forever. The typical usage is to automate confirmation prompts ("Are you sure you want to delete this file?") using piping, but we'll use it here to make a massive file full of "y" lines. Just redirect yes to a file in your home directory, and you'll fill your disk in a minute or two!

This challenge forces you to fill the disk and then clean up. The process:

Fill your disk.
Run /challenge/check. It will attempt to create a 1 megabyte temporary file. If that fails, you pass the first stage and the checker will ask you to free the space.
Delete the file you made (with rm) to clear up the space.
Run /challenge/check a second time. If it can now create the temporary file (i.e., you successfully cleaned up your home directory), you’ll receive the flag.
Why two stages? Your home directory persists across challenge instances. If we let you keep it full, your pwn.college will stop working. This is by far the most common cause of weird issues on pwn.college!

HELP IT BROKE! If you fill the disk and don't clean it up afterwards, you'll need to ssh in to fix things (by removing that file). This is a bit tricky, but we describe how to do it under "Connecting over SSH" in the Getting Started module.

### Solve
**Flag:** `pwn.college{EUFHE4sO48sYof-UAXeItAr4oCn.0lMyEzNxwiNyUDN0EzW}`

This challenge focused on resource exhaustion by intentionally filling the limited storage space available in the home directory. The yes command was redirected into a file, causing it to continuously write data until the disk quota was exceeded. Once the home directory was full, /challenge/check confirmed that it could no longer create a temporary file. The large file was then deleted to free the disk space, and running the checker a second time verified that the cleanup was successful, revealing the flag.

```bash
hacker@destruction~disk-space-doomsday:~$ ls
COLLEGE  bomb.sh  f             myflag        script    x
Desktop  catflag  instructions  not-the-flag  scripts   x.sh
PWN      evil     leap          pwn           the-flag
hacker@destruction~disk-space-doomsday:~$ yes > x.sh
yes: standard output: Disk quota exceeded
hacker@destruction~disk-space-doomsday:~$ /challenge/check
Well done, you clogged the disk. Now free that space (remove the file you created) and run /challenge/check again to prove you cleaned up!
hacker@destruction~disk-space-doomsday:~$ rm x.sh
hacker@destruction~disk-space-doomsday:~$ /challenge/check
Disk space restored. Here is your flag:
pwn.college{EUFHE4sO48sYof-UAXeItAr4oCn.0lMyEzNxwiNyUDN0EzW}
```

### New Learnings
Learned how the yes command can generate an unlimited stream of output and how output redirection can rapidly consume disk space. Reinforced the concept that storage is a finite system resource and that exhausting it can prevent programs from creating new files. Also gained experience intentionally triggering a disk-full condition, verifying its effects with a challenge program, and restoring system functionality by removing the oversized file.