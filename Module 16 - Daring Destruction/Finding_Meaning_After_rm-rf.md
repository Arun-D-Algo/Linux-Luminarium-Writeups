# Linux Luminarium
# Module 15: Daring Destruction

## Finding Meaning After rm -rf/
So you can live without cat! How about without ls? This time, /challenge/check will restore the flag to a randomly-named file. You'll need to find it without reaching for your ls command.

There are a lot of ways to solve this challenge. echo is a builtin, and you can File Glob an argument to it to expand to all files! For example, echo * will print out the names of all of the files in the current directory. Similarly, you can use tab-completion (hit tab a few times) of an argument to have the shell list possible files for you.

Whatever route you use, find the randomly-named file that /challenge/check makes in / after you rm, read it, and get the flag!

### Solve
**Flag:** `pwn.college{E5yIJiRBXAQZhGVB5IcCODvGFSH.0FNzEzNxwiNyUDN0EzW}`

This challenge extended the previous level by removing another commonly used tool: ls. After wiping the filesystem, /challenge/check restored the flag inside a randomly named file rather than /flag. Since ls was no longer available, Bash's built-in globbing and echo command were used to list the contents of directories. By printing the contents of /, the newly created random file was identified. The file's contents were then loaded into a variable using the built-in read command and displayed with echo, revealing the flag.

```bash
hacker@destruction~finding-meaning-after-rm-rf-:~$ rm -rf --no-preserve-root /
/bin/rm: skipping '/home/hacker', since it's on a different device
/bin/rm: cannot remove '/etc/resolv.conf': Device or resource busy
/bin/rm: cannot remove '/etc/hostname': Device or resource busy
/bin/rm: cannot remove '/etc/hosts': Device or resource busy
/bin/rm: skipping '/dev', since it's on a different device
/bin/rm: cannot remove '/usr/sbin/docker-init': Device or resource busy
/bin/rm: skipping '/run/dojo/sys', since it's on a different device
/bin/rm: skipping '/sys', since it's on a different device
/bin/rm: skipping '/proc', since it's on a different device
/bin/rm: skipping '/nix', since it's on a different device
hacker@destruction~finding-meaning-after-rm-rf-:~$ /challenge/check
Looks like you haven't wiped the system! We'll check again in 5 seconds...
Looks like you haven't wiped the system! We'll check again in 5 seconds...
Looks like you haven't wiped the system! We'll check again in 5 seconds...
Looks like you haven't wiped the system! We'll check again in 5 seconds...
YES! You did it again! Go read the flag!
hacker@destruction~finding-meaning-after-rm-rf-:~$ echo *
COLLEGE Desktop PWN bomb.sh catflag evil f instructions leap myflag not-the-flag pwn script scripts the-flag x
hacker@destruction~finding-meaning-after-rm-rf-:~$ echo /*
/633bb3d7 /dev /etc /home /nix /proc /run /sys /usr
hacker@destruction~finding-meaning-after-rm-rf-:~$ read flag < /633bb3d7
hacker@destruction~finding-meaning-after-rm-rf-:~$ echo $flag
pwn.college{E5yIJiRBXAQZhGVB5IcCODvGFSH.0FNzEzNxwiNyUDN0EzW}
```

### New Learnings
Learned that shell globbing (*) is performed by Bash itself and does not depend on external programs such as ls. Reinforced that built-in commands like echo and read continue working even after most of the filesystem has been deleted, as long as the shell remains running. Also gained experience using glob expansion to discover files when directory listing tools are unavailable, demonstrating how Bash's built-in features can replace common utilities in extreme situations.