# Linux Luminarium
# Module 8: Data Manipulation

## Deleting Newlines
A common class of characters to remove is a line separator. This happens when you have a stream of data that you want to turn into a single line for further processing. You can specify newlines almost like any other character, by escaping them:

hacker@dojo:~$ echo "hello_world!" | tr _ "\n"
hello
world!
hacker@dojo:~$
Here, the backslash (\) signifies that the character that follows it is a standin for a character that's hard to input into the shell normally. The newline, of course, is hard to input because when you typically hit Enter, you'll run the command itself. \n is a standin for this newline, and it must be in quotes to prevent the shell interpreter itself from trying to interpret it and pass it to tr instead.

Now, let's combine this with deletion. In this challenge, we'll inject a bunch of newlines into the flag. Delete them with tr's -d flag and the escaped newline specification!

Fun fact! Want to actually replace a backslash (\) character? Because \ is the escape character, you gotta escape it! \\ will be treated as a backslash by tr. This isn't relevant to this challenge, but is a fun fact nonetheless!


### Solve
**Flag:** `pwn.college{cgWV0_plgj3tljlL2tZSqY1aYbX.0VNxEzNxwiNyUDN0EzW}`

This challenge focused on removing newline characters from a stream of text. The /challenge/run program printed the flag split across many lines, injecting newline characters between parts of it. By piping the output into tr -d "\n", every newline character was deleted from the stream. Since \n represents a newline and must be quoted so the shell passes it correctly to tr, the command effectively collapsed multiple lines into a single continuous line, revealing the complete flag in proper format.

```bash
hacker@data~deleting-newlines:~$ /challenge/run | tr -d "\n"
Your line-split flag: pwn.college{cgWV0_plgj3tljlL2tZSqY1aYbX.0VNxEzNxwiNyUDN0EzW}
```

### New Learnings
Learned how special characters like newlines can be represented using escape sequences such as \n, and why quoting is necessary to prevent the shell from interpreting them prematurely. Reinforced that tr -d can remove not only visible characters but also invisible control characters like line breaks. Also strengthened understanding of how stream manipulation allows restructuring output instantly without editing files manually.