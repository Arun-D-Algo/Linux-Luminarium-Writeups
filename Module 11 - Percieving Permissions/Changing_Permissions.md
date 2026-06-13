# Linux Luminarium
# Module 11: Percieving Permissions

## Changing Permissions
So now we're well-versed in ownership. Let's talk about the other side of the coin: file permissions. Recall our example:

hacker@dojo:~$ mkdir pwn_directory
hacker@dojo:~$ touch college_file
hacker@dojo:~$ ls -l
total 4
-rw-r--r-- 1 hacker hacker    0 May 22 13:42 college_file
drwxr-xr-x 2 hacker hacker 4096 May 22 13:42 pwn_directory
hacker@dojo:~$
As a reminder, the first character is the file type. The next nine characters are the actual access permissions of the file or directory, split into 3 characters denoting permissions for the owning user (now you understand this!), 3 characters denoting the permissions for the owning group (now you understand this as well!), and 3 characters denoting the permissions that all other access (e.g., by other users and other groups) has to the file.

Each character of the three represent permission for a different type:

r - user/group/other can read the file (or list the directory)
w - user/group/other can modify the files (or create/delete files in the directory)
x - user/group/other can execute the file as a program (or can enter the directory, e.g., using `cd`)
- - nothing 
For college_file above, the rw-r--r-- permissions entry decodes to:

r: the user that owns the file (user hacker) can read it
w: the user that owns the file (user hacker) can write to it
-: the user that owns the file (user hacker) cannot execute it
r: users in the group that owns the file (group hacker) can read it
-: users in the group that owns the file (group hacker) cannot write to it
-: users in the group that owns the file (group hacker) cannot execute it
r: all other users can read it
-: all other users cannot write to it
-: all other users cannot execute it
Now, let's look at the default permissions of /flag:

hacker@dojo:~$ ls -l /flag
-r-------- 1 root root 53 Jul  4 04:47 /flag
hacker@dojo:~$
Here, there is only one bit set: the read permission for the owning user (in this case, root). Members of the owning group (the root group) and all other users have no access to the file.

You might be wondering how the chgrp levels worked, if there is no group access to the file. Well, for those levels, I set the permissions differently:

hacker@dojo:~$ ls -l /flag
-r--r----- 1 root root 53 Jul  4 04:47 /flag
hacker@dojo:~$
The group had access! That is why chgrping the file enabled you to read the file.

Anyways! Like ownership, file permissions can also be changed. This is done with the chmod (change mode) command. The basic usage for chmod is:

chmod [OPTIONS] MODE FILE
You can specify the MODE in two ways: as a modification of the existing permissions mode, or as a completely new mode to overwrite the old one.

In this level, we will cover the former: modifying an existing mode. chmod allows you to tweak permissions with the mode format of WHO+/-WHAT, where WHO is user/group/other and WHAT is read/write/execute. For example, to add read access for the owning user, you would specify a mode of u+r. write and execute access for the group and the other (or all the modes) are specified the same way. More examples:

u+r, as above, adds read access to the user's permissions
g+wx adds write and execute access to the group's permissions
o-w removes write access for other users
a-rwx removes all permissions for the user, group, and world
So:

root@dojo:~# mkdir pwn_directory
root@dojo:~# touch college_file
root@dojo:~# ls -l
total 4
-rw-r--r-- 1 root root    0 May 22 13:42 college_file
drwxr-xr-x 2 root root 4096 May 22 13:42 pwn_directory
root@dojo:~# chmod go-rwx *
root@dojo:~# ls -l
total 4
-rw------- 1 hacker root    0 May 22 13:42 college_file
drwx------ 2 root   root 4096 May 22 13:42 pwn_directory
root@dojo:~#
In this challenge, you must change the permissions of the /flag file to read it! Typically, you need to be the owner of the file in order to change its permissions, but I have made the chmod command all-powerful for this level, and you can chmod anything you want even though you are the hacker user. This is an ultimate power. The /flag file is owned by root, and you can't change that, but you can make it readable. Go and solve this!

### Solve
**Flag:** `pwn.college{k4ccYofHtStRKthmVAkOmzzm9_X.QXzcjM1wiNyUDN0EzW}`

This challenge shifted focus from ownership and groups to file permissions. The /flag file remained owned by root, but the challenge granted permission to use chmod on any file. Instead of changing who owned the file or which group it belonged to, the solution was to modify the file's permissions directly. By adding read permission for all users with chmod a+r /flag, the file became readable by the hacker user and the flag could then be retrieved with cat.

```bash
hacker@permissions~changing-permissions:~$ ls -l
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
hacker@permissions~changing-permissions:~$ chmod a+r /flag
hacker@permissions~changing-permissions:~$ cat /flag
pwn.college{k4ccYofHtStRKthmVAkOmzzm9_X.QXzcjM1wiNyUDN0EzW}
```

### New Learnings
Learned that Linux access control is determined by both ownership and permissions, and that permissions can be modified independently of ownership. Unlike the previous challenges, where access was gained by changing the owner (chown) or group (chgrp) of a file, this challenge demonstrated that simply granting the appropriate permission bits can be enough to access a protected file. Also gained experience using chmod with symbolic modes such as a+r, and developed a deeper understanding of the user, group, and other permission model represented by the r, w, and x bits.