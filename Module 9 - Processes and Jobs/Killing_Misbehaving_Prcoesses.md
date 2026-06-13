# Linux Luminarium
# Module 9: Processes and Jobs

## Killing Misbehaving Processes
Sometimes, misbehaving processes can interfere with your work. These processes might need to be killed...

In this challenge, there's a decoy process that's hogging a critical resource - a named pipe (FIFO) at /tmp/flag_fifo into which (like in the Practicing Piping FIFO challenge) /challenge/run wants to write your flag. You need to kill this process.

Your general workflow should be:

Check what processes are running.
Find /challenge/decoy in the list and figure out its process ID.
kill it.
Run /challenge/run to get the flag without being overwhelmed by decoys (you don't need to redirect its output; it'll write to the FIFO on its own).
Good luck!

NOTE: You might see a few decoy flags show up even after killing the decoy process. This happens because Linux pipes are buffered: conceptually, they have a sort of length through which data flows, and you might kill the decoy process while data is in the pipe. That data, having already entered the pipe, will proceed to the other end (your cat). If you wait a second, you'll see the decoys stop, and then you can /challenge/run and win!

### Solve
**Flag:** `pwn.college{sM5Qdr6-vi0XYI6BiEKmjR6_Wzm.0FNzMDOxwiNyUDN0EzW}`

This challenge involved a decoy process that continuously occupied the FIFO at /tmp/flag_fifo, preventing the real challenge program from using it properly. The first step was to inspect the process list using ps -efww | grep /challenge/decoy, which revealed the running decoy process and its PID. After identifying the actual decoy process (PID 115), the kill command was used to terminate it. Once the interfering process was removed, /challenge/run successfully wrote to the FIFO and displayed the real flag. A number of fake flags continued to appear briefly because data already buffered inside the pipe was still being delivered, demonstrating how Linux pipe buffering works even after a process has been terminated.

```bash
hacker@processes~killing-misbehaving-processes:~$ ps -efww | grep /challenge/decoy
root         114       1  0 17:44 ?        00:00:00 su -c exec /challenge/decoy > /tmp/flag_fifo hacker
hacker       115     114  0 17:44 ?        00:00:00 /usr/bin/python3 /challenge/decoy
hacker       341     335  0 17:45 pts/1    00:00:00 grep --color=auto /challenge/decoy
hacker@processes~killing-misbehaving-processes:~$ kill 115
hacker@processes~killing-misbehaving-processes:~$ /challenge/run
Sending the flag to /tmp/flag_fifo!
pwn.college{W7M6jyLgHaENnMSOvrF5TE-316NgjNQRjTsgbrkSC4JZ6QV}
pwn.college{7CtXu3bAh7h13snqqmbUvabl0zgoIiJ22ALzF0lErUBjqX2}
pwn.college{ojq5sOdZ3svOeQWh5u7CQGolM656w4jKhIMFEggY9Hnhvd.}
pwn.college{Z3qkPkH.wGS-KsmgknEss9MdJBx3V3iAQNsDtcxxSExjPGp}
pwn.college{n9ue6WXMjjN-X3-9o5c.cr7EA8AezQ7jrvQHlIOcXdWrOs2}
pwn.college{Oa-rYNVjClpeayoNBCeHWKjleeTja0DUWDIv-FakjJCmlmA}
pwn.college{FJQPBblRhtX6rD2M2MoBBXyyFXzU4toOow1KvUF4yg-IoRt}
pwn.college{DaAgcOsG-YGN6mG1mHny-867MmnrklynxOHzhpcp580EfKf}
pwn.college{9LK22C6J8bFPFR9lDEjl4iOMmfGPJkaH3gEHiqccuT1cXad}
pwn.college{tJZDLc7Yz5WT1ElEOsp.ysBfGuO2XSiu94updjIxthQxq.I}
pwn.college{Y.pelFhqqykF5YWb64fVMfPOA9XVlGseCNb-TQ9lZVg.1Su}
pwn.college{qxwmJm0MnSJHAN-Lrgu5Mlwlcy1nRbpI684uJIhKpaAJ6sc}
pwn.college{NcoCEnMAI7565qNOdBZzRVi1ixY9DJ.ROb9BCxDCgxN2YPn}
pwn.college{yqbL-UhzMIikxBbdV8gr3EAzGADCxS3MjE-DF7atKkdXx39}
pwn.college{UeEHrk.NKptNXTsGxsndbWWaFaRk1p9IN47nuyll0IfcrzP}
pwn.college{dA-95nB8tQMb3WcW3IIlxMVMxE0gnI0I0Bx8M4kZ1FnQ-t4}
pwn.college{4PfxOHgAn10PvWscFjOlbbomjxg2QJ2Z5A.tJPsGgQZGjFg}
pwn.college{sM5Qdr6-vi0XYI6BiEKmjR6_Wzm.0FNzMDOxwiNyUDN0EzW}
```

### New Learnings
Learned how to identify and terminate specific running processes using their Process ID (PID). Reinforced the use of ps and grep together to locate a target process among many running processes. Also gained a better understanding of how processes can compete for shared resources such as FIFOs, and how killing a misbehaving process can restore normal system behavior.