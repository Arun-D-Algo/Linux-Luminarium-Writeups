# Linux Luminarium
# Module 7: Shell Variables

## Reading Input
We'll start with reading input from the user (you). That's done using the aptly named read builtin, which reads input into a variable!

Here is an example using the -p argument, which lets you specify a prompt (otherwise, it would be hard for you, reading this now, to separate input from output in the example below):

hacker@dojo:~$ read -p "INPUT: " MY_VARIABLE
INPUT: Hello!
hacker@dojo:~$ echo "You entered: $MY_VARIABLE"
You entered: Hello!
Keep in mind, read reads data from your standard input! The first Hello!, above, was inputted rather than outputted. Let's try to be more explicit with that. Here, we annotated the beginning of each line with whether the line represents INPUT from the user or OUTPUT to the user:

 INPUT: hacker@dojo:~$ echo $MY_VARIABLE
OUTPUT:
 INPUT: hacker@dojo:~$ read MY_VARIABLE
 INPUT: Hello!
 INPUT: hacker@dojo:~$ echo "You entered: $MY_VARIABLE"
OUTPUT: You entered: Hello!
In this challenge, your job is to use read to set the PWN variable to the value COLLEGE. Good luck!


### Solve
**Flag:** `pwn.college{EHCcgw1ov6yO3zFvOZ80OU92D_9.QX4cTN0wiNyUDN0EzW}`

This challenge focused on taking user input and storing it inside a shell variable using the read builtin. Instead of assigning a value with =, the shell waits for input from standard input (the keyboard) and stores whatever is typed into the specified variable. By running read PWN and typing COLLEGE, the value was captured into the PWN variable. The challenge program then checked that the variable contained the correct value and returned the flag.

```bash
hacker@variables~reading-input:~$ read PWN
COLLEGE
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{EHCcgw1ov6yO3zFvOZ80OU92D_9.QX4cTN0wiNyUDN0EzW}
```

### New Learnings
Learned how the read builtin collects input from standard input and assigns it directly to a variable. Reinforced the understanding that shell variables can be set not only through direct assignment (VAR=value) but also dynamically through user input, and that standard input is simply the keyboard unless redirected.