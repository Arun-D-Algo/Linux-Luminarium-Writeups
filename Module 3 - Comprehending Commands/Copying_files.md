# Linux Luminarium
# Module 3: Comprehending Commands

## Copying files
But what if you want to keep the original file? You can do so with the cp command. The usage is the same as with mv, but it will keep the source file.

This challenge wants you to copy the /flag file into /tmp/hack-the-planet (do it)! When you're done, run /challenge/check, which will check things out and give the flag to you.

### Solve
**Flag:** `pwn.college{IysB4iREslf_kAPjv1UiYWjrWbH.0lNxQTMywiNyUDN0EzW}`

Used the cp command to copy the /flag file into /tmp/hack-the-planet file, then ran /challenge/check to get the flag.

```bash
hacker@commands~copying-files:~$ cp /flag /tmp/hack-the-planet
Correct! Performing 'cp /flag /tmp/hack-the-planet'.
hacker@commands~copying-files:~$ /challenge/check
Congrats! You successfully copied the flag to /tmp/hack-the-planet! Here it is:
pwn.college{IysB4iREslf_kAPjv1UiYWjrWbH.0lNxQTMywiNyUDN0EzW}
```

### New Learnings
Learnt how to use the cp command.