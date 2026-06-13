# Linux Luminarium
# Module 8: Data Manipulation

## Extracting Specific Sections of text
Sometimes, you want to grab specific columns of data, such as the first column, the third column, or the 42nd column. For this, there's the cut command.

For example, imagine that you have the following data file:

hacker@dojo:~$ cat scores.txt
hacker 78 99 67
root 92 43 89
hacker@dojo:~$
You could use cut to extract specific columns:

hacker@dojo:~$ cut -d " " -f 1 scores.txt
hacker
root
hacker@dojo:~$ cut -d " " -f 2 scores.txt
78
92
hacker@dojo:~$ cut -d " " -f 3 scores.txt
99
43
hacker@dojo:~$
The -d argument specifies the column delimiter (how columns are separated). In this case, it's a space character. Of course, it has to be in quotes here so that the shell knows that the space is an argument rather than a space separating other arguments! The -f argument specifies the field number (which column to extract).

In this challenge, the /challenge/run program will give you a bunch of lines with random numbers and single characters (characters of the flag) as columns. Use cut to extract the flag characters, then pipe them to tr -d "\n" (like the previous level!) to join them together into a single line. Your solution will look something like /challenge/run | cut ??? | tr ???, with the ??? filled out.


### Solve
**Flag:** `pwn.college{UXCoNyQFb2iFV4dLS5k2ZBQlZUE.01NxEzNxwiNyUDN0EzW}`

This challenge focused on extracting specific columns of structured text using the cut command. The /challenge/run program printed multiple lines where each line contained a number followed by a single character of the flag, separated by a space. By piping the output into cut -d " " -f 2, only the second field (the character column) was extracted from each line. Since each character was still on its own line, the result was then piped into tr -d "\n" to remove all newline characters and join them into a single continuous string, revealing the complete flag.

```bash
hacker@data~extracting-specific-sections-of-text:~$ /challenge/run
19499 p
11768 w
30547 n
6890 .
14610 c
30415 o
6632 l
21466 l
8340 e
29353 g
15086 e
25998 {
23081 U
26203 X
30627 C
11017 o
29479 N
7183 y
10784 Q
19876 F
26124 b
15552 2
32307 i
24701 F
19236 V
22329 4
29244 d
23832 L
2631 S
28980 5
19924 k
22234 2
4888 Z
6620 B
29728 Q
28755 l
31727 Z
8341 U
9194 E
1372 .
4963 0
2383 1
14154 N
30766 x
15497 E
32732 z
17832 N
7999 x
662 w
32140 i
6872 N
28247 y
13400 U
13627 D
13942 N
13257 0
29211 E
21177 z
8267 W
17549 }
hacker@data~extracting-specific-sections-of-text:~$ /challenge/run | cut -d " " -f 2 | tr -d "\n"
pwn.college{UXCoNyQFb2iFV4dLS5k2ZBQlZUE.01NxEzNxwiNyUDN0EzW}
```

### New Learnings
Learned how cut extracts specific fields from structured text using a delimiter and field selection. Reinforced how combining cut with tr allows both structural filtering (selecting columns) and formatting adjustments (removing newlines). Also strengthened understanding of how pipelines can be layered to progressively transform raw data into the desired final output.