# Linux Luminarium
# Module 14: Pondering PATH

## Finding Commands
When you type the name of a command, something inside one of the many directories listed in your $PATH variable is what actually gets executed (of course, unless the command is a builtin!). But which file, precisely? You can find out with the aptly-named which command:

```
hacker@dojo:~$ which cat
/bin/cat
hacker@dojo:~$ /bin/cat /flag
YEAH
hacker@dojo:~$
```
Mirroring what the shell does when searching for commands, which looks at each directory in $PATH in order and prints the first file it finds whose name matches the argument you passed.

In this challenge, we added a win command somewhere in your $PATH, but it won't give you the flag. Instead, it's in the same directory as a flag file that we made readable by you! You must find win (with the which command), and cat the flag out of that directory!

### Solve
**Flag:** `pwn.college{ItpjhUpVKdKPD1aTZNjvuohZzaD.01NzEzNxwiNyUDN0EzW}`

This challenge required modifying the PATH variable so that the shell could locate the win command. The challenge program attempted to execute win by name, but the command was located in /challenge/more_commands/, which was not initially included in PATH. By setting PATH to /challenge/more_commands/, the shell successfully found and executed win, causing the challenge to reveal the flag.

```bash
hacker@path~finding-commands:~$ which win
/challenge/paths/29291/win
hacker@path~finding-commands:~$ cd /challenge/paths/29291
hacker@path~finding-commands:/challenge/paths/29291$ ls
flag  win
hacker@path~finding-commands:/challenge/paths/29291$ cat flag
pwn.college{ItpjhUpVKdKPD1aTZNjvuohZzaD.01NzEzNxwiNyUDN0EzW}
```

### New Learnings
Learned that PATH can be modified to include directories containing custom executables and scripts. Reinforced that when a command is entered without a path, Bash searches the directories listed in PATH to locate it. Also gained experience configuring PATH to expose commands that would otherwise require their full filesystem path to execute.
