# Linux Luminarium
# Module 6: Practicing Piping

## Grepping Stored Results
You know how to run commands, how to redirect their output (e.g., >), and how to search through the resulting file (e.g., grep). Let's put this together!

In preparation for more complex levels, we want you to:

Redirect the output of /challenge/run to /tmp/data.txt.
This will result in a hundred thousand lines of text, with one of them being the flag, in /tmp/data.txt.
grep that for the flag!

### Solve
**Flag:** `pwn.college{oYdFMGHyQW_zE_CJwzG-TdFM751.QX4EDO0wiNyUDN0EzW}`

This challenge was solved by redirecting standard output to a file and then searching that stored output using grep. The command /challenge/run > /tmp/data.txt saved all output from the challenge into a file, and running grep "pwn.college" /tmp/data.txt filtered the large dataset to extract the single line containing the flag.

```bash
hacker@piping~grepping-stored-results:~$ /challenge/run > /tmp/data.txt
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge will check that output is redirected to a specific file path : /tmp/data.txt
[INFO] - the challenge will output a reward file if all the tests pass : /challenge/.data.txt

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /challenge/.data.txt file.

[TEST] You should have redirected my stdout to a file called /tmp/data.txt. Checking...

[HINT] File descriptors are inherited from the parent, unless the FD_CLOEXEC is set by the parent on the file descriptor.
[HINT] For security reasons, some programs, such as python, do this by default in certain cases. Be careful if you are
[HINT] creating and trying to pass in FDs in python.

[PASS] The file at the other end of my stdout looks okay!
[PASS] Success! You have satisfied all execution requirements.
hacker@piping~grepping-stored-results:~$ grep "pwn.college" /tmp/data.txt
pwn.college{oYdFMGHyQW_zE_CJwzG-TdFM751.QX4EDO0wiNyUDN0EzW}
```

### New Learnings
Learned how output redirection and text searching can be combined to process large amounts of command output efficiently. This reinforced the workflow of generating data, storing it for later inspection, and using grep to quickly locate relevant information within large files.