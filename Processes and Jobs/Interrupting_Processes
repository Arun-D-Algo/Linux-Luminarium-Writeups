# Linux Luminarium
# Module 9: Processes and Jobs

## Interrupting Processes
You've learned how to kill other processes with the kill command, but sometimes you just want to get rid of the process that's clogging up your terminal! Luckily, terminals have a hotkey for this: Ctrl-C (e.g., holding down the Ctrl key and pressing C) sends an "interrupt" to whatever application is waiting on input from the terminal and, typically, this causes the application to cleanly exit.

Try it here! /challenge/run will refuse to give you the flag until you interrupt it. Good luck!

For the very interested, check out this article about terminals and "control codes" (such as Ctrl-C).


### Solve
**Flag:** `pwn.college{sNarpai3srNi22WVzhDr8D7D96N.QXzQDO0wiNyUDN0EzW}`

This challenge centered on interrupting a running process directly from the terminal instead of killing it from another session. When /challenge/run was executed, it deliberately waited and refused to provide the flag until it was interrupted. Pressing Ctrl-C sent an interrupt signal (SIGINT) from the terminal to the running foreground process, causing it to exit immediately. Once interrupted, the program acknowledged the signal and revealed the flag. The task demonstrated how terminals communicate control signals to active programs.

```bash
hacker@processes~interrupting-processes:~$ /challenge/run
I could give you the flag... but I won't, until this process exits. Remember, 
you can force me to exit with Ctrl-C. Try it now!
^C
Good job! You have used Ctrl-C to interrupt this process! Here is your flag:
pwn.college{sNarpai3srNi22WVzhDr8D7D96N.QXzQDO0wiNyUDN0EzW}
```

### New Learnings
Learned that Ctrl-C sends a SIGINT signal to the foreground process attached to the terminal, allowing it to terminate cleanly without using the kill command. Reinforced the difference between manually killing a process by PID and interrupting the currently running process directly through terminal control signals. Also strengthened understanding of how the terminal manages foreground jobs and how user input can directly influence process execution.