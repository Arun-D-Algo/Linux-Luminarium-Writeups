# Linux Luminarium
# Module 15: Daring Destruction

## rm -rf/
Want to wipe the slate clean and start over? You can!

```
hacker@dojo:~$ ls /
bin etc blah blah blah
hacker@dojo:~$ rm -rf /
hacker@dojo:~$ ls /
bash: ls: command not found
hacker@dojo:~$
```
What happened here? As you recall, rm removes files. The -r (recursive) flag removes directories and all files containing them. The -f (force) flag ignores any errors the rm command runs into or compulsions that it may have. Combined and aimed at /, the results are catastrophic: a full wipe of your system. On a modern system, things aren't that simple, but you'll figure that out when you see it.

In this challenge, you will do something that you might never do again: wipe the whole system. We've actually modified things a bit to keep your home directory safe (normally, it would get wiped as well!), but otherwise, all that stands before you and the flag is your willingness to wipe the drive. But before you wipe it all, make sure to start /challenge/check so that it can watch the fireworks (and give you the flag)!

NOTE: The rm will take a while to run. There's a lot to delete!

NOTE: There are various technical reasons why you're unlikely to be able to delete everything, including the technique we use to protect your home directory in this level. Don't worry, you'll be doing enough damage!

### Solve
**Flag:** `pwn.college{MsA7e9jvq26m3TA17CMYgXZgUhU.0lMzEzNxwiNyUDN0EzW}`

This challenge demonstrated the destructive power of rm -rf. By running rm -rf --no-preserve-root /, the system attempted to recursively delete nearly everything from the root filesystem. Although some directories and files were protected or busy, enough of the system was removed for /challenge/check to detect the damage. Once the checker confirmed that the system had been sufficiently wiped, it revealed the flag.

```bash
hacker@destruction~rm-rf-:~$ rm -rf --no-preserve-root /
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
hacker@destruction~rm-rf-:~$ 
hacker@destruction~rm-rf-:~$ /challenge/check
Looks like you haven't wiped the system! We'll check again in 5 seconds...
Looks like you haven't wiped the system! We'll check again in 5 seconds...
Looks like you haven't wiped the system! We'll check again in 5 seconds...
Looks like you haven't wiped the system! We'll check again in 5 seconds...
YES! You wiped it, you wild hacker! The flag is yours:
pwn.college{MsA7e9jvq26m3TA17CMYgXZgUhU.0lMzEzNxwiNyUDN0EzW}
```

### New Learnings
Learned how rm -rf combines recursive deletion (-r) with force mode (-f) to remove entire directory trees without confirmation. Reinforced that targeting / attempts to delete the whole filesystem and can render a system unusable. Also gained experience with Linux safety mechanisms such as --no-preserve-root, mounted filesystems, and busy resources, which prevent certain critical parts of the system from being removed even during a destructive operation.