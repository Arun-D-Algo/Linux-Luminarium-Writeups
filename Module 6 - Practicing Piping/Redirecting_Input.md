# Linux Luminarium
# Module 6: Practicing Piping

## Redirecting Input
Just like you can redirect output from programs, you can redirect input to programs! This is done using <, as so:

hacker@dojo:~$ echo yo > message
hacker@dojo:~$ cat message
yo
hacker@dojo:~$ rev < message
oy
You can do interesting things with a lot of different programs using input redirection! In this level, we will practice using /challenge/run, which will require you to redirect the PWN file to it and have the PWN file contain the value COLLEGE! To write that value to the PWN file, recall the prior challenge on output redirection from echo!

### Solve
**Flag:** `pwn.college{g2YkHBlfh4a0rQC9sket4vq5yGb.QXwcTN0wiNyUDN0EzW}`

This challenge was solved by combining output redirection and input redirection. First, the required value was written into a file using echo COLLEGE > PWN. Then, the file was redirected into /challenge/run using <, causing the program to read COLLEGE from standard input instead of the keyboard and return the flag.

```bash
hacker@piping~redirecting-input:~$ echo COLLEGE > PWN
hacker@piping~redirecting-input:~$ /challenge/run < PWN
Reading from standard input...
Correct! You have redirected the PWN file into my standard input, and I read 
the value 'COLLEGE' out of it!
Here is your flag:
pwn.college{g2YkHBlfh4a0rQC9sket4vq5yGb.QXwcTN0wiNyUDN0EzW}
```

### New Learnings
Learned how input redirection (<) feeds file contents into a program’s standard input, allowing programs to consume data non-interactively. This reinforced how input and output redirection work together to fully control a program’s data flow in Unix systems.