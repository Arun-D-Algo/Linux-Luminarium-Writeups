# Linux Luminarium
# Module 9: Processes and Jobs

## Resuming Processes
Usually, when you suspend processes, you'll want to resume them at some point. Otherwise, why not just terminate them? To resume processes, your shell provides the fg command, a builtin that takes the suspended process, resumes it, and puts it back in the foreground of your terminal.

Go try it out! This challenge's run needs you to suspend it, then resume it. Good luck!


### Solve
**Flag:** `pwn.college{IT3qyt2bXkdghE6THi8tJq6h12k.QX2QDO0wiNyUDN0EzW}`

This challenge focused on resuming a suspended process using built-in job control. When /challenge/run was executed, it asked to be suspended first. Pressing Ctrl-Z sent a stop signal to the foreground process, placing it in a suspended state while keeping it alive in memory. The shell then returned control to the prompt. Using the fg command brought that stopped job back to the foreground and resumed its execution. Once resumed properly, the program confirmed it had been suspended and restored, then revealed the flag. The task demonstrated how a process can pause and later continue exactly where it left off.

```bash
hacker@processes~resuming-processes:~$ /challenge/run
Let's practice resuming processes! Suspend me with Ctrl-Z, then resume me with 
the 'fg' command! Or just press Enter to quit me!
^Z
[1]+  Stopped                    /challenge/run
hacker@processes~resuming-processes:~$ fg
/challenge/run
I'm back! Here's your flag:
pwn.college{IT3qyt2bXkdghE6THi8tJq6h12k.QX2QDO0wiNyUDN0EzW}
Don't forget to press Enter to quit me!

Goodbye!
```

### New Learnings
Learned how the fg command resumes a suspended job and returns it to the foreground of the terminal. Reinforced the distinction between interrupting (Ctrl-C), suspending (Ctrl-Z), and resuming (fg) processes. Also strengthened understanding of shell job control and how the terminal manages the lifecycle of foreground processes without terminating them.