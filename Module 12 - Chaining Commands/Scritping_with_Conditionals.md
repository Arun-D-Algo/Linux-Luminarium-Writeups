# Linux Luminarium
# Module 12: Chaining Commands

## Scripting with Conditionals
Now that you can use arguments in scripts, let's make them smarter with conditional logic!

In bash, you can use if statements to make decisions:

```
if [ "$1" == "ping" ]
then
    echo "pong"
fi
```
The above, in English, is if the first argument is "ping", print out "pong". The syntax is somewhat unforgiving for a few reasons. First, you must have spaces after if (if you're used to a language like C, this is different), after [, and before ]. Second, if, then, and fi must all be on different lines (or separated by semicolons); you can't lump them into the same statement. It's also a bit weird: instead of endif or end or something like that, the terminator of the if statement is fi (if backwards). Just something you have to remember.

For this challenge, write a script at /home/hacker/solve.sh that:

Takes one argument
If the argument is "pwn", output "college"
For any other input, output nothing
Example:

```
hacker@dojo:~$ bash /home/hacker/solve.sh pwn
college
hacker@dojo:~$ bash /home/hacker/solve.sh foo
hacker@dojo:~$
```
Once your script works correctly, run /challenge/run to get your flag!

NOTE: Interested in what else you can check in a condition, other than string equality? Read all about it with help test!

### Solve
**Flag:** `pwn.college{sBYcuSYxMbYAuOCe1A7LPTWhpu_.0lNzMDOxwiNyUDN0EzW}`

This challenge required creating a script that accepted a single argument and printed college only when the argument was pwn. A Bash script was created with a shebang followed by an if statement that compared the first positional parameter ($1) against the string pwn. If the condition evaluated to true, the script executed echo college; otherwise, it produced no output. The condition was implemented using Bash's test syntax: if [ "$1" = "pwn" ]; then echo college; fi. After creating the script, /challenge/run was executed, which tested the script with multiple inputs and confirmed that it handled the condition correctly, revealing the flag.

```bash
hacker@chaining~scripting-with-conditionals:~$ echo '#!/bin/bash' > /home/hacker/solve.sh
hacker@chaining~scripting-with-conditionals:~$ echo 'if [ "$1" = "pwn" ]; then echo college; fi' >> /home/hacker/solve.sh
hacker@chaining~scripting-with-conditionals:~$ /challenge/run
Correct! Your script properly handles all the conditions.
Here's your flag:
pwn.college{sBYcuSYxMbYAuOCe1A7LPTWhpu_.0lNzMDOxwiNyUDN0EzW}
```

### New Learnings
Learned how to use conditional statements in Bash scripts with the if, then, and fi keywords. Reinforced the importance of Bash syntax rules, particularly the required spaces around [ and ] in test conditions. Also gained experience using positional parameters inside conditions, allowing script behavior to change based on the values passed as command-line arguments.
