# Linux Luminarium
# Module 13: Terminal Multiplexing

## Switching Windows
Okay, so far, screen is just a weird sort of terminal-with-a-terminal. But it can be much more!

Inside a single screen session, you can have multiple windows, like your browser has multiple tabs. This can be super handy for organizing different tasks!

These windows are handled with different keyboard shortcuts, all starting with Ctrl-A:

Ctrl-A c - Create a new window
Ctrl-A n - Next window
Ctrl-A p - Previous window
Ctrl-A 0 through Ctrl-A 9 - Jump directly to window 0-9
Ctrl-A " - bring up a selection menu of all of the windows
For this challenge, we've set up a screen session with two windows:

Window 0 has... well, you'll have to switch there to find out!
Window 1 has a welcome message
Attach to the session with screen -r, then use one of the key combinations above to switch to Window 1. Go get that flag!

### Solve
**Flag:** `pwn.college{Q8c96rmyjSo14IyRYly0BwrEjWl.0FO4IDOxwiNyUDN0EzW}`

This challenge introduced Screen windows, which function similarly to tabs inside a web browser. A Screen session was already running and contained two windows. Window 1 displayed a welcome message explaining that the flag was located in Window 0.

The session was attached using screen -r, which opened Window 1. After reading the instructions, the Screen window-switching shortcut Ctrl-A 0 was used to jump directly to Window 0. Once switched, the hidden message containing the flag became visible. After viewing the flag, the Screen session terminated normally.

```bash
hacker@terminal-multiplexing~switching-windows:~$ screen -r
 cat <<MSG
Welcome to the window switching challenge!
You are currently in window 1.
The flag is hidden in window 0.
Use Ctrl-A 0 to switch to window 0!
MSG
hacker@terminal-multiplexing~switching-windows:~$  cat <<MSG
> Welcome to the window switching challenge!
> You are currently in window 1.
> The flag is hidden in window 0.
> Use Ctrl-A 0 to switch to window 0!
> MSG
Welcome to the window switching challenge!
You are currently in window 1.
The flag is hidden in window 0.
Use Ctrl-A 0 to switch to window 0!
hacker@terminal-multiplexing~switching-windows:~$ 
hacker@terminal-multiplexing~switching-windows:~$  cat <<MSG
> Excellent work! You found window 0!
> Here is your flag: pwn.college{Q8c96rmyjSo14IyRYly0BwrEjWl.0FO4IDOxwiNyUDN0EzW}
> MSG
Excellent work! You found window 0!
Here is your flag: pwn.college{Q8c96rmyjSo14IyRYly0BwrEjWl.0FO4IDOxwiNyUDN0EzW}
[screen is terminating]
```

### New Learnings
Learned that a single Screen session can contain multiple independent windows, similar to tabs within a browser. Reinforced the distinction between Screen sessions and Screen windows: attaching with screen -r connects to a session, while keyboard shortcuts are used to move between windows inside that session.
