# Linux Luminarium
# Module 11: Percieving Permissions

## Executable Files
So far, you have mostly been dealing with read permissions. This makes sense, because you have been making the /flag file readable to read it. In this level, we will explore execute permissions.

When you invoke a program, such as /challenge/run, Linux will only actually execute it if you have execute-access to the program file. Consider:

hacker@dojo:~$ ls -l /challenge/run
-rwxr-xr-x 1 root root    0 May 22 13:42 /challenge/run
hacker@dojo:~$ /challenge/run
Successfully ran the challenge!
hacker@dojo:~$
In this case, /challenge/run runs because it is executable by the hacker user. Because the file is owned by the root user and root group, this requires that the execute bit is set on the other permissions. If we remove these permissions, the execution will fail!

hacker@dojo:~$ chmod o-x /challenge/run
hacker@dojo:~$ ls -l /challenge/run
-rwxr-xr-- 1 root root    0 May 22 13:42 /challenge/run
hacker@dojo:~$ /challenge/run
bash: /challenge/run: Permission denied
hacker@dojo:~$
In this challenge, the /challenge/run program will give you the flag, but you must first make it executable! Remember your chmod, and get /challenge/run to tell you the flag!

### Solve
**Flag:** `pwn.college{0LWNqFYmTkfQ4A3nnvpiJ6rGvQB.QXyEjN0wiNyUDN0EzW}`

This challenge focused on execute permissions. The /challenge/run program contained the flag, but it could not be executed because the execute bit was missing for the current user. Using chmod, execute permission was added to the file, allowing it to be launched normally. Once the program became executable, running it revealed the flag.

```bash
hacker@permissions~executable-files:~$ chmod u+x /challenge/run
hacker@permissions~executable-files:~$ /challenge/run
Successful execution! Here is your flag:
pwn.college{0LWNqFYmTkfQ4A3nnvpiJ6rGvQB.QXyEjN0wiNyUDN0EzW}
```

### New Learnings
Learned that the execute (x) permission controls whether a file can be run as a program. Reinforced that having read permission alone is not enough to execute a file, and that Linux checks the execute bit before launching a program. Building on the previous challenge's permission concepts, this level demonstrated how chmod can be used not only to grant read access but also to make files executable. Also gained experience interpreting the x permission bit in ls -l output and understanding its role in program execution.