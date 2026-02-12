# Linux Luminarium
# Module 6: Practicing Piping

## Redirecting Output
First, let's look at redirecting stdout to files. You can accomplish this with the > character, as so:

hacker@dojo:~$ echo hi > asdf
This will redirect the output of echo hi (which will be hi) to the file asdf. You can then use a program such as cat to output this file:

hacker@dojo:~$ cat asdf
hi
In this challenge, you must use this output redirection to write the word PWN (all uppercase) to the filename COLLEGE (all uppercase).

### Solve
**Flag:** `pwn.college{QleSX8acS5tFpBnBWJURPV6pBBv.QX0YTN0wiNyUDN0EzW}`

This challenge was solved by redirecting standard output to a file using the > operator. The command echo PWN > COLLEGE redirected the output of echo into a file named COLLEGE, satisfying the requirement to write the exact uppercase text into an uppercase filename and revealing the flag.

```bash
hacker@piping~redirecting-output:~$ echo PWN > COLLEGE
Correct! You successfully redirected 'PWN' to the file 'COLLEGE'! Here is your 
flag:
pwn.college{QleSX8acS5tFpBnBWJURPV6pBBv.QX0YTN0wiNyUDN0EzW}
```

### New Learnings
Learned how output redirection (>) sends a command’s stdout to a file instead of the terminal. This reinforced the idea that redirection is handled by the shell, not the command itself, and is a fundamental building block for more advanced piping and file manipulation in Unix systems.