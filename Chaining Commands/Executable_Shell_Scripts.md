# Linux Luminarium
# Module 12: Chaining Commands

## Executable Shell Scripts
You have written your first shell script, but calling it via bash script.sh is a pain. Why do you need that bash?

When you invoke bash script.sh, you are, of course launching the bash command with the script.sh argument. This tells bash to read its commands from script.sh instead of standard input, and thus your shell script is executed.

It turns out that you can avoid the need to manually invoke bash. If your shell script file is executable (recall File Permissions), you can simply invoke it via its relative or absolute path! For example, if you create script.sh in your home directory and make it executable, you can invoke it via /home/hacker/script.sh or ~/script.sh or (if your working directory is /home/hacker) ./script.sh.

Try that here! Make a shellscript that will invoke /challenge/solve, make it executable, and run it without explicitly invoking bash!

### Solve
**Flag:** `pwn.college{A1YI_OvZw8NiNnDS9FUlrQ_SoPf.QX0cjM1wiNyUDN0EzW}`

This challenge required creating a shell script that executed /challenge/solve and then running that script without invoking bash manually. First, a script named x.sh was created containing the command /challenge/solve. By default, the file only had read and write permissions, so attempting to execute it directly would fail. The chmod +x x.sh command was then used to add execute permissions to the file. Once executable, the script could be launched using its relative path ./x.sh, causing the shell to execute the commands inside the script automatically. This satisfied the challenge requirements and revealed the flag.

```bash
hacker@chaining~executable-shell-scripts:~$ echo /challenge/solve > x.sh
hacker@chaining~executable-shell-scripts:~$ ls -l x.sh
-rw-r--r-- 1 hacker hacker 17 Jun  5 06:26 x.sh
hacker@chaining~executable-shell-scripts:~$ chmod +x x.sh
hacker@chaining~executable-shell-scripts:~$ ./x.sh
Congratulations on your shell script execution! Your flag:
pwn.college{A1YI_OvZw8NiNnDS9FUlrQ_SoPf.QX0cjM1wiNyUDN0EzW}
```

### New Learnings
Learned that shell scripts can be executed directly like normal programs when they have execute permissions. Reinforced the role of file permissions in controlling whether a file can be run as a command. Also gained experience using chmod +x to make a script executable and invoking it through a relative path such as ./x.sh instead of explicitly launching it with bash.
