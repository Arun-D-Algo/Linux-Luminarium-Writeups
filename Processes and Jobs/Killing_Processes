# Linux Luminarium
# Module 9: Processes and Jobs

## Killing Processes
You've launched processes, you've viewed processes, now you will learn to terminate processes! In Linux, this is done using the aggressively-named kill command. With default options (which is all we'll cover in this level), kill will terminate a process in a way that gives it a chance to get its affairs in order before ceasing to exist.

Let's say you had a pesky sleep process (sleep is a program that simply hangs out for the number of seconds specified on the commandline, in this case, 1337 seconds) that you launched in another terminal, like so:

hacker@dojo:~$ sleep 1337
How do we get rid of it? You use kill to terminate it by passing the process identifier (the PID from ps) as an argument, like so:

hacker@dojo:~$ ps -e | grep sleep
 342 pts/0    00:00:00 sleep
hacker@dojo:~$ kill 342
hacker@dojo:~$ ps -e | grep sleep
hacker@dojo:~$
Now, it's time to terminate your first process! In this challenge, /challenge/run will refuse to run while /challenge/dont_run is running! You must find the dont_run process and kill it. If you fail, pwn.college will disavow all knowledge of your mission. Good luck.


### Solve
**Flag:** `pwn.college{EmnXkw-VtZrnNRKQcU5xCsLR9No.QXyQDO0wiNyUDN0EzW}`

This challenge focused on terminating a running process that was blocking another program from executing. The /challenge/dont_run process had to be identified using ps, since processes in Linux are managed by their unique Process IDs (PIDs). After locating the correct PID from the process list, the kill command was used to send a termination signal to that process. Once the blocking process was stopped, /challenge/run could execute normally and reveal the flag. The task reinforced how process control directly affects program behavior in a multi-process environment.

```bash
hacker@processes~killing-processes:~$ ps -efww | grep "/challenge/dont_run"
hacker       138     137  0 11:45 ?        00:00:00 /challenge/dont_run
hacker       369     354  0 11:47 pts/0    00:00:00 grep --color=auto /challenge/dont_run
hacker@processes~killing-processes:~$ kill 138
hacker@processes~killing-processes:~$ /challenge/run
Great job! Here is your payment:
pwn.college{EmnXkw-VtZrnNRKQcU5xCsLR9No.QXyQDO0wiNyUDN0EzW}
```

### New Learnings
Learned how the kill command terminates a process by targeting its PID and how default signals allow a program to shut down cleanly. Reinforced the practical workflow of combining ps with grep to locate specific processes before acting on them. Also strengthened understanding of how Linux handles concurrent processes, and how managing them properly is essential for system control and troubleshooting.