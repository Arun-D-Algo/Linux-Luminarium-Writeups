# Linux Luminarium
# Module 7: Shell Variables

## Printing Exported Variables
There are multiple ways to access variables in bash. echo was just one of them, and we'll now learn at least one more in this challenge.

Try the env command: it'll print out every exported variable set in your shell, and you can look through that output to find the FLAG variable!


### Solve
**Flag:** `pwn.college{EG19ew6CaGcm7_lWynEZ_ZTMZBg.QX4UTN0wiNyUDN0EzW}`

This challenge was solved by using the env command to list all exported environment variables in the current shell session. Since the flag was stored in an exported variable named FLAG, running "env | grep FLAG" allowed the output of env to be piped into grep, which filtered the large list of environment variables down to the single line containing the flag. This avoided manually scanning through dozens of unrelated variables and demonstrated efficient use of pipes for targeted searching.

```bash
hacker@variables~printing-exported-variables:~$ env | grep FLAG
FLAG=pwn.college{EG19ew6CaGcm7_lWynEZ_ZTMZBg.QX4UTN0wiNyUDN0EzW}
```

### New Learnings
Learned that env displays only exported variables — not all shell variables. This reinforced the distinction between local shell variables (which exist only inside the current shell process) and environment variables (which are exported and inherited by child processes). It also strengthened understanding of how piping (|) and filtering (grep) can be combined to efficiently extract specific data from large outputs, which is a core Unix workflow principle.