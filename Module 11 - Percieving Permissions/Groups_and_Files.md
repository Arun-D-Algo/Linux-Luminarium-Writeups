# Linux Luminarium
# Module 11: Percieving Permissions

## Groups and Files
Sharing is caring, and sharing is built into Linux's design. Files have both an owning user and group. A group can have multiple users in it, and a user can be a member of multiple groups.

You can check what groups you are part of with the id command:

hacker@dojo:~$ id
uid=1000(hacker) gid=1000(hacker) groups=1000(hacker)
hacker@dojo:~$
Here, the hacker user is only in the hacker group. The most common use-case for groups is to control access to different system resources. For example, "Privileged Mode" in pwn.college grants you root access to allow better debugging and so on. This is handled by giving you an extra group when you launch in Privileged Mode:

hacker@dojo:~$ id
uid=1000(hacker) gid=1000(hacker) groups=1000(hacker),27(sudo)
hacker@dojo:~$
A typical main user of a typical Linux desktop has a lot of groups. For example, this is Zardus' desktop:

zardus@yourcomputer:~$ id
uid=1000(zardus) gid=1000(zardus) groups=1000(zardus),24(cdrom),25(floppy),27(sudo),29(audio),30(dip),44(video),46(plugdev),100(users),106(netdev),114(bluetooth),117(lpadmin),120(scanner),995(docker)
zardus@yourcomputer:~$
All these groups give Zardus the ability to read CDs and floppy disks (who does that anymore?), administer the system, play music, draw to the video monitor, use bluetooth, and so on. Often, this access control happens via group ownership on the filesystem! For example, graphical output can be done via the special /dev/fb0 file:

zardus@yourcomputer:~$ ls -l /dev/fb0
crw-rw---- 1 root video 29, 0 Jun 30 23:42 /dev/fb0
zardus@yourcomputer:~$
This file is a special device file (type c means it is a "character device"), and interacting with it results in changes to the display output (rather than changes to disk storage, as for a normal file!). Zardus' user account on his machine can interact with it because the file has a group ownership of video, and Zardus is a member of the video group.

No such luck for the /flag file in the dojo, though! Consider the following:

hacker@dojo:~$ id
uid=1000(hacker) gid=1000(hacker) groups=1000(hacker)
hacker@dojo:~$ ls -l /flag
-r--r----- 1 root root 53 Jul  4 04:47 /flag
hacker@dojo:~$ cat /flag
cat: /flag: Permission denied
hacker@dojo:~$
Here, the flag file is owned by the root user and the root group, and the hacker user is neither the root user nor a member of the root group, so the file cannot be accessed. Luckily, group ownership can be changed with the chgrp (change group) command! Unless you are the owner of the file and a member in the new group, this typically requires root access, so let's check it out as root:

root@dojo:~# mkdir pwn_directory
root@dojo:~# touch college_file
root@dojo:~# ls -l
total 4
-rw-r--r-- 1 root root    0 May 22 13:42 college_file
drwxr-xr-x 2 root root 4096 May 22 13:42 pwn_directory
root@dojo:~# chgrp hacker college_file
root@dojo:~# ls -l
total 4
-rw-r--r-- 1 root hacker    0 May 22 13:42 college_file
drwxr-xr-x 2 root root   4096 May 22 13:42 pwn_directory
root@dojo:~#
In this level, I have made the flag readable by whatever group owns it, but this group is currently root. Luckily, I have also made it possible for you to invoke chgrp as the hacker user! Change the group ownership of the flag file, and read the flag!

### Solve
**Flag:** `pwn.college{YVxURSlLV11DQe_aAmCfaEtUG6B.QXxcjM1wiNyUDN0EzW}`

This challenge built directly on the previous one. Instead of changing the owner of /flag, the goal was to change its group ownership. The flag was configured so that members of its owning group could read it, but the group was initially root, which the hacker user did not belong to. Since the challenge allowed the use of chgrp, the group ownership of /flag was changed from root to hacker. Because the current user was a member of the hacker group, the file became readable and the flag could then be retrieved with cat.

```bash
hacker@permissions~groups-and-files:~$ ls -l
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
hacker@permissions~groups-and-files:~$ chgrp hacker /flag
hacker@permissions~groups-and-files:~$ cat /flag
pwn.college{YVxURSlLV11DQe_aAmCfaEtUG6B.QXxcjM1wiNyUDN0EzW}
```

### New Learnings
Learned that Linux access control depends not only on file ownership but also on group ownership. Reinforced that every file has both an owner and an associated group, and permissions can be granted to either. Unlike the previous challenge, where access was obtained by changing the file's owner with chown, this challenge demonstrated that changing the file's group with chgrp can also grant access when group-read permissions are enabled. Also gained experience viewing user group memberships with id and understanding how groups are commonly used to share access to files and system resources among multiple users.