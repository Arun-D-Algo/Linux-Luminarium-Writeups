# Linux Luminarium
# Module 6: Practicing Piping

## Split Piping stderr and stdout
Now, let's put your knowledge together. You must master the ultimate piping task: redirect stdout to one program and stderr to another.

The challenge here, of course, is that the | operator links the stdout of the left command with the stdin of the right command. Of course, you've used 2>&1 to redirect stderr into stdout and, thus, pipe stderr over, but this then mixes stderr and stdout. How to keep it unmixed?

You will need to combine your knowledge of >(), 2>, and |. How to do it is a task I'll leave to you.

In this challenge, you have:

/challenge/hack: this produces data on stdout and stderr
/challenge/the: you must redirect hack's stderr to this program
/challenge/planet: you must redirect hack's stdout to this program
Go get the flag!

BONUS: For some added difficulty, find a solution that doesn't use |.

### Solve
**Flag:** `pwn.college{Mf4tXjBVjPiOfM4qnFEdGWzbUJA.QXxQDM2wiNyUDN0EzW}`

This challenge required sending the standard output of /challenge/hack to /challenge/planet while simultaneously sending its standard error to /challenge/the. A normal pipe was insufficient because it only handles stdout and would not keep the two streams separate. Using output process substitution, stdout was redirected with > >(/challenge/planet) and stderr was redirected with 2> >(/challenge/the). This allowed each stream to be delivered directly to the correct program without mixing them together. Once both programs received their expected input streams, the challenge revealed the flag.

```bash
hacker@piping~split-piping-stderr-and-stdout:~$ /challenge/hack > >(/challenge/planet) 2> >(/challenge/the)
Congratulations, you have learned a redirection technique that even experts 
struggle with! Here is your flag:
pwn.college{Mf4tXjBVjPiOfM4qnFEdGWzbUJA.QXxQDM2wiNyUDN0EzW}
```

### New Learnings
Learned how stdout and stderr can be redirected independently to different destinations instead of being merged together. Reinforced that >(command) creates a writable file-like target connected to a program's standard input. Also gained experience using file descriptor redirection (> for stdout and 2> for stderr) to route different output streams to separate programs simultaneously.