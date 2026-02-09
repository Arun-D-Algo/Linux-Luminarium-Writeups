# Linux Luminarium
# Module 2: Pondering Paths

## Position elsewhere
Same thing, but 5 times!

### Solve
**Flag:** `pwn.college{I50Tsgidsq326MQ6UkHUIzYSTag.QX3QTN0wiNyUDN0EzW}`

Changed directories as specified 5 different times, ran /challenge/run in the final directory to get the flag.

```bash
hacker@paths~position-elsewhere:~$ /challenge/run
Starting level 1.
Incorrect...
You are not currently in the /etc/apt/sources.list.d directory.
Please use the `cd` utility to change directory appropriately.
hacker@paths~position-elsewhere:~$ cd /etc/apt/sources.list.d
hacker@paths~position-elsewhere:/etc/apt/sources.list.d$ /challenge/run
Starting level 1.
Correct!!!
/challenge/run is an absolute path, invoked from the right directory!
Moving on to level 2
Please use the `cd` utility to change directory to /proc/335
hacker@paths~position-elsewhere:/etc/apt/sources.list.d$ cd /proc/335
hacker@paths~position-elsewhere:/proc/335$ /challenge/run
Correct!!!
/challenge/run is an absolute path, invoked from the right directory!
Moving on to level 3
Please use the `cd` utility to change directory to /sys/kernel
hacker@paths~position-elsewhere:/proc/335$ cd /sys/kernel
hacker@paths~position-elsewhere:/sys/kernel$ /challenge/run
Correct!!!
/challenge/run is an absolute path, invoked from the right directory!
Moving on to level 4
Please use the `cd` utility to change directory to /usr/share/zoneinfo/posix/Asia
hacker@paths~position-elsewhere:/sys/kernel$ cd /usr/share/zoneinfo/posix/Asia
hacker@paths~position-elsewhere:/usr/share/zoneinfo/posix/Asia$ /challenge/run
Correct!!!
/challenge/run is an absolute path, invoked from the right directory!
Moving on to level 5
Please use the `cd` utility to change directory to /var/log
hacker@paths~position-elsewhere:/usr/share/zoneinfo/posix/Asia$ cd /var/log
hacker@paths~position-elsewhere:/var/log$ /challenge/run
Correct!!!
/challenge/run is an absolute path, invoked from the right directory!
Here is your flag:
pwn.college{I50Tsgidsq326MQ6UkHUIzYSTag.QX3QTN0wiNyUDN0EzW}
```

### New Learnings
Learnt how to change multiple directories.
