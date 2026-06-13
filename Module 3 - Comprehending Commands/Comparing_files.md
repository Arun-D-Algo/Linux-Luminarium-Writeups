# Linux Luminarium
# Module 3: Comprehending Commands

## Comparing files
When looking for changes between similar files, eyeballing them might not be the most efficient approach! This is where the diff command becomes invaluable.

diff compares two files line by line and shows you exactly what's different between them. For example:

hacker@dojo:~$ cat file1
hello
world
hacker@dojo:~$ cat file2
hello
universe
hacker@dojo:~$ diff file1 file2
2c2
< world
---
> universe
The output tells us that line 2 changed (2c2), with world in the first file (<) being replaced by universe in the second file (>).

Sometimes, when new lines are added, you'll see something like:

hacker@dojo:~$ cat old
pwn
hacker@dojo:~$ cat new
pwn
college
hacker@dojo:~$ diff old new
1a2
> college
This tells us that after line 1 in the first file, the second file has an additional line (1a2 means "after line 1 of file1, add line 2 of file2").

Now for your challenge! There are two files in /challenge:

/challenge/decoys_only.txt contains 100 fake flags
/challenge/decoys_and_real.txt contains all 100 fake flags plus the one real flag
Use diff to find what's different between these files and get your flag!

### Solve
**Flag:** `pwn.college{wP9f2y58gS7yI8t5k5EeB5ZoRoV.01MwMDOxwiNyUDN0EzW}`

Used the diff command with the two given paths to find the added flag in the second file path.

```bash
hacker@commands~comparing-files:~$ diff /challenge/decoys_only.txt /challenge/decoys_and_real.txt
12a13
> pwn.college{wP9f2y58gS7yI8t5k5EeB5ZoRoV.01MwMDOxwiNyUDN0EzW}

```

### New Learnings
Learnt how to use the diff command.