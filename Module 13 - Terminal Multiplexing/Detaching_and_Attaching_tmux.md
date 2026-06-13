# Linux Luminarium
# Module 13: Terminal Multiplexing

## Detaching and Attaching (tmux)
Let's try the same thing with tmux!

tmux (terminal multiplexer) is screen's younger, more modern cousin. It does all the same things but with some different key bindings. The biggest difference? Instead of Ctrl-A, tmux uses Ctrl-B as its command prefix.

So to detach from tmux, you press Ctrl-B followed by d.

```
hacker@dojo:~$ tmux
[doing some work...]
[Press Ctrl-B, then d]
[detached (from session 0)]
hacker@dojo:~$ 
```
The commands also differ:

tmux ls - List sessions
tmux attach or tmux a - Reattach to session
For this challenge:

Launch tmux
Detach from it.
Run /challenge/run (this will send the flag to your detached session!)
Reattach to see your prize

### Solve
**Flag:** `pwn.college{EW3iKuW2AxsdAV1lxteCPey4JGT.0VO4IDOxwiNyUDN0EzW}`

This challenge introduced tmux, a modern terminal multiplexer that provides functionality similar to GNU Screen. A tmux session was first launched using the tmux command. The session was then detached by pressing Ctrl-B followed by d, which left the tmux session running in the background while returning control to the normal shell. After detaching, /challenge/run was executed. The challenge detected the detached tmux session and sent the flag directly into it instead of displaying it in the current terminal. Finally, the session was reattached using tmux attach (or tmux a), revealing the flag inside the tmux session.

```bash
hacker@terminal-multiplexing~detaching-and-attaching-tmux:~$ tmux
[detached (from session 0)]
hacker@terminal-multiplexing~detaching-and-attaching-tmux:~$ /challenge/run
Found detached tmux session: 0
Sending flag to your tmux session...

Flag sent! Now reattach to your tmux session with:
  tmux attach

You'll find the flag waiting for you there!
hacker@terminal-multiplexing~detaching-and-attaching-tmux:~$ tmux a
hacker@terminal-multiplexing~detaching-and-attaching-tmux:~$  echo Congratulations, here is your flag: pwn.college{EW3iKuW2AxsdAV1lxteCPey4JGT.0VO4IDOxwiNyUDN0EzW}
Congratulations, here is your flag: pwn.college{EW3iKuW2AxsdAV1lxteCPey4JGT.0VO4IDOxwiNyUDN0EzW}
[exited]
```

### New Learnings
Learned that tmux is a terminal multiplexer similar to GNU Screen, allowing multiple virtual terminal sessions to run independently of the current terminal window. Reinforced the concept of detaching sessions using Ctrl-B d, which keeps processes running in the background even after leaving the session. Also gained experience reattaching to detached tmux sessions with tmux attach and learned the key difference between tmux and Screen: tmux uses Ctrl-B as its command prefix instead of Screen's Ctrl-A.
