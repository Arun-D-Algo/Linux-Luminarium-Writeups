# Linux Luminarium
# Module 14: Pondering PATH

## Adding Commands
Recall our example from the previous level:

hacker@dojo:~$ ls /home/hacker/scripts
goodscript	badscript	okayscript
hacker@dojo:~$ PATH=/home/hacker/scripts
hacker@dojo:~$ goodscript
YEAH! This is the best script!
hacker@dojo:~$
What we see here, of course, is the hacker making the shell more useful for themselves by bringing their own commands to the party. Over time, you might amass your own elegant tools. Let's start with win!

Previously, the win command that /challenge/run executed was stored in /challenge/more_commands. This time, win does not exist! Recall the final level of Chaining Commands, and make a shell script called win, add its location to the PATH, and enable /challenge/run to find it!

Hint: /challenge/run runs as root and will call win. Thus, win can simply cat the flag file. Again, the win command is the only thing that /challenge/run needs, so you can just overwrite PATH with that one directory. But remember, if you do that, your win command won't be able to find cat.

You have three options to avoid that:

Figure out where the cat program is on the filesystem. It must be in a directory that lives in the PATH variable, so you can print the variable out (refer to Shell Variables to remember how!), and go through the directories in it (recall that the different entries are separated by :), find which one has cat in it, and invoke cat by its absolute path.
Set a PATH that has the old directories plus a new entry for wherever you create win.
Use read (again, refer to Shell Variables) to read /flag. Since read is a builtin functionality of bash, it is unaffected by PATH shenanigans.
Now, go and win!


### Solve
**Flag:** `pwn.college{ItpjhUpVKdKPD1aTZNjvuohZzaD.01NzEzNxwiNyUDN0EzW}`

This challenge introduced the which command, which reveals the exact executable file that Bash will run when a command is entered. The challenge placed a win executable somewhere in the directories listed in PATH, but the flag itself was stored in the same directory as that executable. Using which win revealed the location of the win command. After navigating to its parent directory, the readable flag file was located and displayed with cat, revealing the flag.

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
Learned that the which command shows the exact executable that Bash finds when searching through PATH. Reinforced how command lookup works by checking directories in PATH from left to right until a matching executable is found. Also gained experience locating executables and using their filesystem location to discover related files stored in the same directory.
