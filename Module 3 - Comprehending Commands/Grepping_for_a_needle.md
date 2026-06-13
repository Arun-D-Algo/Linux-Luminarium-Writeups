# Linux Luminarium
# Module 3: Comprehending Commands

## Grepping for a needle in a haystack
Sometimes, the files that you might cat out are too big. Luckily, we have the grep command to search for the contents we need! We'll learn it in this challenge.

There are many ways to grep, and we'll learn one way here:

hacker@dojo:~$ grep SEARCH_STRING /path/to/file
Invoked like this, grep will search the file for lines of text containing SEARCH_STRING and print them to the console.

In this challenge, I've put a hundred thousand lines of text into the /challenge/data.txt file. grep it for the flag!

HINT: The flag always starts with the text pwn.college.

### Solve
**Flag:** `pwn.college{Mbyt1KKbMwkYF0No89kRaOf_qHX.QX3EDO0wiNyUDN0EzW}`

Used the grep command, with search string as 'pwn.college' in the provided file path, to get the flag.

```bash
hacker@commands~grepping-for-a-needle-in-a-haystack:~$ grep pwn.college /challenge/data.txt
pwn.college{Mbyt1KKbMwkYF0No89kRaOf_qHX.QX3EDO0wiNyUDN0EzW}
```

### New Learnings
Learnt how to use the grep command.