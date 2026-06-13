# Linux Luminarium
# Module 7: Shell Variables

## Setting Variables
Naturally, as well as reading values stored in variables, you can write values to variables. This is done, as with many other languages, using =. To set variable VAR to value 1337, you would use:

hacker@dojo:~$ VAR=1337
Note that there are no spaces around the =! If you put spaces (e.g., VAR = 1337), the shell won't recognize a variable assignment and will, instead, try to run the VAR command (which does not exist).

Also note that this uses VAR and not $VAR: the $ is only prepended to access variables. In shell terms, this prepending of $ triggers what is called variable expansion, and is, surprisingly, the source of many potential vulnerabilities (if you're interested in that, check out the Art of the Shell dojo when you get comfortable with the command line!).

After setting variables, you can access them using the techniques you've learned previously, such as:

hacker@dojo:~$ echo $VAR
1337
To solve this level, you must set the PWN variable to the value COLLEGE. Be careful: both the names and values of variables are case-sensitive! PWN is not the same as pwn and COLLEGE is not the same as College.


### Solve
**Flag:** `pwn.college{g1NukbBmnF_Y-bPC8iYSzP9ozFx.QX5UTN0wiNyUDN0EzW}`

This challenge was solved by assigning a value to a shell variable using the correct assignment syntax. The variable PWN was set to COLLEGE using PWN=COLLEGE, with no spaces around the = operator. Once the variable was correctly assigned with the proper case sensitivity, the challenge validated the assignment and revealed the flag.

```bash
hacker@variables~setting-variables:~$ PWN=COLLEGE
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{g1NukbBmnF_Y-bPC8iYSzP9ozFx.QX5UTN0wiNyUDN0EzW}
```

### New Learnings
Learned how shell variable assignment works using the VAR=value syntax, and why spacing rules are strict in shell scripting. This reinforced the difference between assigning a variable (VAR=value) and expanding a variable ($VAR), as well as the importance of case sensitivity in Unix environments.