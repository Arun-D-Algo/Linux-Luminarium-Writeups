# Linux Luminarium
# Module 3: Comprehending Commands

## More catting practice
You can specify all sorts of paths as arguments to commands, and we'll practice some more with cat. In this level, I'll put the flag in some crazy directory, and I will not allow you to change directories with cd, so no cat flag for you. You must retrieve the flag by absolute path, wherever it is.

### Solve
**Flag:** `pwn.college{4sVKJ0h90xU6_7vPxYtqchxc386.QXwITO0wiNyUDN0EzW}`

This challenge disabled the use of the cd command, preventing navigation into the directory containing the flag. However, the challenge explicitly revealed the flag's location as /usr/share/flag. Since absolute paths work independently of the current directory, the solution was simply to provide the full path to cat. By running cat /usr/share/flag, the shell directly accessed the file from its exact filesystem location and displayed the flag without requiring any directory changes.

```bash
You cannot use the 'cd' command in this level, and must retrieve the flag by 
absolute path. Plus, I hid the flag in a different directory! You can find it 
in the file /usr/share/flag. Go cat it out **without** cding into that 
directory!
hacker@commands~more-catting-practice:~$ cat /usr/share/flag
pwn.college{4sVKJ0h90xU6_7vPxYtqchxc386.QXwITO0wiNyUDN0EzW}
```

### New Learnings
Learned how absolute paths allow files to be accessed from anywhere in the filesystem without needing to change the current working directory. Reinforced the difference between absolute and relative paths, and understood that commands like cat can directly access files using their full location. Also gained more practice navigating the Linux filesystem conceptually by identifying and using paths that start from the root directory (/).
