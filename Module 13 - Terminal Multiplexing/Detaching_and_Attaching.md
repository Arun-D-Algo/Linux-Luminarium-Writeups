# Linux Luminarium
# Module 13: Terminal Multiplexing

## Detaching and Attaching
Now we'll start digging in with the magic of detaching!

Imagine you're working on something important over a remote connection, and your connection drops. With a normal terminal (outside of this awesome dojo environment), everything's gone. With screen, your work keeps running, and you can reattach later!

You can also detach on purpose, which we'll do in this challenge. You detach by pressing Ctrl-A, followed by d (for detach). This leaves your session running in the background while you return to your normal terminal.

```
hacker@dojo:~$ screen
[doing some work...]
[Press Ctrl-A, then d]
[detached from 12345.pts-0.hostname]
hacker@dojo:~$ 
```
To reattach, you can use the -r argument to screen:

```
hacker@dojo:~$ screen -r
```
For this challenge, you'll need to:

Launch screen
Detach from it.
Run /challenge/run (this will secretly send the flag to your detached session!)
Reattach to see your prize
FUN FACT: Ctrl-A is screen's activation key for all of its shortcuts in its default configuration. All screen functionality is activated by some command combination starting with Ctrl-A.

HINT: Remember: Hold Ctrl and press A, then release both and press d.

HINT: If you see [detached from...], you did it right!

### Solve
**Flag:** `pwn.college{E9bAHUJE-GuC4FPgAv5DtYgK8aF.0lN4IDOxwiNyUDN0EzW}`

This challenge introduced one of Screen's most powerful features: detaching and reattaching sessions. A Screen session was first launched using the screen command. Instead of terminating the session, it was detached by pressing Ctrl-A followed by d, which left the virtual terminal running in the background. After returning to the normal shell, /challenge/run was executed. The challenge secretly sent the flag to the detached Screen session rather than displaying it in the current terminal. Finally, the session was reattached using screen -r, allowing the hidden output to be viewed and the flag to be recovered.

```bash
hacker@terminal-multiplexing~detaching-and-attaching:~$
hacker@terminal-multiplexing~detaching-and-attaching:~$ echo Yes! Flag is: pwn.college{E9bAHUJE-GuC4FPgAv5DtYgK8aF.0lN4IDOxwiNyUDN0EzW}
Yes! Flag is: pwn.college{E9bAHUJE-GuC4FPgAv5DtYgK8aF.0lN4IDOxwiNyUDN0EzW}
```

### New Learnings
Learned how Screen sessions can continue running independently of the terminal they were launched from. Reinforced the concept of detaching a session with Ctrl-A d, which leaves programs running in the background without terminating them. Also gained experience reattaching to an existing session using screen -r, demonstrating how Screen can preserve work across disconnected terminals or interrupted remote connections.
