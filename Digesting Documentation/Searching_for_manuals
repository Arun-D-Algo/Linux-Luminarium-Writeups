# Linux Luminarium
# Module 4: Digesting Documentation

## Searching for Manuals
This level is tricky: it hides the manpage for the challenge by randomizing its name. Luckily, all of the manpages are gathered in a searchable database, so you'll be able to search the man page database to find the hidden challenge man page! To figure out how to search for the right manpage, read the man page manpage by doing: man man!

HINT 1: man man teaches you advanced usage of the man command itself, and you must use this knowledge to figure out how to search for the hidden manpage that will tell you how to use /challenge/challenge

HINT 2: though the manpage is randomly named, you still actually use /challenge/challenge to get the flag!

### Solve
**Flag:** `pwn.college{4NJs0N39UY7Jt7_CIKdS8LSCSbj.QX2EDO0wiNyUDN0EzW}`

This challenge required locating a randomly named man page that documented how to use the /challenge/challenge binary. Since the man page name could not be guessed, the solution began by consulting man man to learn how to search the man page database by content. Using man -K /challenge/challenge, the system searched through all installed man pages and revealed the hidden documentation. Reading this man page showed that the binary prints the flag when called with the --stdbjw option and the value 403. Executing /challenge/challenge --stdbjw 403 with the correct argument successfully returned the flag.

```bash
hacker@man~searching-for-manuals:~$ man man
hacker@man~searching-for-manuals:~$ man -K /challenge/challenge
hacker@man~searching-for-manuals:~$ /challenge/challenge --stdbjw 403
Correct usage! Your flag: pwn.college{4NJs0N39UY7Jt7_CIKdS8LSCSbj.QX2EDO0wiNyUDN0EzW}
```

### New Learnings
Learned how to search the man page database by content using man -K, rather than relying on knowing command names in advance. This reinforced the idea that Unix documentation is fully searchable and that randomized or unknown command names can still be discovered by querying documentation contents directly.