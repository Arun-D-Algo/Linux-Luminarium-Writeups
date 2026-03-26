# Linux Luminarium
# Module 12: Chaining Commands

## Chaining with Semicolons
The easiest way to chain commands is ;. In most contexts, ; separates commands in a similar way to how Enter separates lines. So, this:

hacker@dojo:~$ echo COLLEGE > pwn
hacker@dojo:~$ cat pwn
COLLEGE
hacker@dojo:~$
Is roughly the same as this:

hacker@dojo:~$ echo COLLEGE > pwn; cat pwn
COLLEGE
hacker@dojo:~$
Basically, when you hit Enter, your shell executes your typed command and, after that command terminates, gives you the prompt to input another command. The semicolon is analogous, just without the prompt and with you entering both commands before anything is executed.

Give it a try now! In this level, you must run /challenge/pwn and then /challenge/college, chaining them with a semicolon.

### Solve
**Flag:** `pwn.college{surDOHiizNFYM6VJLM6ebQawNIV.QX1UDO0wiNyUDN0EzW}`

This challenge required executing two programs consecutively: /challenge/pwn followed by /challenge/college. Instead of running them on separate lines, both commands were chained using a semicolon. The shell interpreted this as two distinct commands to be executed sequentially. Once /challenge/pwn completed, /challenge/college ran immediately after, satisfying the condition of the challenge. This chaining allowed both required programs to execute in a single input line, which resulted in the flag being displayed successfully.

```bash
hacker@chaining~chaining-with-semicolons:~$ /challenge/pwn; /challenge/college
Yes! You chained /challenge/pwn and /challenge/college! Here is your flag:
pwn.college{surDOHiizNFYM6VJLM6ebQawNIV.QX1UDO0wiNyUDN0EzW}
```

### New Learnings
Learned how semicolons (;) allow sequential execution of multiple commands in a single line, mimicking how the shell normally processes commands one after another after pressing Enter. Reinforced the idea that command chaining does not depend on the success or failure of previous commands—each command runs independently in order. Also strengthened understanding of how the shell parses and executes command lists, and how chaining improves efficiency by reducing manual input steps.
