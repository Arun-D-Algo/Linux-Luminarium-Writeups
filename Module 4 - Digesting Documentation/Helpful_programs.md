# Linux Luminarium
# Module 4: Digesting Documentation

## Helpful Programs
Some programs don't have a man page, but might tell you how to run them if invoked with a special argument. Usually, this argument is --help, but it can often be -h or, in rare cases, -?, help, or other esoteric values like /? (though that latter is more frequently encountered on Windows).

In this level, you will practice reading a program's documentation with --help. Try it out!

### Solve
**Flag:** `pwn.college{UAvf0pVuo4mQqHxv7yVo2wkeEmM.QX3IDO0wiNyUDN0EzW}`

The challenge program did not have a full manpage, so its usage needed to be discovered through the --help option. Running /challenge/challenge --help revealed multiple arguments, including a -p option that prints the secret value required for the -g (or --give-the-flag) argument. After reading the help output, the -p option was invoked to obtain the correct value. This value was then supplied to the -g flag, which caused the program to print the flag successfully.

```bash
hacker@man~helpful-programs:~$ /challenge/challenge --help
usage: a challenge to make you ask for help [-h] [--fortune] [-v]
                                            [-g GIVE_THE_FLAG] [-p]

optional arguments:
  -h, --help            show this help message and exit
  --fortune             read your fortune
  -v, --version         get the version number
  -g GIVE_THE_FLAG, --give-the-flag GIVE_THE_FLAG
                        get the flag, if given the correct value
  -p, --print-value     print the value that will cause the -g option to give
                        you the flag
hacker@man~helpful-programs:~$ /challenge/challenge -p
The secret value is: 47
hacker@man~helpful-programs:~$ /challenge/challenge -g 47
Correct usage! Your flag: pwn.college{UAvf0pVuo4mQqHxv7yVo2wkeEmM.QX3IDO0wiNyUDN0EzW}
```

### New Learnings
Learned how programs without manpages can still document their usage through built-in help options such as --help, -h, or similar flags, and how these help messages expose the required arguments to correctly use the program.