# Linux Luminarium
# Module 9: Processes and Jobs

## Process Exit Codes
Every shell command, including every program and every builtin, exits with an exit code when it finishes running and terminates. This can be used by the shell, or the user of the shell (that's you!) to check if the process succeeded in its functionality (this determination, of course, depends on what the process is supposed to do in the first place).

You can access the exit code of the most recently-terminated command using the special ? variable (don't forget to prepend it with $ to read its value!):

hacker@dojo:~$ touch test-file
hacker@dojo:~$ echo $?
0
hacker@dojo:~$ touch /test-file
touch: cannot touch '/test-file': Permission denied
hacker@dojo:~$ echo $?
1
hacker@dojo:~$
As you can see, commands that succeed typically return 0 and commands that fail typically return a non-zero value, most commonly 1 but sometimes an error code that identifies a specific failure mode.

In this challenge, you must retrieve the exit code returned by /challenge/get-code and then run /challenge/submit-code with that error code as an argument. Good luck!


### Solve
**Flag:** `pwn.college{8IaDtWjIelpehBUyUa_Som2zlV_.QX5YDO1wiNyUDN0EzW}`

This challenge focused on understanding process exit codes and how the shell tracks the success or failure of commands. When /challenge/get-code was executed, it intentionally exited with a specific non-zero status code. Instead of printing that number directly, the program relied on the shell’s built-in mechanism for storing the exit status of the most recently completed command. By checking $?, the stored exit code was revealed. That numeric value then had to be passed as an argument to /challenge/submit-code, which validated it and returned the flag. The key idea was recognizing that every process communicates its result back to the shell through an exit status, even if nothing obvious is printed.

```bash
hacker@processes~process-exit-codes:~$ /challenge/get-code
Exiting with an error code!
hacker@processes~process-exit-codes:~$ echo $?
31
hacker@processes~process-exit-codes:~$ /challenge/submit-code 31
CORRECT! Here is your flag:
pwn.college{8IaDtWjIelpehBUyUa_Som2zlV_.QX5YDO1wiNyUDN0EzW}
```

### New Learnings
Learned that every command in Linux terminates with an exit code, where 0 typically indicates success and non-zero values indicate failure or special conditions. Reinforced that $? always contains the exit status of the most recently executed command and must be checked immediately before running anything else. Strengthened understanding of how shells use exit codes for flow control, validation, and scripting logic, forming the foundation for conditional execution in more advanced shell usage.