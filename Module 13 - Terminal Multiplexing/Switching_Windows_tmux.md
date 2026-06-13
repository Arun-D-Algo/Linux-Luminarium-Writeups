# Linux Luminarium
# Module 13: Terminal Multiplexing

## Switching Windows (tmux)
Let's learn to navigate windows in tmux!

Just like screen, tmux has windows. The key combos are different, but the concept is the same:

Ctrl-B c - Create a new window
Ctrl-B n - Next window
Ctrl-B p - Previous window
Ctrl-B 0 through Ctrl-B 9 - Jump to window 0-9
Ctrl-B w - See a nice window picker
Tmux shows your windows at the bottom in a status bar that looks like:

[0] 0:bash* 1:bash
The * shows your current window, and each entry also shows the process that the window was created to run.

We've created a tmux session with two windows:

Window 0 has the flag!
Window 1 has your warm welcome.
Go get that flag!

### Solve
**Flag:** `pwn.college{E9WvfeJyr9nYfcGPzJSDyjKP_K2.0FM5IDOxwiNyUDN0EzW}`

TThis challenge introduced window management in tmux. A tmux session had already been created with two windows. Window 1 displayed instructions explaining that the flag was hidden in Window 0. After attaching to the session using tmux a (or tmux attach), the instructions in Window 1 were read. The tmux window-switching shortcut Ctrl-B 0 was then used to jump directly to Window 0. Once switched, the hidden message containing the flag became visible, successfully completing the challenge.

```bash
hacker@terminal-multiplexing~switching-windows-tmux:~$ tmux a
cat <<MSG
Welcome to the tmux window switching challenge!
You are currently in window 1.
The flag is hidden in window 0.
Use Ctrl-B 0 to switch to window 0!
MSG
hacker@terminal-multiplexing~switching-windows-tmux:~$  cat <<MSG
> Welcome to the tmux window switching challenge!
> You are currently in window 1.
> The flag is hidden in window 0.
> Use Ctrl-B 0 to switch to window 0!
> MSG
Welcome to the tmux window switching challenge!
You are currently in window 1.
The flag is hidden in window 0.
Use Ctrl-B 0 to switch to window 0!
hacker@terminal-multiplexing~switching-windows-tmux:~$  cat <<MSG
> Excellent work! You found window 0!
> Here is your flag: pwn.college{E9WvfeJyr9nYfcGPzJSDyjKP_K2.0FM5IDOxwiNyUDN0EzW}
> MSG
Excellent work! You found window 0!
Here is your flag: pwn.college{E9WvfeJyr9nYfcGPzJSDyjKP_K2.0FM5IDOxwiNyUDN0EzW}
[exited]
```

### New Learnings
Learned that tmux supports multiple windows within a single session, similar to tabs in a browser or windows in Screen. Reinforced the distinction between tmux sessions and tmux windows: attaching with tmux a connects to a session, while keyboard shortcuts are used to navigate between windows inside that session.