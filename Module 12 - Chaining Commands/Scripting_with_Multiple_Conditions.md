# Linux Luminarium
# Module 12: Chaining Commands

## Scripting with Mutliple Conditions
You've learned how to use a single if statement to check a condition. But what if you need to check multiple conditions? You can use elif (short for else if):

```
if [ "$1" == "one" ]
then
    echo "1"
elif [ "$1" == "two" ]
then
    echo "2"
elif [ "$1" == "three" ]
then
    echo "3"
else
    echo "unknown"
fi
```
Note that you do need a then after the elif, just like the if. As before the else at the end catches everything that didn't match.

For this challenge, write a script at /home/hacker/solve.sh that:

Takes one argument
If the argument is "hack", output "the planet"
If the argument is "pwn", output "college"
If the argument is "learn", output "linux"
For any other input, output "unknown"
Example:

```
hacker@dojo:~$ bash /home/hacker/solve.sh hack
the planet
hacker@dojo:~$ bash /home/hacker/solve.sh pwn
college
hacker@dojo:~$ bash /home/hacker/solve.sh learn
linux
hacker@dojo:~$ bash /home/hacker/solve.sh foo
unknown
hacker@dojo:~$
```
Once your script works correctly, run /challenge/run to get your flag!

NOTE: As you're creating your script, make sure to follow the spacing closely in the examples. Unlike many other languages, bash requires the [ and the ] to be separated from other characters by spaces, otherwise it cannot parse the condition.

### Solve
**Flag:** `pwn.college{Y15asLBKZ7mYSZqmU5WNoAe9YJU.0FOzMDOxwiNyUDN0EzW}`

This challenge required creating a Bash script that accepted a single argument and responded differently depending on its value. The script used a chain of conditional statements to check whether the first argument ($1) matched hack, pwn, or learn. If the argument was hack, the script printed the planet; if it was pwn, it printed college; and if it was learn, it printed linux. Any input that did not match these conditions was handled by the else block, which printed unknown. The logic was implemented using an if statement followed by multiple elif branches and a final else clause. After creating the script and saving it to /home/hacker/solve.sh, /challenge/run tested the script against several inputs and confirmed that all conditions were handled correctly, revealing the flag.

```bash
hacker@chaining~scripting-with-multiple-conditions:~$ echo '#!/bin/bash' > /home/hacker/solve.sh
hacker@chaining~scripting-with-multiple-conditions:~$ echo 'if [ "$1" = "hack" ]; then echo "the planet"; elif [ "$1" = "pwn" ]; then echo college; elif [ "$1" = "learn" ]; then echo linux; else echo unknown; fi' >> /home/hacker/solve.sh
hacker@chaining~scripting-with-multiple-conditions:~$ /challenge/run
Correct! Your script properly handles all the conditions with elif.
Here's your flag:
pwn.college{Y15asLBKZ7mYSZqmU5WNoAe9YJU.0FOzMDOxwiNyUDN0EzW}
```

### New Learnings
Learned how to use elif to handle multiple conditional branches within a Bash script. Reinforced the structure of multi-way decision making using if, elif, else, and fi, where conditions are evaluated sequentially until a match is found. Also gained experience building scripts that map different input values to different outputs while providing a default fallback case for unexpected input.
