# Linux Luminarium
# Module 4: Digesting Documentation

## Searching Manuals
You can scroll man pages with the arrow keys (and PgUp/PgDn) and search with /. After searching, you can hit n to go to the next result and N to go to the previous result. Instead of /, you can use ? to search backwards!

Find the option that will give you the flag by reading the challenge man page.

### Solve
**Flag:** `pwn.college{M-H-mQ5Wdm9j7KD5udER8j4ssSl.QX1EDO0wiNyUDN0EzW}`

To solve this, the manual page for /challenge/challenge was opened with man challenge.
Inside the manpage, the search function was triggered using /flag, which highlighted every option in the documentation referencing the flag.
Scrolling through matches with n eventually revealed the correct option that prints the flag.
Running /challenge/challenge with that option returned the flag.

```bash
hacker@man~searching-manuals:~$ man challenge
hacker@man~searching-manuals:~$ 
hacker@man~searching-manuals:~$ /challenge/challenge --vrmknbq
Initializing...
Correct usage! Your flag: pwn.college{M-H-mQ5Wdm9j7KD5udER8j4ssSl.QX1EDO0wiNyUDN0EzW}
```

### New Learnings
Broke down how manual page search works and how / and n streamline looking for relevant information inside long documentation. Understood how hidden command options can be revealed through manpage navigation instead of guesswork.