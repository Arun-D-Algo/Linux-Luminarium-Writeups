# Linux Luminarium
# Module 12: Chaining Commands

## Scripting with Arguments
You've learned how to make shell scripts, but so far they've just been lists of commands. Scripts become much more powerful when they can accept arguments! This might look like:

```
hacker@dojo:~$ bash myscript.sh hello world
```
The script can access these arguments using special variables:

$1 contains the first argument ("hello")
$2 contains the second argument ("world")
$3 would contain the third argument (if there had been one)
...and so on
Here's a simple example:

```
hacker@dojo:~$ cat myscript.sh
#!/bin/bash
echo "First argument: $1"
echo "Second argument: $2"
hacker@dojo:~$ bash myscript.sh hello world
First argument: hello
Second argument: world
hacker@dojo:~$
```
For this challenge, you need to write a script at /home/hacker/solve.sh that:

Takes two arguments
Outputs them in REVERSE order (second argument first, then the first argument)
For example:

```
hacker@dojo:~$ bash /home/hacker/solve.sh pwn college
college pwn
hacker@dojo:~$
```
Once your script works correctly, run /challenge/run to get your flag!

### Solve
**Flag:** `pwn.college{A_zZn5LANkIOKB0NS5_BeJaziZ0.0VNzMDOxwiNyUDN0EzW}`

This challenge required creating a shell script at /home/hacker/solve.sh that accepted two command-line arguments and printed them in reverse order. A Bash script was created with a shebang (#!/bin/bash) followed by the command echo $2 $1, which outputs the second argument first and the first argument second. The script was then tested using bash /home/hacker/solve.sh pwn college, which correctly produced college pwn. After confirming the script behaved as expected, /challenge/run was executed, which validated the script and revealed the flag.

```bash
hacker@chaining~scripting-with-arguments:~$ echo '#!/bin/bash' > /home/hacker/solve.sh
hacker@chaining~scripting-with-arguments:~$ echo 'echo $2 $1' >> /home/hacker/solve.sh
hacker@chaining~scripting-with-arguments:~$ bash /home/hacker/solve.sh pwn college
college pwn
hacker@chaining~scripting-with-arguments:~$ /challenge/run
Correct! Your script properly reversed the arguments.
Here's your flag:
pwn.college{A_zZn5LANkIOKB0NS5_BeJaziZ0.0VNzMDOxwiNyUDN0EzW}
```

### New Learnings
Learned how shell scripts can accept command-line arguments using special positional parameters such as $1, $2, $3, and so on. Reinforced that arguments supplied when executing a script are automatically assigned to these variables by Bash. Also gained experience manipulating argument order within a script by referencing positional parameters in any sequence rather than being restricted to the order they were provided