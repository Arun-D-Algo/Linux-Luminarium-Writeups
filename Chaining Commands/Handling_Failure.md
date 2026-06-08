# Linux Luminarium
# Module 12: Chaining Commands

## Handling Failure
You just learned about the && operator, which runs the second command only if the first succeeds. Now let's learn about its opposite: the || operator allows you to run a second command only if the first command fails (exits with a non-zero code). This is called the "OR" operator because either the first command succeeds OR the second command will run.

Here's the syntax:

hacker@dojo:~$ command1 || command2
This means: "Run command1, and IF it fails, then run command2."

Some examples:

hacker@dojo:~$ touch /file || echo "touch failed, so this runs"
touch: cannot touch '/file': Permission denied
touch failed, so this runs
hacker@dojo:~$ touch /home/hacker/file || echo "this will NOT run"
hacker@dojo:~$
The || operator is super useful for providing fallback commands or error handling!

In this challenge, you need to chain /challenge/first-failure and /challenge/second using the || operator. Go for it!

### Solve
**Flag:** `pwn.college{UhwUt5944SDEChpJasUSOMuEGkh.01M0MDOxwiNyUDN0EzW}`

This challenge required executing /challenge/second only if /challenge/first-failure failed. By chaining them with ||, the shell triggered the second command upon failure of the first. This satisfied the condition of the challenge, and the flag was successfully displayed.

```bash
hacker@chaining~handling-failure:~$ /challenge/first-failure || /challenge/second
Nice chaining! Flag: pwn.college{UhwUt5944SDEChpJasUSOMuEGkh.01M0MDOxwiNyUDN0EzW}
```

### New Learnings
Learned how the || operator enables fallback execution when a command fails. Reinforced that the second command runs only if the first exits with a non-zero status. Also strengthened understanding of using exit codes for basic error handling and recovery in shell workflows.