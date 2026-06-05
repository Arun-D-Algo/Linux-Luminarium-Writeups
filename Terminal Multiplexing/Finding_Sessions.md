# Linux Luminarium
# Module 13: Terminal Multiplexing

## Finding Sessions
Time for some screen detective work!

If you become an avid screen user, you will inevitably end up with multiple sessions running. How do you find the right one to reattach to?

Well, we can list them:

hacker@dojo:~$ screen -ls
There are screens on:
        23847.mysession   (Detached)
        23851.goodwork    (Detached)
        23855.morework    (Detached)
3 Sockets in /run/screen/S-hacker.
The identifiers of the sessions are the PID of each respective screen process, a dot, and the name of the screen session. To attach to a specific one, you use its name or its PID by giving it as an argument to screen -r.

hacker@dojo:~$ screen -r goodwork
In this challenge, we've created three screen sessions for you. One of them contains the flag. The other two are decoys!

You'll need to check each one until you find it. Don't forget to detach (Ctrl-A d) before trying the next session!

### Solve
**Flag:** `pwn.college{w6oVdWiR_4EaEYn6iEKLkDghO8j.01N4IDOxwiNyUDN0EzW}`

This challenge expanded on Screen session management by introducing multiple detached sessions. Three Screen sessions had already been created, but only one contained the flag while the others were decoys. The screen -ls command was used to list all active Screen sessions and display their identifiers. Each session was then reattached individually using screen -r <session-name> (or the session PID). After checking the contents of each session and detaching with Ctrl-A d, the correct session was eventually found. Reattaching to that session revealed the flag.

```bash
hacker@terminal-multiplexing~finding-sessions:~$  echo 'Congratulations! You found the right session!'
Congratulations! You found the right session!
hacker@terminal-multiplexing~finding-sessions:~$  echo pwn.college{w6oVdWiR_4EaEYn6iEKLkDghO8j.01N4IDOxwiNyUDN0EzW}
pwn.college{w6oVdWiR_4EaEYn6iEKLkDghO8j.01N4IDOxwiNyUDN0EzW}
```

### New Learnings
Learned how to view all active Screen sessions using screen -ls. Reinforced that multiple detached Screen sessions can exist simultaneously, each identified by a unique session ID and name. Also gained experience reattaching to specific sessions with screen -r, navigating between multiple detached sessions, and using session management techniques to locate information stored in a particular Screen instance.