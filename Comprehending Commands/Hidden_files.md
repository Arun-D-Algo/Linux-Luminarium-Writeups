# Linux Luminarium
# Module 3: Comprehending Commands

## Hidden files
Interestingly, ls doesn't list all the files by default. Linux has a convention where files that start with a . don't show up by default in ls and in a few other contexts. To view them with ls, you need to invoke ls with the -a flag, as so:

hacker@dojo:~$ touch pwn
hacker@dojo:~$ touch .college
hacker@dojo:~$ ls
pwn
hacker@dojo:~$ ls -a
.college	pwn
hacker@dojo:~$
Now, it's your turn! Go find the flag, hidden as a dot-prepended file in /.

### Solve
**Flag:** `pwn.college{kLsxkI557pdKAbrtPOBUo8pxCUj.QXwUDO0wiNyUDN0EzW}`

This challenge hid the flag inside a dot-prefixed file located in the root directory (/). Since hidden files do not appear in standard ls output, the first step was to navigate to the root directory and use ls -a to reveal all files, including hidden ones. Among the listed entries was a file named .flag-12778221955773. Once the hidden file was identified, cat was used to read its contents and retrieve the flag successfully.

```bash
hacker@commands~hidden-files:~$ cd /
hacker@commands~hidden-files:/$ ls -a
.           .flag-12778221955773  challenge  home   media  opt   run   sys  var
..          bin                   dev        lib    mnt    proc  sbin  tmp
.dockerenv  boot                  etc        lib64  nix    root  srv   usr
hacker@commands~hidden-files:/$ cat .flag-12778221955773
pwn.college{kLsxkI557pdKAbrtPOBUo8pxCUj.QXwUDO0wiNyUDN0EzW}
```

### New Learnings
Learned that Linux treats files beginning with a dot (.) as hidden files, causing them to be excluded from normal ls output. Reinforced the use of the -a flag with ls to display all files, including hidden ones. Also gained experience identifying hidden files within a directory and accessing them normally once their names are known.

