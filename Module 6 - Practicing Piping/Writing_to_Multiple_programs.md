# Linux Luminarium
# Module 6: Practicing Piping

## Writing to Multiple Programs
Now you've learned that process substitution can make command output appear as files for reading with <(command). But you can also use process substitution for writing to commands!

You can duplicate data to two files with tee:

```
hacker@dojo:~$ echo HACK | tee THE > PLANET
hacker@dojo:~$ cat THE
HACK
hacker@dojo:~$ cat PLANET
HACK
hacker@dojo:~$
```
And you've used tee to duplicate data to a file and a command:

```
hacker@dojo:~$ echo HACK | tee THE | cat
HACK
hacker@dojo:~$ cat THE
HACK
hacker@dojo:~$
```
But what about duplicating to two commands? As tee says in its manpage, it's designed to write to files and to standard output:

```
TEE(1)                           User Commands                          TEE(1)

NAME
       tee - read from standard input and write to standard output and files
```
But wait! You just learned that bash can make commands look like files using process substitution! For writing to a command (output process substitution), use >(command). If you write an argument of >(rev), bash will run the rev command (this command reads data from standard input, reverses its order, and writes it to standard output!), but hook up its input to a temporary named pipe file. When commands write to this file, the data goes to the standard input of the command:

```
hacker@dojo:~$ echo HACK | rev
KCAH
hacker@dojo:~$ echo HACK | tee >(rev)
HACK
KCAH
```
Above, the following sequence of events took place:

bash started up the rev command, hooking a named pipe (presumably /dev/fd/63) to rev's standard input
bash started up the tee command, hooking a pipe to its standard input, and replacing the first argument to tee with /dev/fd/63. tee never even saw the argument >(rev); the shell substituted it before launching tee
bash used the echo builtin to print HACK into tee's standard input
tee read HACK, wrote it to standard output, and then wrote it to /dev/fd/63 (which is connected to rev's stdin)
rev read HACK from its standard input, reversed it, and wrote KCAH to standard output
Now it's your turn! In this challenge, we have /challenge/hack, /challenge/the, and /challenge/planet. Run the /challenge/hack command, and duplicate its output as input to both the /challenge/the and the /challenge/planet commands! Scroll back through the previous challenges "Duplicating piped data with tee" and "Process substitution for input" if you need a refresher on this method.

Trivia!

The observant learner will realize that the following are equivalent:

```
hacker@dojo:~$ echo hi | rev
ih
hacker@dojo:~$ echo hi > >(rev)
ih
hacker@dojo:~$
```
More than one way to pipe data! Of course, the second route is way harder to read and also harder to expand. For example:

```
hacker@dojo:~$ echo hi | rev | rev
hi
hacker@dojo:~$ echo hi > >(rev | rev)
hi
hacker@dojo:~$
```
That's just silly! The lesson here is that, while Process Substitution is a powerful tool in your toolbox, it's a very specialized tool; don't use it for everything!

### Solve
**Flag:** `pwn.college{w67QKV2k2E6ZTt-J9zIhaFMe4le.QXwgDN1wiNyUDN0EzW}`

This challenge required sending the output of /challenge/hack to both /challenge/the and /challenge/planet at the same time. A normal pipe could only deliver the data to one program, so tee was used to duplicate the stream. Process substitution created a file-like destination connected to /challenge/the, while the original output stream continued through the pipe to /challenge/planet. The command /challenge/hack | tee >(/challenge/the) | /challenge/planet ensured that both programs received the exact same data simultaneously, satisfying the challenge requirements and revealing the flag.

```bash
hacker@piping~writing-to-multiple-programs:~$ /challenge/hack | tee >(/challenge/the) | /challenge/planet
Congratulations, you have duplicated data into the input of two programs! Here 
is your flag:
pwn.college{w67QKV2k2E6ZTt-J9zIhaFMe4le.QXwgDN1wiNyUDN0EzW}
```

### New Learnings
Learned how output process substitution (>(command)) allows a program's input to be exposed as a writable file-like target. Reinforced how tee can duplicate a data stream so that the same input can be delivered to multiple destinations simultaneously. Also gained experience combining pipes, tee, and process substitution to send identical data to multiple programs without creating temporary files.