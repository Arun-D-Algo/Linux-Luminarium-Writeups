# Linux Luminarium
# Module 9: Processes and Jobs

## Background Processes
You've resumed processes in the foreground with the fg command. You can also resume processes in the background with the bg command! This will allow the process to keep running, while giving you your shell back to invoke more commands in the meantime.

This level's run wants to see another copy of itself running, not suspended, and using the same terminal. How? Use the terminal to launch it, then suspend it, then background it with bg and launch another copy while the first is running in the background!

ARCANUM: If you're interested in some deeper details, check out how to view the differences between suspended and backgrounded properties! Allow me to demonstrate. First, let's suspend a sleep:

hacker@dojo:~$ sleep 1337
^Z
[1]+  Stopped                 sleep 1337
hacker@dojo:~$
The sleep process is now suspended in the background. We can see this with ps by enabling the stat column output with the -o option:

hacker@dojo:~$ ps -o user,pid,stat,cmd
USER         PID STAT CMD
hacker       702 Ss   bash
hacker       762 T    sleep 1337
hacker       782 R+   ps -o user,pid,stat,cmd
hacker@dojo:~$ 
See that T? That means that the process is suspended due to our Ctrl-Z. The S in bash's STAT column means that bash is sleeping while waiting for input. The R in ps's column means that it's actively running, and the + means that it's in the foreground!

Watch what happens when we resume sleep in the background:

hacker@dojo:~$ bg
[1]+ sleep 1337 &
hacker@dojo:~$ ps -o user,pid,stat,cmd
USER         PID STAT CMD
hacker       702 Ss   bash
hacker       762 S    sleep 1337
hacker      1224 R+   ps -o user,pid,stat,cmd
hacker@dojo:~$
Boom! The sleep now has an S. It's sleeping while, well, sleeping, but it's not suspended! It's also in the background and thus doesn't have the +.


### Solve
**Flag:** `pwn.college{YpZOJaKiSkc0fgfAy7igIlp_1aM.QX3QDO0wiNyUDN0EzW}`

This challenge focused on running a suspended process in the background instead of bringing it back to the foreground. After launching /challenge/run, it required another active copy of itself that was not suspended. Pressing Ctrl-Z first suspended the process (placing it in a stopped state). Using the bg command then resumed that stopped job, but kept it running in the background, allowing the shell prompt to return immediately. With the first instance now actively running (not stopped), launching /challenge/run again created a second foreground copy. The program detected the already-running background instance and revealed the flag. This demonstrated how background execution allows multiple active processes to share the same terminal session.

```bash
hacker@processes~backgrounding-processes:~$ /challenge/run
I'll only give you the flag if there's already another copy of me running *and 
not suspended* in this terminal... Let's check!

UID          PID STAT CMD
root         347 S+   bash /challenge/run
root         349 R+   ps -o user=UID,pid,stat,cmd

I don't see a second me!

To pass this level, you need to suspend me, resume the suspended process in the 
background, and then launch a new version of me! You can background me with 
Ctrl-Z (and resume me in the background with 'bg') or, if you're not ready to 
do that for whatever reason, just hit Enter and I'll exit!
^Z
[1]+  Stopped                    /challenge/run
hacker@processes~backgrounding-processes:~$ bg
[1]+ /challenge/run &
hacker@processes~backgrounding-processes:~$ 


Yay, I'm now running the background! Because of that, this text will probably 
overlap weirdly with the shell prompt. Don't panic; just hit Enter a few times 
to scroll this text out.

hacker@processes~backgrounding-processes:~$ /challenge/run
I'll only give you the flag if there's already another copy of me running *and 
not suspended* in this terminal... Let's check!

UID          PID STAT CMD
root         347 S    bash /challenge/run
root         357 S    sleep 6h
root         358 S+   bash /challenge/run
root         360 R+   ps -o user=UID,pid,stat,cmd

Yay, I found another version of me running in the background! Here is the flag:
pwn.college{YpZOJaKiSkc0fgfAy7igIlp_1aM.QX3QDO0wiNyUDN0EzW}
```

### New Learnings
Learned how bg resumes a suspended process and allows it to continue executing in the background without taking over the terminal. Reinforced the difference between a suspended process (STAT = T) and a background running process (STAT = S without +). Strengthened understanding of shell job control, especially how Ctrl-Z, bg, and launching new commands work together to manage multiple concurrent processes within a single terminal session.