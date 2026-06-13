# Linux Luminarium
# Module 7: Shell Variables

## Printing Variables
Let's start with printing variables out. The /challenge/run program will not, and cannot, give you the flag, but that's okay, because the flag has been put into the variable called "FLAG"! Just have your shell print it out!

You can accomplish this using a number of ways, but we'll start with echo. This command just prints stuff. For example:

hacker@dojo:~$ echo Hello Hackers!
Hello Hackers!
You can also print out variables with echo, by prepending the variable name with a $. For example, there is a variable, PWD, that always holds the current working directory of the current shell. You print it out as so:

hacker@dojo:~$ echo $PWD
/home/hacker
Now it's your turn. Have your shell print out the FLAG variable and solve this challenge!


### Solve
**Flag:** `pwn.college{QfVQkLLwA9iRviHs_y8vryEcIiT.QX3UTN0wiNyUDN0EzW}`

This challenge was solved by printing the value of a shell variable using echo. The flag was already stored in an environment variable named FLAG, and by running echo $FLAG, the shell expanded the variable and displayed its value directly in the terminal.

```bash
hacker@variables~printing-variables:~$ echo $FLAG
pwn.college{QfVQkLLwA9iRviHs_y8vryEcIiT.QX3UTN0wiNyUDN0EzW}
```

### New Learnings
Learned how shell variable expansion works using the $ prefix, and how environment variables can store important data accessible within the shell session. This reinforced that commands like echo print expanded values after the shell performs variable substitution.