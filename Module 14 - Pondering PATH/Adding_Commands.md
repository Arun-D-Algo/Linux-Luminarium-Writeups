# Linux Luminarium
# Module 14: Pondering PATH

## Adding Commands
Recall our example from the previous level:

```
hacker@dojo:~$ ls /home/hacker/scripts
goodscript	badscript	okayscript
hacker@dojo:~$ PATH=/home/hacker/scripts
hacker@dojo:~$ goodscript
YEAH! This is the best script!
hacker@dojo:~$
```
What we see here, of course, is the hacker making the shell more useful for themselves by bringing their own commands to the party. Over time, you might amass your own elegant tools. Let's start with win!

Previously, the win command that /challenge/run executed was stored in /challenge/more_commands. This time, win does not exist! Recall the final level of Chaining Commands, and make a shell script called win, add its location to the PATH, and enable /challenge/run to find it!

Hint: /challenge/run runs as root and will call win. Thus, win can simply cat the flag file. Again, the win command is the only thing that /challenge/run needs, so you can just overwrite PATH with that one directory. But remember, if you do that, your win command won't be able to find cat.

You have three options to avoid that:

Figure out where the cat program is on the filesystem. It must be in a directory that lives in the PATH variable, so you can print the variable out (refer to Shell Variables to remember how!), and go through the directories in it (recall that the different entries are separated by :), find which one has cat in it, and invoke cat by its absolute path.
Set a PATH that has the old directories plus a new entry for wherever you create win.
Use read (again, refer to Shell Variables) to read /flag. Since read is a builtin functionality of bash, it is unaffected by PATH shenanigans.
Now, go and win!

### Solve
**Flag:** `pwn.college{oSmq5g5GXgcQiZzKy5G69666s83.QX2cjM1wiNyUDN0EzW}`

This challenge required creating a custom command named win and making it discoverable through the PATH variable. A shell script called win was created inside a custom directory and configured to print the flag using the absolute path to cat. After making the script executable, PATH was overwritten to include only the directory containing win. When /challenge/run attempted to execute win, the shell located the custom command through PATH, executed it, and revealed the flag.

```bash
hacker@path~adding-commands:~$ mkdir scripts
hacker@path~adding-commands:~$ nano scripts/win
(#!/bin/bash
/bin/cat /flag)
hacker@path~adding-commands:~$ chmod +x scripts/win
hacker@path~adding-commands:~$ PATH=/home/hacker/scripts
hacker@path~adding-commands:~$ /challenge/run
Invoking 'win'....
pwn.college{oSmq5g5GXgcQiZzKy5G69666s83.QX2cjM1wiNyUDN0EzW}
```

### New Learnings
Learned that users can create their own executable commands and expose them to the shell through the PATH variable. Reinforced that command lookup depends entirely on the directories listed in PATH, allowing custom programs to be executed by name. Also gained experience creating executable scripts, using absolute paths to avoid PATH dependency issues, and effectively extending the shell's command set.