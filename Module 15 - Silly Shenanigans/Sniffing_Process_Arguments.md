# Linux Luminarium
# Module 15: Silly Sehnanigans

## Sniffing Process Arguments
Poor Zardus; you've hacked him pretty heavily. But he's wisened up and secured his home directory! Game over?

Not quite! One of the things that people often don't think about when there are multiple accounts on one computer is what kind of data their command invocations leak. Remember, when you do ps aux, you get:

```
hacker@dojo:~$ ps aux
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
hacker         1  0.0  0.0   1128     4 ?        Ss   05:34   0:00 /sbin/docker-init -- /bin/sleep 6h
hacker         7  0.0  0.0   2736   580 ?        S    05:34   0:00 /bin/sleep 6h
hacker       102  0.4  0.0 723944 64660 ?        Sl   05:34   0:00 /usr/lib/code-server/lib/node /usr/lib/code-serve
hacker       138  3.3  0.0 968792 106272 ?       Sl   05:34   0:07 /usr/lib/code-server/lib/node /usr/lib/code-serve
hacker       287  0.0  0.0 717648 53136 ?        Sl   05:34   0:00 /usr/lib/code-server/lib/node /usr/lib/code-serve
hacker       318  3.3  0.0 977472 98256 ?        Sl   05:34   0:06 /usr/lib/code-server/lib/node --dns-result-order=
hacker       554  0.4  0.0 650560 55360 ?        Rl   05:35   0:00 /usr/lib/code-server/lib/node /usr/lib/code-serve
hacker       571  0.0  0.0   4600  4032 pts/0    Ss   05:35   0:00 /usr/bin/bash --init-file /usr/lib/code-server/li
hacker      1172  0.0  0.0   5892  2924 pts/0    R+   05:38   0:00 ps aux
hacker@dojo:~$
```
But what would happen if one of the arguments of one of those commands was something sensitive, like the flag or a password? This happens, and nefarious users sharing the same machine (or somehow otherwise listing processes on it) can steal that data and use it!

That's what this challenge explores. Zardus is using an automation script, passing his account password to it as an argument. Zardus is also allowed to use sudo (and, thus, to sudo cat /flag!). Steal the password, log in to Zardus' account (recall the su command from the Untangling Users module), and get that flag!

### Solve
**Flag:** `pwn.college{4b9RuLEgGrF-SPUt7JnnRIu-PZQ.0FOzEzNxwiNyUDN0EzW}`

This challenge demonstrated how sensitive information can leak through process arguments. Zardus launched an automation script while passing his account password directly on the command line. By inspecting running processes with ps aux, the password was visible in plain text. After extracting the password, it was used to switch to Zardus' account with su. Since Zardus had sudo privileges, the flag was retrieved using sudo cat /flag.

```bash
hacker@shenanigans~sniffing-process-arguments:~$ ps aux | grep zardus
root         123  0.0  0.0   4332  2560 ?        S    17:01   0:00 su -c auto.sh --user zardus --pass pw_3199028493 zardus
zardus       126  0.0  0.0   4752  2880 ?        Ss   17:01   0:00 /bin/bash /run/challenge/bin/auto.sh --user zardus --pass pw_3199028493
zardus       128  0.0  0.0 232424  3200 ?        S    17:01   0:00 sleep 6h
hacker       345  0.0  0.0 230748  2560 pts/0    S+   17:03   0:00 grep --color=auto zardus
hacker@shenanigans~sniffing-process-arguments:~$ su zardus
Password: 
zardus@shenanigans~sniffing-process-arguments:/home/hacker$ sudo cat /flag
pwn.college{4b9RuLEgGrF-SPUt7JnnRIu-PZQ.0FOzEzNxwiNyUDN0EzW}
```

### New Learnings
Learned that command-line arguments are often visible to other users through process-listing tools such as ps. This means passwords, API keys, tokens, and other secrets should never be passed as process arguments because they can be exposed to anyone who can view running processes. Also reinforced the use of su for switching users and how leaked credentials can lead directly to privilege escalation.