# Linux Luminarium
# Module 7: Shell Variables

## Mutli-Word Variables
In this level, you will learn about quoting. Spaces have special significance in the shell, and there are places where you can't use them spuriously. Recall our variable setting:

hacker@dojo:~$ VAR=1337
That sets the VAR variable to 1337, but what if you wanted to set it to 1337 SAUCE? You might try the following:

hacker@dojo:~$ VAR=1337 SAUCE
This looks reasonable, but it does not work, for similar reasons to needing to have no spaces around the =. When the shell sees a space, it ends the variable assignment and interprets the next word (SAUCE in this case) as a command. To set VAR to 1337 SAUCE, you need to quote it:

hacker@dojo:~$ VAR="1337 SAUCE"
Here, the shell reads 1337 SAUCE as a single token, and happily sets that value to VAR. In this level, you'll need to set the variable PWN to COLLEGE YEAH. Good luck!


### Solve
**Flag:** `pwn.college{QKw__g9ygtzc6Hj0pTn3WgJqvQ2.QXwYTN0wiNyUDN0EzW}`

This challenge was solved by assigning a multi-word value to a shell variable using quotes. Since spaces terminate tokens in the shell, the value COLLEGE YEAH had to be wrapped in quotes when assigning it to PWN. Using PWN="COLLEGE YEAH" ensured the shell treated the entire phrase as a single value, allowing the challenge to validate it and return the flag.

```bash
hacker@variables~multi-word-variables:~$ PWN="COLLEGE YEAH"
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{QKw__g9ygtzc6Hj0pTn3WgJqvQ2.QXwYTN0wiNyUDN0EzW}
```

### New Learnings
Learned how quoting preserves spaces in shell variable assignments, allowing multi-word strings to be stored as a single value. This reinforced how the shell tokenizes input based on spaces and how quotes control that behavior.