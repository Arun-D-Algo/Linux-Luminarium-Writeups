# Linux Luminarium
# Module 6: Practicing Piping

## Redirecting Errors
Just like standard output, you can also redirect the error channel of commands. Here, we'll learn about File Descriptor numbers. A File Descriptor (FD) is a number that describes a communication channel in Linux. You've already been using them, even though you didn't realize it. We're already familiar with three:

FD 0: Standard Input
FD 1: Standard Output
FD 2: Standard Error
When you redirect process communication, you do it by FD number, though some FD numbers are implicit. For example, a > without a number implies 1>, which redirects FD 1 (Standard Output). Thus, the following two commands are equivalent:

hacker@dojo:~$ echo hi > asdf
hacker@dojo:~$ echo hi 1> asdf
Redirecting errors is pretty easy from this point. If you have a command that might produce data via standard error (such as /challenge/run), you can do:

hacker@dojo:~$ /challenge/run 2> errors.log
That will redirect standard error (FD 2) to the errors.log file. Furthermore, you can redirect multiple file descriptors at the same time! For example:

hacker@dojo:~$ some_command > output.log 2> errors.log
That command will redirect output to output.log and errors to errors.log.

Let's put this into practice! In this challenge, you will need to redirect the output of /challenge/run, like before, to myflag, and the "errors" (in our case, the instructions) to instructions. You'll notice that nothing will be printed to the terminal, because you have redirected everything! You can find the instructions/feedback in instructions and the flag in myflag when you successfully pull this off!

### Solve
**Flag:** `pwn.college{UmWPY5b2ED5jtKHpaZ9u7nUl94G.QX3YTN0wiNyUDN0EzW}`

This challenge was solved by redirecting multiple file descriptors simultaneously. Standard output (FD 1), which contained the flag, was redirected to myflag, while standard error (FD 2), which contained the instructions and feedback, was redirected to instructions. Using /challenge/run > myflag 2> instructions ensured that all output streams were captured in the correct files and nothing was printed to the terminal.

```bash
hacker@piping~redirecting-errors:~$ /challenge/run > myflag 2> instructions
hacker@piping~redirecting-errors:~$ cat myflag

[FLAG] Here is your flag:
[FLAG] pwn.college{UmWPY5b2ED5jtKHpaZ9u7nUl94G.QX3YTN0wiNyUDN0EzW}
```

### New Learnings
Learned how file descriptor numbers control different output streams and how they can be redirected independently. This reinforced the distinction between stdout and stderr and demonstrated how combining multiple redirections provides precise control over where program output is written.