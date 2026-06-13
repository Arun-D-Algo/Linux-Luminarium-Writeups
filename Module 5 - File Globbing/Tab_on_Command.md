# Linux Luminarium
# Module 5: File Globbing

## Tab Completion on Command
Tab completion is for more than files! You can also tab-complete commands. This level has a command that starts with pwncollege, and it'll give you the flag. Type pwncollege and hit the tab key to auto-complete it!

NOTE: You can auto-complete any command, but be careful: callous auto-completes without double-checking the result can wreak havoc in your shell if you accidentally run the wrong commands!

### Solve
**Flag:** `pwn.college{wHG7TadfhXIjAoZZ6AGBn0Ox-33.0VN0EzNxwiNyUDN0EzW}`

This challenge was solved by using tab completion on commands rather than filenames. Typing pwncollege and pressing Tab allowed the shell to auto-complete the full command name, which was then executed to print the flag.

```bash
hacker@globbing~tab-completion-on-commands:~$ pwncollege-7231 
Correct! Here is your flag:
pwn.college{wHG7TadfhXIjAoZZ6AGBn0Ox-33.0VN0EzNxwiNyUDN0EzW}
```

### New Learnings
Learned that tab completion works for commands as well as files, enabling safe and accurate execution without needing to know or type the full command name. This reinforced how shell auto-completion reduces errors while bypassing manual typing restrictions.