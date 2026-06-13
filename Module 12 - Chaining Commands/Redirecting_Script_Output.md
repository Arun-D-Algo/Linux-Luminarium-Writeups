# Linux Luminarium
# Module 12: Chaining Commands

## Redirecting Script Output
Let's try something a bit trickier! You've piped output between programs with |, but so far, this has just been between one command's output and a different command's input. But what if you wanted to send the output of several programs to one command? There are a few ways to do this, and we'll explore a simple one here: redirecting output from your script!

As far as the shell is concerned, your script is just another command. That means you can redirect its input and output just like you did for commands in the Piping module! For example, you can write it to a file:

hacker@dojo:~$ cat script.sh
echo PWN
echo COLLEGE
hacker@dojo:~$ bash script.sh > output
hacker@dojo:~$ cat output
PWN
COLLEGE
hacker@dojo:~$
All of the various redirection methods work: > for stdout, 2> for stderr, < for stdin, >> and 2>> for append-mode redirection, >& for redirecting to other file descriptors, and | for piping to another command.

In this level, we will practice piping (|) from your script to another program. Like before, you need to create a script that calls the /challenge/pwn command followed by the /challenge/college command, and pipe the output of the script into a single invocation of the /challenge/solve command!

### Solve
**Flag:** `pwn.college{wg0t25xfA27MYZdpNQKY58JNwho.QX4ETO0wiNyUDN0EzW}`

This challenge required creating a shell script that executed both /challenge/pwn and /challenge/college in sequence, then piping the script's combined output into a single invocation of /challenge/solve. A script was created containing the two required commands on separate lines. After making the script executable, its output was redirected through a pipe (|) into /challenge/solve. Since the challenge expected the outputs from both commands through a single input stream, piping the script's output satisfied the requirement and revealed the flag.

```bash
hacker@chaining~redirecting-script-output:~$ nano x.sh
 (#!/bin/bash
 /challenge/pwn
 /challenge/college)
hacker@chaining~redirecting-script-output:~$ chmod +x x.sh
hacker@chaining~redirecting-script-output:~$ ./x.sh | /challenge/solve
Correct! Here is your flag:
pwn.college{wg0t25xfA27MYZdpNQKY58JNwho.QX4ETO0wiNyUDN0EzW}
```

### New Learnings
Learned that shell scripts behave like normal commands and can participate in redirection and piping operations. Reinforced that a script's standard output can be sent directly into another program using the pipe (|) operator. Also gained experience combining multiple command outputs through a script and forwarding them as a single input stream to another process.