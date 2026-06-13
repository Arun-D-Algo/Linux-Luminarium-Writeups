# Linux Luminarium
# Module 13: Terminal Multiplexing

## Launching Screen
Let's dive right in!

screen is a program that creates virtual terminals inside your terminal. It's somewhat like having multiple browser tabs, but for your command line!

Starting screen is super simple:
```
hacker@dojo:~$ screen
```
That's it! You're now inside a screen session. It looks exactly like a terminal, but there are new capabilities there, waiting to be discovered.

For this challenge, we've hooked things up so that just launching screen will get you the flag. Easy!

NOTE: When you're done with your command line, type exit or press Ctrl-D to leave the screen session. Then screen will terminate and return you to your original shell.

### Solve
**Flag:** `pwn.college{0FCjeUzGQUs0jxU1K4BOceR6Hrn.0VN4IDOxwiNyUDN0EzW}`

This challenge introduced GNU Screen, a terminal multiplexer that allows multiple virtual terminal sessions to run inside a single terminal window. The challenge was intentionally simple and only required launching a Screen session. Running the screen command started a new virtual terminal environment, and the challenge detected that a Screen session had been created. Upon successfully entering the session, the flag was immediately displayed. Exiting the Screen session with exit (or Ctrl+D) returned control to the original shell.

```bash
hacker@terminal-multiplexing~launching-screen:~$ screen
Congratulations! You're inside a screen session!
Here's your flag:
pwn.college{0FCjeUzGQUs0jxU1K4BOceR6Hrn.0VN4IDOxwiNyUDN0EzW}
[screen is terminating]
```

### New Learnings
Learned what a terminal multiplexer is and how GNU Screen creates virtual terminal sessions inside an existing terminal. Reinforced that Screen sessions behave like independent shells while remaining attached to a single terminal window. Also gained initial experience launching and exiting a Screen session, laying the foundation for managing multiple terminal environments simultaneously.
