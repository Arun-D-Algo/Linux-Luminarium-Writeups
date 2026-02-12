# Linux Luminarium
# Module 7: Shell Variables

## Reading Files
Often, when shell users want to read a file into an environment variable, they do something like:

hacker@dojo:~$ echo "test" > some_file
hacker@dojo:~$ VAR=$(cat some_file)
hacker@dojo:~$ echo $VAR
test
This works, but it represents what grouchy hackers call a "Useless Use of Cat". That is, running a whole other program just to read the file is a waste. It turns out that you can just use the powers of the shell!

Previously, you read user input into a variable. You've also previously redirected files into command input! Put them together, and you can read files with the shell.

hacker@dojo:~$ echo "test" > some_file
hacker@dojo:~$ read VAR < some_file
hacker@dojo:~$ echo $VAR
test
What happened there? The example redirects some_file into the standard input of read, and so when read reads into VAR, it reads from the file! Now, use that to read /challenge/read_me into the PWN environment variable, and we'll give you the flag! The /challenge/read_me will keep changing, so you'll need to read it right into the PWN variable with one command!


### Solve
**Flag:** `pwn.college{0LcsGuQlkQ0wpL-S6Tu53r3T57e.QXwIDO0wiNyUDN0EzW}`

This challenge demonstrated how to read the contents of a file directly into a shell variable using input redirection instead of command substitution. By running read PWN < /challenge/read_me, the shell redirected the file into the standard input of read, causing the contents of /challenge/read_me to be stored directly in the variable PWN. The challenge then verified that PWN contained the correct value and revealed the flag.

```bash
hacker@variables~reading-files:~$ read PWN < /challenge/read_me
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{0LcsGuQlkQ0wpL-S6Tu53r3T57e.QXwIDO0wiNyUDN0EzW}
```

### New Learnings
Learned how input redirection (<) can be combined with the read builtin to load file contents into a variable without using external commands like cat. This reinforced how the shell itself can handle file input efficiently and how standard input can be redirected from sources other than the keyboard.