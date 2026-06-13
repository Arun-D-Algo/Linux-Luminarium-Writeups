# Linux Luminarium
# Module 12: Chaining Commands

## Reading Shell Scripts
You're not the only one who writes shell scripts! They are very handy for doing simple "system-level" tasks, and are a common tool that developers and sysadmins reach for. In fact, a surprising fraction of the programs on a typical Linux machine are shell scripts.

In this level, we will learn to read shell scripts. /challenge/run is a shell script that requires you to put in a secret password, but that password is hardcoded into the script itself! Read the script (using, say, cat), figure out the password, and get the flag!

NOTE: Feel free to try to read the code of other challenges as well! Reading code is a critical strategy in learning new skills, because you can see how certain functionality was implemented and reuse those strategies in your own scripts. But watch out: some program files are machine code, and will not be readable to humans. You can use the file command to differentiate, but almost all the challenges in the Linux Luminarium are implemented as shell scripts and are safe to cat out.

### Solve
**Flag:** `pwn.college{EsSAYDFb13-Y5RzrSAZg2R2yceG.0lMwgDOxwiNyUDN0EzW}`

This challenge required discovering a hidden password embedded directly inside the /challenge/run shell script. Instead of guessing inputs, the script was opened and inspected using cat /challenge/run. Reading the source code revealed that the program used read GUESS to accept input from standard input and then compared the value against the hardcoded string hack the PLANET. If the input matched exactly, the script displayed the flag. After identifying the correct password from the code, /challenge/run was executed and the string hack the PLANET was entered when prompted. The condition evaluated to true, causing the script to print the flag and complete the challenge.

```bash
hacker@chaining~reading-shell-scripts:~$ cat /challenge/run
#!/usr/bin/exec-suid -- /bin/bash -p

read GUESS
if [ "$GUESS" == "hack the PLANET" ]
then
	echo "CORRECT! Your flag:"
	cat /flag
else
	echo "Read the /challenge/run file to figure out the correct password!"
fi
hacker@chaining~reading-shell-scripts:~$ /challenge/run
hack the PLANET
CORRECT! Your flag:
pwn.college{EsSAYDFb13-Y5RzrSAZg2R2yceG.0lMwgDOxwiNyUDN0EzW}
```

### New Learnings
Learned that shell scripts can be inspected and understood using normal file-reading tools such as cat. Reinforced the importance of reading source code to determine how a program expects input and what conditions it checks internally. Also gained experience distinguishing between command-line arguments and standard input, as the script used read to collect user input rather than relying on positional parameters like $1.
