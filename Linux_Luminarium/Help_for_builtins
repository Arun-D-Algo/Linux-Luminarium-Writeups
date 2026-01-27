# Linux Luminarium
# Module 4: Digesting Documentation

## Help for Builtins
Some commands, rather than being programs with man pages and help options, are built into the shell itself. These are called builtins. Builtins are invoked just like commands, but the shell handles them internally instead of launching other programs. You can get a list of shell builtins by running the builtin help, as so:

hacker@dojo:~$ help
You can get help on a specific one by passing it to the help builtin. Let's look at a builtin that we've already used earlier, cd!

hacker@dojo:~$ help cd
cd: cd [-L|[-P [-e]] [-@]] [dir]
    Change the shell working directory.
    
    Change the current directory to DIR.  The default DIR is the value of the
    HOME shell variable.
...
Some good information! In this challenge, we'll practice using help to look up help for builtins. This challenge's challenge command is a shell builtin, rather than a program. Like before, you need to lookup its help to figure out the secret value to pass to it!

### Solve
**Flag:** `pwn.college{oj1HF4gIKz0LDwtyGeGy0TcoXPD.QX0ETO0wiNyUDN0EzW}`

The challenge binary was actually a shell builtin, so normal --help or man wouldn’t work. Instead, it had to be inspected using the shell’s builtin help command. Running help challenge revealed the valid arguments for the builtin along with the exact secret value required for the --secret option. Supplying that value to challenge --secret printed the flag.

```bash
hacker@man~help-for-builtins:~$ help challenge 
challenge: challenge [--fortune] [--version] [--secret SECRET]
    This builtin command will read you the flag, given the right arguments!
    
    Options:
      --fortune		display a fortune
      --version		display the version
      --secret VALUE	prints the flag, if VALUE is correct

    You must be sure to provide the right value to --secret. That value
    is "oj1HF4gI".
hacker@man~help-for-builtins:~$ challenge --secret oj1HF4gI
Correct! Here is your flag!
pwn.college{oj1HF4gIKz0LDwtyGeGy0TcoXPD.QX0ETO0wiNyUDN0EzW}
```

### New Learnings
Learned that some commands in Linux are implemented as shell builtins, not external programs, and therefore must be inspected using the shell’s internal help mechanism rather than man or program-level help flags. Also reinforced how builtins expose their own argument formats and how documentation can embed required values directly within the help text.