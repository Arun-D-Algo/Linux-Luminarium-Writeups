# Linux Luminarium
# Module 10: Untangling Users

## Using sudo
In the olden days, a typical Linux system had a root password that administrators would use to su to root (after logging into their account with their normal account password). But root passwords are a pain to maintain, they (or their hashes!) can leak, and they don't lend themselves well to larger environments (e.g., fleets of servers). To address this, in recent decades, the world has moved from administration via su to administration via sudo (Fun Fact: sudo originally stood for superuser do, but has changed to "su 'do'", and because su stands for "substitute user", the current meaning of sudo is "substitute user, do").

Unlike su, which defaults to launching a shell as a specified user, sudo defaults to running a command as root:

hacker@dojo:~$ whoami
hacker
hacker@dojo:~$ sudo whoami
root
hacker@dojo:~$
Or, more relevant to getting flags:

hacker@dojo:~$ grep hacker /etc/shadow
grep: /etc/shadow: Permission denied
hacker@dojo:~$ sudo grep hacker /etc/shadow
hacker:$6$Xro.e7qB3Q2Jl2sA$j6xffIgWn9xIxWUeFzvwPf.nOH2NTWNJCU5XVkPuONjIC7jL467SR4bXjpVJx4b/bkbl7kyhNquWtkNlulFoy.:19921:0:99999:7:::
hacker@dojo:~$
Unlike su, which relies on password authentication, sudo checks policies to determine whether the user is authorized to run commands as root. These policies are defined in /etc/sudoers, and though it's mostly out of scope for our purposes, there are plenty of resources for learning about this!

So, the world has moved to sudo and has (for the purposes of system administration) left su behind. In fact, even pwn.college's Privileged Mode works by giving you sudo access to elevate privileges!

In this level, we will give you sudo access, and you will use it to read the flag. Nice and easy!

NOTE: After this level, we will enable Privileged Mode! When you launch a challenge in Privileged Mode (by clicking the Privileged button instead of the Start button), the resulting container will give you full sudo access to allow you to introspect and debug to your heart's content, but of course with a placeholder flag.


### Solve
**Flag:** `pwn.college{8euMueoWy9nqObQzvZY_Ttjc0QK.QX4UDN1wiNyUDN0EzW}`

The challenge required using sudo to execute a command with root privileges instead of switching users. Unlike su, which launches a root shell after password authentication, sudo allowed authorized users to run specific commands as root based on defined policies. By executing the appropriate command with sudo, restricted access to the flag file was bypassed and the flag was successfully retrieved.

```bash
hacker@users~using-sudo:~$ sudo cat /flag
pwn.college{8euMueoWy9nqObQzvZY_Ttjc0QK.QX4UDN1wiNyUDN0EzW}
```

### New Learnings
Learned that sudo provides controlled privilege escalation based on policy rules defined in the sudoers configuration. Learned that sudo runs individual commands as root rather than launching a full root shell by default. Learned that modern Linux systems favor sudo over su for better security, accountability, and administrative control.