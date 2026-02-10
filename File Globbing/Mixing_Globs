# Linux Luminarium
# Module 5: File Globbing

## Mixing Globs
Now, let's put the previous levels together! We put a few happy, but diversely-named files in /challenge/files. Go cd there and, using the globbing you've learned, write a single, short (6 characters or less) glob that (when passed as an argument to /challenge/run) will match only the files "challenging", "educational", and "pwning"!

HINT: Make sure to look at the names of the files in /challenge/files. Do you see any patterns that could help you make your glob?

### Solve
**Flag:** `pwn.college{0FHCYz0vyB2mOYaLvdbv4SaoYaC.QX1IDO0wiNyUDN0EzW}`

This challenge was solved by combining bracket globbing with * to match filenames based on their starting letter. The glob [ecp]* expanded to exactly challenging, educational, and pwning, and passing this single short glob to /challenge/run successfully returned the flag.

```bash
hacker@globbing~mixing-globs:~$ cd /challenge/files
hacker@globbing~mixing-globs:/challenge/files$ /challenge/run [ecp]*
You got it! Here is your flag!
pwn.college{0FHCYz0vyB2mOYaLvdbv4SaoYaC.QX1IDO0wiNyUDN0EzW}
```

### New Learnings
Learned that bracket expressions can be combined with * to form compact yet powerful globs, allowing multiple filename patterns to be matched using a single argument. This reinforced how thoughtful analysis of filename prefixes can simplify complex matching constraints while staying within strict character limits.
