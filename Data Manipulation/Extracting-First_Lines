# Linux Luminarium
# Module 8: Data Manipulation

## Extracting the First Lines with Head
In your Linux journey, you'll experience situations where you need to grab just the early output of very verbose programs. For this, you'll reach for head! The head command is used to display the first few lines of its input:

hacker@dojo:~$ cat /something/very/long | head
this
is
just
the
first
ten
lines
of
the
file
hacker@dojo:~$
By default, it shows the first 10 lines, but you can control this with the -n option:

hacker@dojo:~$ cat /something/very/long | head -n 2
this
is
hacker@dojo:~$
This challenge's /challenge/pwn outputs a bunch of data, and you'll need to pipe it through head to grab just the first 7 lines and then pipe them onwards to /challenge/college, which will give you the flag if you do this right! Your solution will be a long composite command with two pipes connecting three commands. Good luck!


### Solve
**Flag:** `pwn.college{ch-we5cUDgP0LkuNS7YWtMT8BdS.0lNxEzNxwiNyUDN0EzW}`

This challenge centered on controlling how much data flows through a pipeline. The /challenge/pwn program produced a large amount of output, but only the first seven lines were meaningful for the next stage. By piping its output into head -n 7, only the first seven lines were allowed to continue forward in the stream. That trimmed output was then piped directly into /challenge/college, which validated the received data and produced the flag. The solution demonstrated how multiple commands can be chained together so that each stage refines or filters the data before passing it along.

```bash
hacker@data~extracting-the-first-lines-with-head:~$ /challenge/pwn | head -n 7 | /challenge/college
Congratulations, you piped the right codes!
pwn.college{ch-we5cUDgP0LkuNS7YWtMT8BdS.0lNxEzNxwiNyUDN0EzW}
```

### New Learnings
Learned how head limits output to a specific number of lines using the -n option, making it useful for handling very verbose programs. Reinforced the idea that pipelines process data step-by-step, where each command transforms or restricts the stream before handing it off. Also strengthened understanding of how combining multiple pipes allows precise control over both the amount and flow of data between programs.