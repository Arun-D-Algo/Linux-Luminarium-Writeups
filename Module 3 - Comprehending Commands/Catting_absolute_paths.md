# Linux Luminarium
# Module 3: Comprehending Commands

## Catting absolute paths
In the last level, you did cat flag to read the flag out of your home directory! You can, of course, specify cat's arguments as absolute paths:

hacker@dojo:~$ cat /challenge/DESCRIPTION.md
In the last level, you did `cat flag` to read the flag out of your home directory!
You can, of course, specify `cat`'s arguments as absolute paths:
...
In this challenge, I will not copy it to your home directory, but I will make it readable. You can read it with cat at its absolute path: /flag.

FUN FACT: /flag is where the flag always lives in pwn.college, but unlike in this challenge, you typically can't access that file directly.

### Solve
**Flag:** `pwn.college{gXmWVU-qoHPF0Qm6UtbM_uMGHBc.QX5ETO0wiNyUDN0EzW}}`

Used the absolute path of flag with cat command to get the flag.

```bash
hacker@commands~catting-absolute-paths:~$ cat /flag
pwn.college{gXmWVU-qoHPF0Qm6UtbM_uMGHBc.QX5ETO0wiNyUDN0EzW}
```

### New Learnings
Learnt to use absolute paths with cat command.
