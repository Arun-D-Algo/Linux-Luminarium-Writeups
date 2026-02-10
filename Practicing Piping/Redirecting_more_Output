# Linux Luminarium
# Module 6: Practicing Piping

## Redirecting more Output
Aside from redirecting the output of echo, you can, of course, redirect the output of any command. In this level, /challenge/run will once more give you a flag, but only if you redirect its output to the file myflag. Your flag will, of course, end up in the myflag file!

You'll notice that /challenge/run will still happily print to your terminal, despite you redirecting stdout. That's because it communicates its instructions and feedback over standard error, and only prints the flag over standard out!

### Solve
**Flag:** `pwn.college{wQ69KzIgbLiIGGjvelyBd1RPlv8.QX1YTN0wiNyUDN0EzW}`

This challenge was solved by redirecting the standard output of a command to a file using the > operator. Running /challenge/run > myflag redirected only the flag output (stdout) into the file myflag, while status and feedback messages continued to appear in the terminal via standard error. Viewing the contents of myflag with cat revealed the flag.

```bash
hacker@piping~redirecting-more-output:~$ /challenge/run > myflag
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge will check that output is redirected to a specific file path : myflag
[INFO] - the challenge will output a reward file if all the tests pass : /flag

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /flag file.

[TEST] You should have redirected my stdout to a file called myflag. Checking...

[PASS] The file at the other end of my stdout looks okay!
[PASS] Success! You have satisfied all execution requirements.
hacker@piping~redirecting-more-output:~$ cat myflag

[FLAG] Here is your flag:
[FLAG] pwn.college{wQ69KzIgbLiIGGjvelyBd1RPlv8.QX1YTN0wiNyUDN0EzW}
```

### New Learnings
Learned the distinction between standard output (stdout) and standard error (stderr), and how redirecting stdout does not affect messages sent to stderr. This reinforced how Unix programs can separate data output from status messages, enabling precise control over redirection and piping behavior.