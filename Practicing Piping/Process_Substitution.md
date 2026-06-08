# Linux Luminarium
# Module 6: Practicing Piping

## Process Substitution for input
Sometimes you need to compare the output of two commands rather than two files. You might think to save each output to a file first:

hacker@dojo:~$ command1 > file1
hacker@dojo:~$ command2 > file2
hacker@dojo:~$ diff file1 file2
But there's a more elegant way! Linux follows the philosophy that "everything is a file". That is, the system strives to provide file-like access to most resources, including the input and output of running programs! The shell follows this philosophy, allowing you to, for example, use any utility that takes file arguments on the command line and hook it up to the output of programs, as you learned in the previous few levels.

Interestingly, we can go further, and hook input and output of programs to arguments of commands. This is done using Process Substitution. For reading from a command (input process substitution), use <(command). When you write <(command), bash will run the command and hook up its output to a temporary file that it will create. This isn't a real file, of course, it's what's called a named pipe, in that it has a file name:

hacker@dojo:~$ echo <(echo hi)
/dev/fd/63
hacker@dojo:~$
Where did /dev/fd/63 come from? bash replaced <(echo hi) with the path of the named pipe file that's hooked up to the command's output! While the command is running, reading from this file will read data from the standard output of the command. Typically, this is done using commands that take input files as arguments:

hacker@dojo:~$ cat <(echo hi)
hi
hacker@dojo:~$
Of course, you can specify this multiple times:

hacker@dojo:~$ echo <(echo pwn) <(echo college)
/dev/fd/63 /dev/fd/64
hacker@dojo:~$ cat <(echo pwn) <(echo college)
pwn
college
hacker@dojo:~$
Now for your challenge! Recall what you learned in the diff challenge from Comprehending Commands. In that challenge, you diffed two files. Now, you'll diff two sets of command outputs: /challenge/print_decoys, which will print a bunch of decoy flags, and /challenge/print_decoys_and_flag which will print those same decoys plus the real flag.

Use process substitution with diff to compare the outputs of these two programs and find your flag!


### Solve
**Flag:** `pwn.college{UvjS3gc4uXSWl_wHQfwnyv_dhw6.0lNwMDOxwiNyUDN0EzW}`

This challenge required comparing the outputs of two programs: /challenge/print_decoys, which printed only decoy flags, and /challenge/print_decoys_and_flag, which printed the same decoys plus the real flag. Instead of saving both outputs to separate files, process substitution was used to feed each command's output directly into diff. The command diff <(/challenge/print_decoys) <(/challenge/print_decoys_and_flag) compared the two streams and displayed only the difference between them. Since the outputs were nearly identical, the additional line shown by diff was the real flag, which completed the challenge.

```bash
hacker@piping~process-substitution-for-input:~$ diff <(/challenge/print_decoys) <(/challenge/print_decoys_and_flag)
27a28
> pwn.college{UvjS3gc4uXSWl_wHQfwnyv_dhw6.0lNwMDOxwiNyUDN0EzW}
```

### New Learnings
Learned how process substitution (<(command)) allows the output of a command to be treated as a temporary file. Reinforced that Bash creates special file descriptors, often under /dev/fd/, which can be passed as arguments to commands expecting filenames. Also gained experience using process substitution with diff to compare command outputs directly without creating intermediate files.