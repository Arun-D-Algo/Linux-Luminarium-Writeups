# Linux Luminarium
# Module 6: Practicing Piping

## Grepping Errors
You know how to redirect errors to a file, and you know how to pipe output to another program, such as grep. But what if you wanted to grep through errors directly?

The > operator redirects a given file descriptor to a file, and you've used 2> to redirect fd 2, which is standard error. The | operator redirects only standard output to another program, and there is no 2| form of the operator! It can only redirect standard output (file descriptor 1).

Luckily, where there's a shell, there's a way!

The shell has a >& operator, which redirects a file descriptor to another file descriptor. This means that we can have a two-step process to grep through errors: first, we redirect standard error to standard output (2>& 1) and then pipe the now-combined stderr and stdout as normal (|)!

Try it now! Like the last level, this level will overwhelm you with output, but this time on standard error. grep through it to find the flag!


### Solve
**Flag:** `pwn.college{IFBEcDEujeMXOA6b3S5sydZ1HNF.QX1ATO0wiNyUDN0EzW}`

This challenge was solved by redirecting standard error into standard output and then piping the combined stream into grep. Using /challenge/run 2>&1 | grep "pwn.college" merged stderr with stdout, allowing grep to filter through error output in real time and extract the line containing the flag.

```bash
hacker@piping~grepping-errors:~$ /challenge/run 2>& 1 | grep "pwn.college"
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge checks for a specific process at the other end of stderr : grep
[INFO] - the challenge will output a reward file if all the tests pass : /challenge/.data.txt

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /challenge/.data.txt file.

[TEST] You should have redirected my stderr to another process. Checking...
[TEST] Performing checks on that process!

[INFO] The process' executable is /nix/store/737jwbhw8ji13x9s88z3wpp8pxaqla92-gnugrep-3.12/bin/grep.
[INFO] This might be different than expected because of symbolic links (for example, from /usr/bin/python to /usr/bin/python3 to /usr/bin/python3.8).
[INFO] To pass the checks, the executable must be grep.

[PASS] You have passed the checks on the process on the other end of my stderr!
[PASS] Success! You have satisfied all execution requirements.
pwn.college{IFBEcDEujeMXOA6b3S5sydZ1HNF.QX1ATO0wiNyUDN0EzW}
```

### New Learnings
Learned how the file descriptor redirection operator (2>&1) can be used to merge stderr into stdout, enabling tools like grep to process error output through pipes. This reinforced a deeper understanding of Unix file descriptors and how combining redirection with piping allows precise control over program output streams.