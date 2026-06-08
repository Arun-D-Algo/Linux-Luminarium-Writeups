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
**Flag:** `pwn.college{wfoEldD48tWaP99g2rO9oaPS7rY.QXxcDO0wiNyUDN0EzW}`

This challenge required running /challenge/first-success and /challenge/second such that the second command executes only if the first succeeds. By chaining them with &&, the shell ensured /challenge/second ran only after /challenge/first-success completed successfully. This satisfied the challenge condition, and the flag was displayed as expected.

```bash
hacker@chaining~your-first-shell-script:~$ echo "/challenge/pwn" > x.sh
echo "/challenge/college" >> x.sh
hacker@chaining~your-first-shell-script:~$ bash x.sh
Great job, you've written your first shell script! Here is the flag:
pwn.college{wfoEldD48tWaP99g2rO9oaPS7rY.QXxcDO0wiNyUDN0EzW}
```

### New Learnings
Learned how the && operator enables conditional command execution based on exit status. Reinforced that a command runs only if the previous one succeeds (exit code 0). Also strengthened understanding of how Linux uses exit codes to control flow in command chaining, making workflows more reliable and dependent on successful execution.