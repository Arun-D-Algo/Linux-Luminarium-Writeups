# Linux Luminarium
# Module 7: Shell Variables

## Storing Command Output
In the course of working with the shell, you will often want to store the output of some command into a variable. Luckily, the shell makes this quite easy using something called Command Substitution! Observe:

hacker@dojo:~$ FLAG=$(cat /flag)
hacker@dojo:~$ echo "$FLAG"
pwn.college{blahblahblah}
hacker@dojo:~$
Neat! Now, you practice. Read the output of the /challenge/run command directly into a variable called PWN, and it will contain the flag!

Trivia: You can also use backticks instead of $(): FLAG=`cat /flag` instead of FLAG=$(cat /flag) in the example above. This is an older format, and has some disadvantages (for example, imagine if you wanted to nest command substitutions. How would you do $(cat $(find / -name flag)) with backticks? The official stance of pwn.college is that you should use $(blah) instead of `blah`.


### Solve
**Flag:** `pwn.college{4A0ZsUDls5CFjxV5CUGgNFBPeNb.QX1cDN1wiNyUDN0EzW}`

This challenge focused on command substitution — capturing the output of a command directly into a variable instead of printing it to the terminal. Using PWN=$(/challenge/run), the shell first executes /challenge/run, collects everything it prints to standard output, and then assigns that entire output as the value of the variable PWN. When the variable is later expanded with $PWN, the stored flag is displayed. The key idea is that the command runs first, and its output replaces the $() expression before the assignment happens.

```bash
hacker@variables~storing-command-output:~$ PWN=$(/challenge/run)
Congratulations! You have read the flag into the PWN variable. Now print it out 
and submit it!
hacker@variables~storing-command-output:~$ echo $PWN
pwn.college{4A0ZsUDls5CFjxV5CUGgNFBPeNb.QX1cDN1wiNyUDN0EzW}
```

### New Learnings
Learned how command substitution works using the $() syntax and how it differs from normal variable expansion. $VAR expands an existing variable, while $(command) executes a command and substitutes its output in place. Also reinforced why $() is preferred over older backtick syntax, especially for clarity and nested commands.