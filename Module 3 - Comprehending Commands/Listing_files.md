# Linux Luminarium
# Module 3: Comprehending Commands

## Listing files
So far, we've told you which files to interact with. But directories can have lots of files (and other directories) inside them, and we won't always be here to tell you their names. You'll need to learn to list their contents using the ls command!

ls will list files in all the directories provided to it as arguments, and in the current directory if no arguments are provided. Observe:

hacker@dojo:~$ ls /challenge
run
hacker@dojo:~$ ls
Desktop    Downloads  Pictures  Templates
Documents  Music      Public    Videos
hacker@dojo:~$ ls /home/hacker
Desktop    Downloads  Pictures  Templates
Documents  Music      Public    Videos
hacker@dojo:~$
In this challenge, we've named /challenge/run with some random name! List the files in /challenge to find it.

### Solve
**Flag:** `pwn.college{A-Pgtp4BtR6iou8DHnCeqZq6RTI.QX4IDO0wiNyUDN0EzW}`

Listed the files in '/challenge' directory, then used the absolute path with the modified run file to get the flag.

```bash
hacker@commands~listing-files:~$ 
hacker@commands~listing-files:~$ ls /challenge
23804-renamed-run-20467  DESCRIPTION.md
hacker@commands~listing-files:~$ /challenge/23804-renamed-run-20467
Yahaha, you found me! Here is your flag:
pwn.college{A-Pgtp4BtR6iou8DHnCeqZq6RTI.QX4IDO0wiNyUDN0EzW}
```

### New Learnings
Learnt how to list directories.