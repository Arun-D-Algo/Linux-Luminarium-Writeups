# Linux Luminarium
# Module 12: Chaining Commands

## Building on Success
You learned about exit codes in the Processes module. Now let's use them to chain commands together!

The && operator allows you to run a second command only if the first command succeeds (in Linux convention, this means it exited with code 0). This is called the "AND" operator because both conditions must be true: the first command must succeed AND then the second command will run. That's super useful for complex commandline workflows where certain actions depend on the success of other actions.

Here's the syntax:

hacker@dojo:~$ command1 && command2
This means: "Run command1, and IF it succeeds, then run command2."

Some examples:

hacker@dojo:~$ touch /home/hacker/file && echo "this will run"
success
this will run
hacker@dojo:~$ touch /file && echo "this will NOT run"
touch: cannot touch '/file': Permission denied
hacker@dojo:~$
That second invocation of touch failed because the hacker user does not have write access to /file, so the echo did not run.

In this challenge, you need to chain the programs /challenge/first-success and /challenge/second using the && operator. Try running each command separately first to see what happens (which is that you will not get the flag). But if you chain them with &&, the flag will appear!

### Solve
**Flag:** `pwn.college{knZLVr6b63Ux2ik0vSMpEOckY1F.0lM0MDOxwiNyUDN0EzW}`

This challenge required running /challenge/first-success and /challenge/second such that the second command executes only if the first succeeds. By chaining them with &&, the shell ensured /challenge/second ran only after /challenge/first-success completed successfully. This satisfied the challenge condition, and the flag was displayed as expected.

```bash
hacker@chaining~building-on-success:~$ /challenge/first-success && /challenge/second
Nice chaining! Flag: pwn.college{knZLVr6b63Ux2ik0vSMpEOckY1F.0lM0MDOxwiNyUDN0EzW}
```

### New Learnings
Learned how the && operator enables conditional command execution based on exit status. Reinforced that a command runs only if the previous one succeeds (exit code 0). Also strengthened understanding of how Linux uses exit codes to control flow in command chaining, making workflows more reliable and dependent on successful execution.