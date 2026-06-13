# Linux Luminarium
# Module 11: Percieving Permissions

## Fun with Group Names
In the previous levels, you may have noticed that your hacker user is a member of the hacker group, and that zardus is a member of the zardus group. There is a convention in Linux that every user has their own group, but this does not have to be the case. For example, many computer labs will put all of their users into a single, shared users group.

The point is, you've used hacker for the group before, but in this level, that is not going to work. I'll still allow you to use chgrp, but I have randomized the name of the group that your user is in. You will need to use the id command to figure that name out, then chgrp to victory!

### Solve
**Flag:** `pwn.college{sHToxYTpu4GL7uGcNjuGVYB_KnY.QXycjM1wiNyUDN0EzW}`

This challenge was almost identical to the previous one, but with a twist: the user's group was no longer named hacker. Instead, the group name was randomized. The id command was used to determine the group that the hacker user belonged to, revealing grp22799 as the primary group. The group ownership of /flag was then changed to this group using chgrp. Since the user was a member of that group, the file became readable and the flag could be retrieved with cat.

```bash
hacker@permissions~fun-with-groups-names:~$ whoami
hacker
hacker@permissions~fun-with-groups-names:~$ id
uid=1000(hacker) gid=1000(grp22799) groups=1000(grp22799)
hacker@permissions~fun-with-groups-names:~$ chgrp grp22799 /flag
hacker@permissions~fun-with-groups-names:~$ cat /flag
pwn.college{sHToxYTpu4GL7uGcNjuGVYB_KnY.QXycjM1wiNyUDN0EzW}
```

### New Learnings
Learned that Linux usernames and group names are independent concepts and do not have to match. Reinforced the use of the id command to inspect a user's UID, GID, and group memberships. Building on the previous challenge, this level showed that changing a file's group ownership only works if the file is assigned to a group that the current user actually belongs to. Also gained experience identifying group information dynamically instead of assuming a fixed group name such as hacker.