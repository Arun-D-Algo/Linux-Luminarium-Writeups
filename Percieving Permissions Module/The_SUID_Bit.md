# Linux Luminarium
# Module 11: Percieving Permissions

## The SUID Bit
As you explored in the previous module, there are many cases in which non-root users need elevated access to do certain system tasks. The system admin can't be there to give them the password every time a user wanted to do a task that only root/sudoers can do. Instead, the "Set User ID" (SUID) permission bit allows the user to run a program as the owner of that program's file.

This is actually the exact mechanism used to let the challenge programs you run read the flag or, outside of pwn.college, to enable system administration tools such as su, sudo, and so on. The permissions of a file with SUID look like this:

hacker@dojo:~$ ls -l /usr/bin/sudo
-rwsr-xr-x 1 root root 232416 Dec 1 11:45 /usr/bin/sudo
hacker@dojo:~$
The s part in place of the executable bit means that the program is executable with SUID. It means that, regardless of what user runs the program (as long as they have executable permissions), the program will execute as the owner user (in this case, the root user).

As the owner of a file, you can set a file's SUID bit by using chmod:

chmod u+s [program]
But be careful! Giving the SUID bit to an executable owned by root can give attackers a possible attack vector to become root. You will learn more about this in the Program Misuse module.

Now, we are going to let you add the SUID bit to the /challenge/getroot program in order to spawn a root shell for you to cat the flag yourself!

### Solve
**Flag:** `pwn.college{8NfZptr_xNV9FBQ4i70wLJYGBcH.QXzEjN0wiNyUDN0EzW}`

This challenge introduced the SUID (Set User ID) permission bit. The /challenge/getroot program was owned by root and designed to spawn a root shell when executed with the SUID bit enabled. By setting the SUID bit using chmod u+s, the program executed with the privileges of its owner (root) rather than the current user. Running the program provided a root shell, which allowed direct access to /flag.

```bash
hacker@permissions~the-suid-bit:~$ chmod u+s /challenge/getroot
hacker@permissions~the-suid-bit:~$ ls -l /challenge/getroot
-rwsr-xr-x 1 root root 175 Jun 12 10:19 /challenge/getroot
hacker@permissions~the-suid-bit:~$ /challenge/getroot
SUCCESS! You have set the suid bit on this program, and it is running as root! 
Here is your shell...
root@permissions~the-suid-bit:/home/hacker# cat /flag
pwn.college{8NfZptr_xNV9FBQ4i70wLJYGBcH.QXzEjN0wiNyUDN0EzW}
```

### New Learnings
Learned about the SUID (Set User ID) permission bit and how it allows a program to run with the privileges of its owner instead of the user who launched it. Reinforced how Linux permissions can influence not just file access but also process privileges. Also gained experience setting the SUID bit with chmod u+s, identifying it through the s in permission strings such as -rwsr-xr-x, and understanding why SUID programs like sudo are powerful and potentially dangerous from a security perspective.