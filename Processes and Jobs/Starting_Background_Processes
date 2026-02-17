# Linux Luminarium
# Module 9: Processes and Jobs

## Starting Background Processes
Of course, you don't have to suspend processes to background them: you can start them backgrounded right off the bat! It's easy; all you have to do is append a & to the command, like so:

hacker@dojo:~$ sleep 1337 &
[1] 1771
hacker@dojo:~$ ps -o user,pid,stat,cmd
USER         PID STAT CMD
hacker      1709 Ss   bash
hacker      1771 S    sleep 1337
hacker      1782 R+   ps -o user,pid,stat,cmd
hacker@dojo:~$ 
Here, sleep is actively running in the background, not suspended. Now it's your turn to practice! Launch /challenge/run backgrounded for the flag!


### Solve
**Flag:** `pwn.college{EcUqSRi_SeWj76MDU-_Ckef9IwC.QX5QDO0wiNyUDN0EzW}`

This challenge demonstrated how a process can be started directly in the background without first suspending it. By appending & to /challenge/run, the shell immediately launched the program as a background job, returning control of the terminal to the user while the process continued running. Because it was never suspended, it showed up as actively running rather than stopped. The program detected that it had been started in the background and printed the flag while the shell prompt remained usable.

```bash
hacker@processes~starting-backgrounded-processes:~$ /challenge/run &
[1] 348
hacker@processes~starting-backgrounded-processes:~$ 


Yay, you started me in the background! Because of that, this text will probably 
overlap weirdly with the shell prompt, but you're used to that by now...

Anyways! Here is your flag!
pwn.college{EcUqSRi_SeWj76MDU-_Ckef9IwC.QX5QDO0wiNyUDN0EzW}
```

### New Learnings
Learned that adding & to a command starts it as a background job from the beginning, avoiding the need for Ctrl-Z and bg. Reinforced the distinction between a suspended process (stopped with SIGTSTP) and a backgrounded process that is actively running. Strengthened understanding of shell job control and how the terminal can manage multiple concurrent processes while remaining interactive.