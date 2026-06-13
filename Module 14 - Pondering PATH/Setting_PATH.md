# Linux Luminarium
# Module 14: Pondering PATH

## Setting PATH
Okay, so things break when you blank out PATH. But what about doing something useful with PATH?

Let's explore how we would, for example, add a new directory of programs to our command repertoire. Recall that PATH stores a list of directories to find commands in and, for commands in nonstandard places, we must typically execute them via their path:

```
hacker@dojo:~$ ls /home/hacker/scripts
goodscript	badscript	okayscript
hacker@dojo:~$ goodscript
bash: goodscript: command not found
hacker@dojo:~$ /home/hacker/scripts/goodscript
YEAH! This is the best script!
hacker@dojo:~$
```
If you maintain useful scripts that you want to be able to launch by bare name, this is annoying. However, by adding directories to or replacing directories in this list, you can expose these programs to be launched using their bare name! For example:

```
hacker@dojo:~$ PATH=/home/hacker/scripts
hacker@dojo:~$ goodscript
YEAH! This is the best script!
hacker@dojo:~$
```
Let's practice. This level's /challenge/run will run the win command via its bare name, but this command exists in the /challenge/more_commands/ directory, which is not initially in the PATH. The win command is the only thing that /challenge/run needs, so you can just overwrite PATH with that one directory. Good luck!

### Solve
**Flag:** `pwn.college{4QHGoGTfCSEMIUiaiARS1FkX6IE.QX1cjM1wiNyUDN0EzW}`

This challenge required modifying the PATH variable so that the shell could locate the win command. The challenge program attempted to execute win by name, but the command was located in /challenge/more_commands/, which was not initially included in PATH. By setting PATH to /challenge/more_commands/, the shell successfully found and executed win, causing the challenge to reveal the flag.

```bash
hacker@path~setting-path:~$ PATH=/challenge/more_commands/
hacker@path~setting-path:~$ /challenge/run
Invoking 'win'....
Congratulations! You properly set the flag and 'win' has launched!
pwn.college{4QHGoGTfCSEMIUiaiARS1FkX6IE.QX1cjM1wiNyUDN0EzW}
```

### New Learnings
Learned that PATH can be modified to include directories containing custom executables and scripts. Reinforced that when a command is entered without a path, Bash searches the directories listed in PATH to locate it. Also gained experience configuring PATH to expose commands that would otherwise require their full filesystem path to execute.
