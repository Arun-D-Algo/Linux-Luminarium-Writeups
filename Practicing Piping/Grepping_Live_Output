# Linux Luminarium
# Module 6: Practicing Piping

## Grepping Live Output
It turns out that you can "cut out the middleman" and avoid the need to store results to a file, like you did in the last level. You can do this by using the | (pipe) operator. Standard output from the command to the left of the pipe will be connected to (piped into) the standard input of the command to the right of the pipe. For example:

hacker@dojo:~$ echo no-no | grep yes
hacker@dojo:~$ echo yes-yes | grep yes
yes-yes
hacker@dojo:~$ echo yes-yes | grep no
hacker@dojo:~$ echo no-no | grep no
no-no
Now try it for yourself! /challenge/run will output a hundred thousand lines of text, including the flag. grep for the flag!

### Solve
**Flag:** `pwn.college{YUuzRWyAibwjhhuk7ltNz3ILHpt.QX5EDO0wiNyUDN0EzW}`

This challenge was solved by piping live output directly into grep instead of writing it to a file first. Using /challenge/run | grep "pwn.college" connected the standard output of /challenge/run directly to the standard input of grep, allowing the flag to be filtered from a very large stream of text in real time. Once the correct process was detected at the other end of the pipe, the challenge returned the flag.

```bash
hacker@piping~grepping-live-output:~$ /challenge/run | grep "pwn.college"
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge checks for a specific process at the other end of stdout : grep
[INFO] - the challenge will output a reward file if all the tests pass : /challenge/.data.txt

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /challenge/.data.txt file.

[TEST] You should have redirected my stdout to another process. Checking...
[TEST] Performing checks on that process!

[INFO] The process' executable is /nix/store/737jwbhw8ji13x9s88z3wpp8pxaqla92-gnugrep-3.12/bin/grep.
[INFO] This might be different than expected because of symbolic links (for example, from /usr/bin/python to /usr/bin/python3 to /usr/bin/python3.8).
[INFO] To pass the checks, the executable must be grep.

[PASS] You have passed the checks on the process on the other end of my stdout!
[PASS] Success! You have satisfied all execution requirements.
pwn.college{YUuzRWyAibwjhhuk7ltNz3ILHpt.QX5EDO0wiNyUDN0EzW}
```

### New Learnings
Learned how the pipe operator (|) connects commands by streaming stdout from one process into stdin of another, eliminating the need for intermediate files. This reinforced the Unix philosophy of composing small tools together to efficiently process large amounts of data.