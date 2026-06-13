# Linux Luminarium
# Module 12: Chaining Commands

## Scripting with Default Cases
Your if statements so far have handled specific cases, but what about everything else? That's where else comes in!

The else clause executes when the if condition is false:

```
if [ "$1" == "hello" ]
then
    echo "Hi there!"
else
    echo "I don't understand"
fi
```
Note that the else doesn't have a condition --- it catches everything that didn't match previously. It also doesn't have a then statement. Finally, the fi goes after the else block to denote the end of the whole complex statement! It is also optional: you didn't have it in the previous level, and you only need it if the logic you're trying to achieve demands it.

Here's a practical example:

```
if [ "$1" == "start" ]
then
    echo "Starting the service..."
else
    echo "Unknown command. Use 'start' to begin."
fi
```
For this challenge, write a script at /home/hacker/solve.sh that:

Takes one argument
If the argument is "pwn", output "college"
For any other input, output "nope"
Example:

```
hacker@dojo:~$ bash /home/hacker/solve.sh pwn
college
hacker@dojo:~$ bash /home/hacker/solve.sh hack
nope
hacker@dojo:~$ bash /home/hacker/solve.sh anything
nope
hacker@dojo:~$
```
Once your script works correctly, run /challenge/run to get your flag!

### Solve
**Flag:** `pwn.college{8r1Tgl9dxDV4lkUdUqTpSH3D6Ic.01NzMDOxwiNyUDN0EzW}`

This challenge required creating a Bash script that accepted a single argument and handled two possible outcomes. If the first argument ($1) was equal to pwn, the script had to output college; otherwise, it had to output nope. A script was created with a shebang and an if/else conditional. The condition checked whether $1 matched pwn, and if it did, echo college was executed. The else block acted as the default case and executed echo nope for every other input. After saving the script to /home/hacker/solve.sh, /challenge/run verified the behavior using multiple test inputs and awarded the flag once all cases were handled correctly.

```bash
hacker@chaining~scripting-with-default-cases:~$ echo '#!/bin/bash' > /home/hacker/solve.sh
hacker@chaining~scripting-with-default-cases:~$ echo 'if [ "$1" = "pwn" ]; then echo college; else echo nope; fi' >> /home/hacker/solve.sh
hacker@chaining~scripting-with-default-cases:~$ /challenge/run
Correct! Your script properly handles the if/else conditions.
Here's your flag:
pwn.college{8r1Tgl9dxDV4lkUdUqTpSH3D6Ic.01NzMDOxwiNyUDN0EzW}
```

### New Learnings
Learned how the else clause provides a default action when an if condition evaluates to false. Reinforced the structure of Bash conditional blocks using if, then, else, and fi, and gained experience handling both matching and non-matching inputs within a script. Also strengthened understanding of positional parameters and how scripts can produce different outputs based on user-provided arguments.
