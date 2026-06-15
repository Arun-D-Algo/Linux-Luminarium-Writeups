# Linux Luminarium
# Module 15: Daring Destruction

## Life After rm -rf/
Let's dig into the effects of blowing away your whole filesystem. You're now an experienced rmer, but previously, /challenge/check printed the flag out for you when you cleared away the clutter of the filesystem. What if it hadn't? Without cat, how would you read that /flag?

Recall, from the Digesting Documentation module, that some shell commands are builtins. While ls, cat, and such aren't, read (which, if you recall from the Shell Variables module, can read files!) is. That means that, even if you blow away your whole filesystem, as long as you have an already-running instance of bash, you can read files!

This challenge will force you to try it. It's almost the same as the previous one, but you must read the flag yourself after you destroy the system. After you rm everything, your previously-launched /challenge/check will restore the /flag file and make it readable. Then you can read it!

### Solve
**Flag:** `pwn.college{wWAsuonti8Ygtzxsljb5yPIDhk3.01MzEzNxwiNyUDN0EzW}`

This challenge built directly on the previous rm -rf / level, but with one important difference: after destroying the filesystem, the flag had to be read manually. Since commands like cat are external programs and may be deleted during the wipe, the solution relied on Bash's built-in read command, which continues to work as long as the shell itself is still running. After /challenge/check restored a readable /flag, the flag was loaded into a shell variable using input redirection and then displayed with echo.

```bash
hacker@destruction~life-after-rm-rf-:~$ rm -rf --no-preserve-root /
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
hacker@destruction~life-after-rm-rf-:~$ /challenge/check
Looks like you haven't wiped the system! We'll check again in 5 seconds...
Looks like you haven't wiped the system! We'll check again in 5 seconds...
Looks like you haven't wiped the system! We'll check again in 5 seconds...
Looks like you haven't wiped the system! We'll check again in 5 seconds...
Looks like you haven't wiped the system! We'll check again in 5 seconds...
Looks like you haven't wiped the system! We'll check again in 5 seconds...
YES! You did it again! Go read the flag!
hacker@destruction~life-after-rm-rf-:~$ read flag < /flag 
hacker@destruction~life-after-rm-rf-:~$ echo $flag
pwn.college{wWAsuonti8Ygtzxsljb5yPIDhk3.01MzEzNxwiNyUDN0EzW}
```

### New Learnings
Learned the distinction between external programs and Bash built-in commands. Reinforced that commands such as cat, ls, and rm depend on executable files existing on the filesystem, while built-ins like read are part of the running shell itself and continue to function even after those files are deleted. Also gained experience using input redirection (<) with read to load file contents into a shell variable, demonstrating how a running shell can remain useful even after most of the underlying filesystem has been destroyed.