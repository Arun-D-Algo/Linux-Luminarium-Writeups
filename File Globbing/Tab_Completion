# Linux Luminarium
# Module 5: File Globbing

## Tab Completion
As tempting as it might be, using * to shorten what must be typed on the commandline can lead to mistakes. Your glob might expand to unintended files, and you might not spot it until the rm command is already running! No one is safe from this style of error.

A safer alternative when you are trying to specify a specific target is tab completion. If you hit tab in the shell, it'll try to figure out what you're going to type and automatically complete it. Auto-completion is super useful, and this challenge will explore its use in specifying files.

This challenge has copied the flag into /challenge/pwncollege, and you can freely cat that file. But you can't type the filename: we used some serious trickery to make sure that you must tab-complete it. Try it out!

hacker@dojo:~$ ls /challenge
DESCRIPTION.md  pwncollege
hacker@dojo:~$ cat /challenge/pwncollege
cat: /challenge/pwncollege: No such file or directory
hacker@dojo:~$ cat /challenge/pwn<TAB>
pwn.college{HECK YEAH}
hacker@dojo:~$
When you hit that tab key, the name will expand and you'll be able to read the file. Good luck!

### Solve
**Flag:** `pwn.college{UqxEAlTa5wX_6avkWJzc4HmuhLe.0FN0EzNxwiNyUDN0EzW}`

This challenge was solved by using tab completion instead of globbing to reference a restricted filename. Since the full filename could not be typed manually, pressing the Tab key allowed the shell to safely auto-complete /challenge/pwncollege, making it possible to cat the file and reveal the flag.

```bash
hacker@globbing~tab-completion:~$ cat /challenge/pwncollege​ 
pwn.college{UqxEAlTa5wX_6avkWJzc4HmuhLe.0FN0EzNxwiNyUDN0EzW}
```

### New Learnings
Learned that tab completion expands filenames without executing glob patterns, making it a safer and more precise alternative to * when targeting specific files. This demonstrated how the shell’s auto-completion can bypass typing restrictions while preventing accidental matches to unintended files.