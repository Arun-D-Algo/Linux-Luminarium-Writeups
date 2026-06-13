# Linux Luminarium
# Module 11: Percieving Permissions

## Changing File Ownership
First things first: file ownership. Every file in Linux is owned by a user on the system. Most often, in your day-to-day life, that user is the user you log in as every day.

On a shared system (such as in a computer lab), there might be many people with different user accounts, all with their own files in their own home directories. But even on a non-shared system (such as your personal PC), Linux still has many "service" user accounts for different tasks.

The two most important user accounts are:

Your user account! On pwn.college, this is the hacker user, regardless of what your username is.
root. This is the administrative account and, in most security situations, the ultimate prize. If you take over the root user, you've almost certainly achieved your hacking objective!
So what? Well, it turns out that the way that we prevent you from just doing cat /flag is by having /flag owned by the root user, configure its permissions so that no other user can read it (you will learn how to do that later), and configure the actual challenge to run as the root user (you will learn how to do this later as well). The result is that when you do cat /flag, you get:

```
hacker@dojo:~$ ls -l /flag
-r-------- 1 root root 53 Jul  4 04:47 /flag
hacker@dojo:~$ cat /flag
cat: /flag: Permission denied
hacker@dojo:~$
```
Here, you can see that the flag is owned by the root user (the first root in that line) and the root group (the second root in that line). When we try to read it as the hacker user, we are denied. However, if we were root (a hacker's dream!), we would have no problem reading this file:

```
root@dojo:~# cat /flag
pwn.college{demo_flag}
root@dojo:~#
```
Interestingly, we can change the ownership of files! This is done via the chown (change owner) command:

```
chown [username] [file]
```
Typically, chown can only be invoked by the root user. Let's pretend that we're root again (that never gets old!), and watch a typical use of chown:

```
root@dojo:~# mkdir pwn_directory
root@dojo:~# touch college_file
root@dojo:~# ls -l
total 4
-rw-r--r-- 1 root root    0 May 22 13:42 college_file
drwxr-xr-x 2 root root 4096 May 22 13:42 pwn_directory
root@dojo:~# chown hacker college_file
root@dojo:~# ls -l
total 4
-rw-r--r-- 1 hacker root    0 May 22 13:42 college_file
drwxr-xr-x 2 root   root 4096 May 22 13:42 pwn_directory
root@dojo:~#
```
college_file's owner has been changed to the hacker user, and now hacker can do with it whatever root had been able to do with it! If this was the /flag file, that means that the hacker user would be able to read it!

In this level, we will practice changing the owner of the /flag file to the hacker user, and then read the flag. For this challenge only, I made it so that you can use chown to your heart's content as the hacker user (again, typically, this requires you to be root). Use this power wisely and chown away!

### Solve
**Flag:** `pwn.college{M2jeqe1SuyXosj7rioSNawLYVnq.QXxEjN0wiNyUDN0EzW}`

This challenge introduced file ownership in Linux. The /flag file was owned by the root user, preventing the hacker user from reading it. Unlike a normal Linux system, this challenge allowed the use of chown without root privileges. By changing the owner of /flag from root to hacker, the file became accessible and could then be read with cat to obtain the flag.

```bash
hacker@permissions~changing-file-ownership:~$ ls -l
total 44
-rw-r--r-- 1 hacker hacker   4 Feb 10 12:03 COLLEGE
drwxr-xr-x 1 hacker hacker   0 Nov  6  2025 Desktop
-rw-r--r-- 1 hacker hacker   8 Feb 10 12:49 PWN
lrwxrwxrwx 1 hacker hacker  18 Dec 10  2025 catflag -> /challenge/catflag
-rw-r--r-- 1 root   hacker  60 Dec  9  2025 f
-rw-r--r-- 1 hacker hacker 244 Mar 17 12:35 instructions
drwxr-xr-x 1 hacker hacker  12 Feb 20 10:36 leap
-rw-r--r-- 1 hacker hacker 681 Mar 17 12:35 myflag
lrwxrwxrwx 1 hacker hacker   5 Dec 10  2025 not-the-flag -> /flag
-rw-r--r-- 1 root   hacker  77 Feb 10 13:22 pwn
drwxr-xr-x 1 hacker hacker   4 Jun 11 05:06 script
drwxr-xr-x 1 hacker hacker   6 Jun 11 05:00 scripts
-rw-r--r-- 1 hacker hacker 437 Feb 10 12:13 the-flag
-rw-r--r-- 1 hacker hacker  35 Mar 25 07:44 x
-rwxr-xr-x 1 hacker hacker  46 Jun 11 03:31 x.sh
hacker@permissions~changing-file-ownership:~$ chown hacker /flag
hacker@permissions~changing-file-ownership:~$ cat /flag
pwn.college{M2jeqe1SuyXosj7rioSNawLYVnq.QXxEjN0wiNyUDN0EzW}
```

### New Learnings
Learned that every file in Linux has an associated owner and group that determine who can access or modify it. Reinforced the relationship between file ownership and permissions, showing that access to a file can change simply by transferring ownership. Also gained experience using the chown command to change a file's owner and observed that ownership control is normally a privileged operation reserved for the root user.