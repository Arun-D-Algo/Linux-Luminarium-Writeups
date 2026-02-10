# Linux Luminarium
# Module 6: Practicing Piping

## Duplicating piped data with tee
When you pipe data from one command to another, you of course no longer see it on your screen. This is not always desired: for example, you might want to see the data as it flows through between your commands to debug unintended outcomes (e.g., "why did that second command not work???").

Luckily, there is a solution! The tee command, named after a "T-splitter" from plumbing pipes, duplicates data flowing through your pipes to any number of files provided on the command line. For example:

hacker@dojo:~$ echo hi | tee pwn college
hi
hacker@dojo:~$ cat pwn
hi
hacker@dojo:~$ cat college
hi
hacker@dojo:~$
As you can see, by providing two files to tee, we ended up with three copies of the piped-in data: one to stdout, one to the pwn file, and one to the college file. You can imagine how you might use this to debug things going haywire:

hacker@dojo:~$ command_1 | command_2
Command 2 failed!
hacker@dojo:~$ command_1 | tee cmd1_output | command_2
Command 2 failed!
hacker@dojo:~$ cat cmd1_output
Command 1 failed: must pass --succeed!
hacker@dojo:~$ command_1 --succeed | command_2
Commands succeeded!
Now, you try it! This process' /challenge/pwn must be piped into /challenge/college, but you'll need to intercept the data to see what pwn needs from you!


### Solve
**Flag:** `pwn.college{AhHe2GZ2BOS9Ko16m8Ulo2ChGD6.QXxITO0wiNyUDN0EzW}`

This challenge was solved by using tee to duplicate data flowing through a pipe without interrupting it. The output of /challenge/pwn was piped into tee, which saved a copy to a file for inspection while still passing the same data onward to /challenge/college. After inspecting the intercepted output and identifying the required secret argument, /challenge/pwn was re-run with the correct flag, allowing /challenge/college to validate the input and reveal the final flag.

```bash
hacker@piping~duplicating-piped-data-with-tee:~$ /challenge/pwn | tee pwn | /challenge/college
Processing...
The input to 'college' does not contain the correct secret code! This code 
should be provided by the 'pwn' command. HINT: use 'tee' to intercept the 
output of 'pwn' and figure out what the code needs to be.
hacker@piping~duplicating-piped-data-with-tee:~$ cat pwn 
Usage: /challenge/pwn --secret [SECRET_ARG]

SECRET_ARG should be "AhHe2GZ2"
hacker@piping~duplicating-piped-data-with-tee:~$ /challenge/pwn --secret AhHe2GZ2 | /challenge/college
Processing...
Correct! Passing secret value to /challenge/college...
Great job! Here is your flag:
pwn.college{AhHe2GZ2BOS9Ko16m8Ulo2ChGD6.QXxITO0wiNyUDN0EzW}
```

### New Learnings
Learned how tee duplicates piped data, allowing simultaneous inspection and forwarding of a stream. This reinforced how Unix pipelines can be debugged non-destructively by observing intermediate data without breaking the flow between commands.