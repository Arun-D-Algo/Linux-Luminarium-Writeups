# Linux Luminarium
# Module 12: Chaining Commands

## Understanding Shebangs
You're well on your way to your new life as a shell scripter! However, so far, your shellscripts can only be launched from the shell. Things worked great in the previous level (because you were invoking your script from the bash shell), but they won't work if your script was being invoked by, say, a program written in Python (or any other language).

When a program is invoked in Linux, the Linux kernel first inspects the file to determine how it should be run. This does NOT use the extension (which is why you don't have to name your shell scripts with a .sh extension, or your Python scripts with a .py extension, or so on). Rather, Linux looks at the first few bytes of the file for this information.

There are a bunch of different types of programs, but if the program file starts with the characters #! (often termed a "shebang"), Linux treats the file as an interpreted program, and the contents of the rest of the line as the path to the interpreter. It then invokes the interpreter with the path to the program file as its only argument.

Consider this shell script:

#!/bin/bash

echo "Hello Hackers!"
This can be executed as:

hacker@dojo:~$ chmod a+x script.sh
hacker@dojo:~$ ./script.sh
Hello Hackers!
hacker@dojo:~$
When ./script.sh was executed, Linux opened the file, read the first line, extracted /bin/bash as the interpreter, and executed /bin/bash ./script.sh to launch the script!

Note, the shebang line must be the VERY FIRST line of the file - no blank lines or spaces before it!

For this challenge, create a script at /home/hacker/solve.sh that has a proper shebang and outputs "hack the planet". Remember to make it executable, then run /challenge/run to verify your script works correctly!

FUN FACT: Common shebangs you might see:

#!/bin/bash for bash scripts
#!/usr/bin/python3 for Python scripts
#!/bin/sh for POSIX shell scripts --- this is a more primitive predecessor to bash with fewer features, but more compatibility to non-Linux systems!

### Solve
**Flag:** `pwn.college{sexWkXWL3akxzGtQWLIkT9uzU9w.0VOzMDOxwiNyUDN0EzW}`

This challenge required creating a script at /home/hacker/solve.sh that printed the text "hack the planet" and could be executed directly by the operating system. The script was created with the shebang #!/bin/bash as its first line, instructing Linux to use Bash as the interpreter whenever the file was executed. A second line containing echo "hack the planet" was added to produce the required output. After creating the script, /challenge/run was executed, which verified both the presence of a valid shebang and the expected output. Since the script met all requirements, the challenge revealed the flag.

```bash
hacker@chaining~understanding-shebangs:~$ echo '#!/bin/bash' > /home/hacker/solve.sh
hacker@chaining~understanding-shebangs:~$ echo 'echo "hack the planet"' >> /home/hacker/solve.sh
hacker@chaining~understanding-shebangs:~$ /challenge/run
Testing your script...
Perfect! Your flag:
Flag: pwn.college{sexWkXWL3akxzGtQWLIkT9uzU9w.0VOzMDOxwiNyUDN0EzW}
```

### New Learnings
Learned the purpose of a shebang (#!) and how Linux uses it to determine which interpreter should execute a script. Reinforced that file extensions are not used by the Linux kernel when deciding how to run a program. Also gained experience creating a script with a valid shebang, understanding why it must be the very first line of the file, and how executable scripts can automatically invoke their interpreter when run.
