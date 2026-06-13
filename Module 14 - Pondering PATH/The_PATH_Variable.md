# Linux Luminarium
# Module 14: Pondering PATH

## The PATH Variable
It turns out that the answer to "How does the shell find ls?" is fairly simple. There is a special shell variable, called PATH, that stores a bunch of directory paths in which the shell will search for programs corresponding to commands. If you blank out the variable, things go badly:

```
hacker@dojo:~$ ls
Desktop    Downloads  Pictures  Templates
Documents  Music      Public    Videos
hacker@dojo:~$ PATH=""
hacker@dojo:~$ ls
bash: ls: No such file or directory
hacker@dojo:~$
```
Without a PATH, bash cannot find the ls command.

In this level, you will disrupt the operation of the /challenge/run program. This program will DELETE the flag file using the rm command. However, if it can't find the rm command, the flag will not be deleted, and the challenge will give it to you! Thus, you must make it so that /challenge/run also can't find the rm command!

Keep in mind: if you don't succeed, and the flag gets deleted, you will need to restart the challenge to try again!

### Solve
**Flag:** `pwn.college{Qxp6Tf4vP1TpVDqIqMkaakCjQi4.QX2cDM1wiNyUDN0EzW}`

This challenge required preventing the challenge program from finding the rm command. Since Bash locates commands using the PATH environment variable, setting PATH to an empty string stopped the shell from finding rm. When /challenge/run attempted to delete the flag, the command failed, leaving the flag intact. The challenge then detected that the flag still existed and printed it.

```bash
hacker@path~the-path-variable:~$ PATH=""
hacker@path~the-path-variable:~$ /challenge/run
Trying to remove /flag...
/challenge/run: line 4: rm: No such file or directory
The flag is still there! I might as well give it to you!
pwn.college{Qxp6Tf4vP1TpVDqIqMkaakCjQi4.QX2cDM1wiNyUDN0EzW}
```

### New Learnings
Learned that the PATH environment variable controls where Bash searches for executable programs. Reinforced that commands such as ls, rm, and cat work because their directories are listed in PATH. Also gained experience modifying environment variables and observed how clearing PATH prevents the shell from locating commands by name.
