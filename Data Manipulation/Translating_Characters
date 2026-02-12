# Linux Luminarium
# Module 8: Data Manipulation

## Translating Characters
One of the purposes of piping data is to modify it. Many Linux commands will help you modify data in really cool ways. One of these is tr, which translates characters it receives over standard input and prints them to standard output.

In its most basic usage, tr translates the character provided in its first argument to the character provided in its second argument:

hacker@dojo:~$ echo OWN | tr O P
PWN
hacker@dojo:~$
It can also handle multiple characters, with the characters in different positions of the first argument replaced with associated characters in the second argument.

hacker@dojo:~$ echo PWM.COLLAGE | tr MA NE
PWN.COLLEGE
hacker@dojo:~$
Now, you try it! In this level, /challenge/run will print the flag but will swap the casing of all characters (e.g., A will become a and vice-versa). Can you undo it with tr and get the flag?


### Solve
**Flag:** `pwn.college{0V2vmeZ8cICssM3TEoN23yZQ8-v.01MxEzNxwiNyUDN0EzW}`

This challenge focused on using the tr command to translate characters flowing through a pipeline. The /challenge/run program printed the flag with every letter’s case swapped, meaning uppercase letters were turned into lowercase and lowercase letters were turned into uppercase. By piping the output into tr and providing two character sets — one lowercase alphabet and one uppercase alphabet — each letter was translated back to its correct case. Since tr replaces characters positionally from the first set to the second set, reversing the alphabets effectively restored the original flag.

```bash
hacker@data~translating-characters:~$ /challenge/run | tr 'abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ' 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz'
yOUR CASE-SWAPPED FLAG:
pwn.college{0V2vmeZ8cICssM3TEoN23yZQ8-v.01MxEzNxwiNyUDN0EzW}
```

### New Learnings
Learned how tr performs direct character-by-character translation using positional mapping between two character sets. Reinforced the concept that tr works purely on streams from standard input to standard output, making it ideal for quick transformations in pipelines. Also strengthened understanding of how pipes allow command output to be modified immediately without creating intermediate files.