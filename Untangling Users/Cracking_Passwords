# Linux Luminarium
# Module 10: Untangling Users

## Cracking Passwords
When you enter a password for su, it compares it against the stored password for that user. These passwords used to be stored in /etc/passwd, but because /etc/passwd is a globally-readable file, this is not good for passwords, these were moved to /etc/shadow. Here is the example /etc/shadow from the previous level:

root:$6$s74oZg/4.RnUvwo2$hRmCHZ9rxX56BbjnXcxa0MdOsW2moiW8qcAl/Aoc7NEuXl2DmJXPi3gLp7hmyloQvRhjXJ.wjqJ7PprVKLDtg/:19921:0:99999:7:::
daemon:*:19873:0:99999:7:::
bin:*:19873:0:99999:7:::
sys:*:19873:0:99999:7:::
sync:*:19873:0:99999:7:::
games:*:19873:0:99999:7:::
man:*:19873:0:99999:7:::
lp:*:19873:0:99999:7:::
mail:*:19873:0:99999:7:::
news:*:19873:0:99999:7:::
uucp:*:19873:0:99999:7:::
proxy:*:19873:0:99999:7:::
www-data:*:19873:0:99999:7:::
backup:*:19873:0:99999:7:::
list:*:19873:0:99999:7:::
irc:*:19873:0:99999:7:::
gnats:*:19873:0:99999:7:::
nobody:*:19873:0:99999:7:::
_apt:*:19873:0:99999:7:::
systemd-timesync:*:19901:0:99999:7:::
systemd-network:*:19901:0:99999:7:::
systemd-resolve:*:19901:0:99999:7:::
mysql:!:19901:0:99999:7:::
messagebus:*:19901:0:99999:7:::
sshd:*:19901:0:99999:7:::
hacker::19916:0:99999:7:::
zardus:$6$bEFkpM0w/6J0n979$47ksu/JE5QK6hSeB7mmuvJyY05wVypMhMMnEPTIddNUb5R9KXgNTYRTm75VOu1oRLGLbAql3ylkVa5ExuPov1.:19921:0:99999:7:::
Separated by :s, the first field of each line is the username and the second is the password. A value of * or ! functionally means that password login for the account is disabled, a blank field means that there is no password (a not-uncommon misconfiguration that allows password-less su in some configurations), and the long string such as Zardus' $6$bEFkpM0w/6J0n979$47ksu/JE5QK6hSeB7mmuvJyY05wVypMhMMnEPTIddNUb5R9KXgNTYRTm75VOu1oRLGLbAql3ylkVa5ExuPov1. is the result of one-way-encrypting (hashing) Zardus' password from the last level (in this case, dont-hack-me). Other fields in this file have other meanings, and you can read more about them here.

When you input a password into su, it one-way-encrypts (hashes) it and compares the result against the stored value. If the result matches, su grants you access to the user!

But what if you don't know the password? If you have the hashed value of the password, you can crack it! Even though /etc/shadow is, by default, only readable by root, leaks can happen! For example, backups are often stored, unencrypted and insufficiently protected, on file servers, and this has led to countless data disclosures.

If a hacker gets their hands on a leaked /etc/shadow, they can start cracking passwords and wreaking havoc. The cracking can be done via the famous John the Ripper, as so:

hacker@dojo:~$ john ./my-leaked-shadow-file
Loaded 1 password hash (crypt, generic crypt(3) [?/64])
Will run 32 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
password1337      (zardus)
1g 0:00:00:22 3/3 0.04528g/s 10509p/s 10509c/s 10509C/s lykys..lank
Use the "--show" option to display all of the cracked passwords reliably
Session completed
hacker@dojo:~$
Here, John the Ripper cracked Zardus' leaked password hash to find the real value of password1337. Poor Zardus!

This level simulates this story, giving you a leak of /etc/shadow (in /challenge/shadow-leak). Crack it (this could take a few minutes), su to zardus, and run /challenge/run to get the flag!


### Solve
**Flag:** `pwn.college{gFpbGjD3MY_d3hJS8-XirgFqu70.QX3UDN1wiNyUDN0EzW}`

The challenge simulated a leaked /etc/shadow file containing hashed user passwords. The hash belonging to the target user was cracked using a password-cracking tool, revealing the actual password. After switching to that user with su and authenticating successfully, the challenge program was executed to obtain the flag.

```bash
hacker@users~cracking-passwords:~$ john /challenge/shadow-leak
Created directory: /home/hacker/.john
Loaded 1 password hash (crypt, generic crypt(3) [?/64])
Press 'q' or Ctrl-C to abort, almost any other key for status
aardvark         (zardus)
1g 0:00:00:20 100% 2/3 0.04965g/s 289.1p/s 289.1c/s 289.1C/s Johnson..buzz
Use the "--show" option to display all of the cracked passwords reliably
Session completed
hacker@users~cracking-passwords:~$ john --show /challenge/shadow-leak
hacker:NO PASSWORD:20388:0:99999:7:::
zardus:aardvark:20501:0:99999:7:::

2 password hashes cracked, 0 left
hacker@users~cracking-passwords:~$ su zardus
Password: 
zardus@users~cracking-passwords:/home/hacker$ /challenge/run
Congratulations, you have become Zardus! Here is your flag:
pwn.college{gFpbGjD3MY_d3hJS8-XirgFqu70.QX3UDN1wiNyUDN0EzW}
```

### New Learnings
Learned that Linux stores hashed passwords in /etc/shadow instead of plain text for security. Learned that password authentication works by hashing user input and comparing it to the stored hash. Learned that leaked hash files can be cracked offline if weak passwords are used, emphasizing the importance of strong password practices and proper file protection.