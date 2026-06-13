# Linux Luminarium
# Module 3: Comprehending Commands

## Finding files
So now we know how to list, read, and create files. But how do we find them? We use the find command!

The find command takes optional arguments describing the search criteria and the search location. If you don't specify a search criteria, find matches every file. If you don't specify a search location, find uses the current working directory (.). For example:

```
hacker@dojo:~$ mkdir my_directory
hacker@dojo:~$ mkdir my_directory/my_subdirectory
hacker@dojo:~$ touch my_directory/my_file
hacker@dojo:~$ touch my_directory/my_subdirectory/my_subfile
hacker@dojo:~$ find
.
./my_directory
./my_directory/my_subdirectory
./my_directory/my_subdirectory/my_subfile
./my_directory/my_file
hacker@dojo:~$
```
And when specifying the search location:

```
hacker@dojo:~$ find my_directory/my_subdirectory
my_directory/my_subdirectory
my_directory/my_subdirectory/my_subfile
hacker@dojo:~$
```
And, of course, we can specify the criteria! For example, here, we filter by name:

```
hacker@dojo:~$ find -name my_subfile
./my_directory/my_subdirectory/my_subfile
hacker@dojo:~$ find -name my_subdirectory
./my_directory/my_subdirectory
hacker@dojo:~$
```
You can search the whole filesystem if you want!

```
hacker@dojo:~$ find / -name hacker
/home/hacker
hacker@dojo:~$
```
Now it's your turn. I've hidden the flag in a random directory on the filesystem. It's still called flag. Go find it!

Several notes. First, there are other files named flag on the filesystem. Don't panic if the first one you try doesn't have the actual flag in it. Second, there're plenty of places in the filesystem that are not accessible to a normal user. These will cause find to generate errors, but you can ignore those; we won't hide the flag there! Finally, find can take a while; be patient!

### Solve
**Flag:** `pwn.college{835rKgRXGRIhExunD8WkUjtGqeH.QXyMDO0wiNyUDN0EzW}`

This challenge required locating a file named flag hidden somewhere on the filesystem. To search the entire filesystem, find / -name flag was used, which recursively examined directories starting from the root (/). During the search, several "Permission denied" messages appeared for protected directories, but these could safely be ignored. The command returned multiple files named flag, so each potential match had to be checked manually. Reading /usr/share/perl5/Dpkg/Vendor/flag with cat revealed the correct flag and completed the challenge.

```bash
hacker@commands~finding-files:~$ find / -name flag
find: ‘/etc/ssl/private’: Permission denied
/usr/lib/python3/dist-packages/pwnlib/flag
/usr/share/perl5/Dpkg/Vendor/flag
find: ‘/var/cache/apt/archives/partial’: Permission denied
find: ‘/var/cache/ldconfig’: Permission denied
find: ‘/var/lib/apt/lists/partial’: Permission denied
find: ‘/root’: Permission denied
^C
hacker@commands~finding-files:~$ cat /usr/share/perl5/Dpkg/Vendor/flag
pwn.college{835rKgRXGRIhExunD8WkUjtGqeH.QXyMDO0wiNyUDN0EzW}
```

### New Learnings
Learned how to use the find command to search for files across the filesystem based on specific criteria. Reinforced that find can start searching from any directory and that the -name option filters results by filename. Also gained experience dealing with permission-denied errors, understanding that inaccessible directories do not prevent find from continuing its search elsewhere.