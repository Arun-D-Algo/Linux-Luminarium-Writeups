# Linux Luminarium
# Module 12: Chaining Commands

## Your First Shell Script
As you combine more and more commands to achieve complex effects, the length of the combined prompt quickly gets really annoying to deal with. When this happens, you can put these commands in a file, called a shell script, and run them by executing the file! For example, consider our semicolon technique:

hacker@dojo:~$ echo COLLEGE > pwn; cat pwn
COLLEGE
hacker@dojo:~$
We can create a shell script called pwn.sh (by convention, shell scripts are frequently named with a sh suffix):

echo COLLEGE > pwn
cat pwn
And then we can execute by passing it as an argument to a new instance of our shell (bash)! When a shell is invoked like this, rather than taking commands from the user, it reads commands from the file.

hacker@dojo:~$ ls
hacker@dojo:~$ bash pwn.sh
COLLEGE
hacker@dojo:~$ ls
pwn
hacker@dojo:~$
You can see that the shell script executed both commands, creating and printing the pwn file.

Now, it's your turn! Same as last level, run /challenge/pwn and then /challenge/college, but this time in a shell script called x.sh, then run it with bash!

NOTE: We haven't yet talked about Linux's amazing array of competent command line file editors. For now, feel free to use the Text Editor application in Desktop mode (Applications->Accessories->Text Editor) or the default editor in the VSCode Workspace!

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