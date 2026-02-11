# Linux Luminarium
# Module 7: Shell Variables

## Exporting Variables
By default, variables that you set in a shell session are local to that shell process. That is, other commands you run won't inherit them. You can experiment with this by simply invoking another shell process in your own shell, like so:

hacker@dojo:~$ VAR=1337
hacker@dojo:~$ echo "VAR is: $VAR"
VAR is: 1337
hacker@dojo:~$ sh
$ echo "VAR is: $VAR"
VAR is: 
In the output above, the $ prompt is the prompt of sh, a minimal shell implementation that is invoked as a child of the main shell process. And it does not receive the VAR variable!

This makes sense, of course. Your shell variables might have sensitive or weird data, and you don't want it leaking to other programs you run unless it explicitly should. How do you mark that it should? You export your variables. When you export your variables, they are passed into the environment variables of child processes. You'll encounter the concept of environment variables in other challenges, but you'll observe their effects here. Here is an example:

hacker@dojo:~$ VAR=1337
hacker@dojo:~$ export VAR
hacker@dojo:~$ sh
$ echo "VAR is: $VAR"
VAR is: 1337
Here, the child shell received the value of VAR and was able to print it out! You can also combine those first two lines.

hacker@dojo:~$ export VAR=1337
hacker@dojo:~$ sh
$ echo "VAR is: $VAR"
VAR is: 1337
In this challenge, you must invoke /challenge/run with the PWN variable exported and set to the value COLLEGE, and the COLLEGE variable set to the value PWN but not exported (e.g., not inherited by /challenge/run). Good luck!


### Solve
**Flag:** `pwn.college{APYOL56IXLNGNK3Zg4-VL9B8dHu.QXyYTN0wiNyUDN0EzW}`

This challenge was solved by correctly distinguishing between shell variables and exported environment variables. The variable PWN was exported and set to COLLEGE using export PWN=COLLEGE, making it available to child processes. The variable COLLEGE was then set to PWN using COLLEGE=PWN but deliberately not exported, ensuring it remained local to the current shell. When /challenge/run was executed, it verified that PWN was inherited while COLLEGE was not, and then revealed the flag.

```bash
hacker@variables~exporting-variables:~$ export PWN=COLLEGE
You've set the PWN variable to the proper value!
hacker@variables~exporting-variables:~$ COLLEGE=PWN
You've set the PWN variable to the proper value!
You've set the COLLEGE variable to the proper value!
hacker@variables~exporting-variables:~$ /challenge/run
CORRECT!
You have exported PWN=COLLEGE and set, but not exported, COLLEGE=PWN. Great 
job! Here is your flag:
pwn.college{APYOL56IXLNGNK3Zg4-VL9B8dHu.QXyYTN0wiNyUDN0EzW}
You've set the PWN variable to the proper value!
You've set the COLLEGE variable to the proper value!
```

### New Learnings
Learned the critical difference between local shell variables and exported environment variables. Exporting a variable makes it part of the process environment so that child processes inherit it, while non-exported variables remain private to the current shell. This reinforced how process inheritance works in Unix systems and how export controls variable visibility across process boundaries.