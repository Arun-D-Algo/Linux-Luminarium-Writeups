# Linux Luminarium
# Module 3: Comprehending Commands

## An Epic Filesystem Quest
With your knowledge of cd, ls, and cat, we're ready to play a little game!

We'll start it out in /. Normally:

```
hacker@dojo:~$ cd /
hacker@dojo:/$ ls
bin   challenge  etc   home  lib32  libx32  mnt  proc  run   srv  tmp  var
boot  dev        flag  lib   lib64  media   opt  root  sbin  sys  usr
```
That's a lot of contents! One day, you will be quite familiar with them, but already, you might recognize the flag file and the challenge directory.

In this challenge, I have hidden the flag! Here, you will use ls and cat to follow my breadcrumbs and find it! Here's how it'll work:

Your first clue is in /. Head on over there.
Look around with ls. There'll be a file named HINT or CLUE or something along those lines!
cat that file to read the clue!
Depending on what the clue says, head on over to the next directory (or don't!).
Follow the clues to the flag!
Good luck!

### Solve
**Flag:** `pwn.college{8UHgP8V9xv31IL7xn7X7rAmtAs-.QX5IDO0wiNyUDN0EzW}`

This challenge was a filesystem scavenger hunt that required following a chain of clues hidden throughout the Linux filesystem. Starting from the root directory (/), each clue was located using ls and read with cat, revealing the location of the next clue. Along the way, different mechanics were introduced, including delayed clues that only became readable after entering a directory with cd, hidden clues that required ls -a to discover, and trapped clues that had to be read directly via absolute paths without entering their directories. By carefully following each instruction and adapting to the different clue types, the final clue was located in /usr/share/doc/ncurses-bin/MESSAGE-TRAPPED, which revealed the flag.

```bash
hacker@commands~an-epic-filesystem-quest:~$ cd /
hacker@commands~an-epic-filesystem-quest:/$ ls
INSIGHT  boot       dev  flag  lib    media  nix  proc  run   srv  tmp  var
bin      challenge  etc  home  lib64  mnt    opt  root  sbin  sys  usr
hacker@commands~an-epic-filesystem-quest:/$ cat INSIGHT
Tubular find!
The next clue is in: /usr/lib/python3/dist-packages/wheel/cli

The next clue is **delayed** --- it will not become readable until you enter the directory with 'cd'.
hacker@commands~an-epic-filesystem-quest:/$ cd /usr/lib/python3/dist-packages/wheel/cli
hacker@commands~an-epic-filesystem-quest:/usr/lib/python3/dist-packages/wheel/cli$ ls
CUE  __init__.py  __pycache__  convert.py  pack.py  tags.py  unpack.py
hacker@commands~an-epic-filesystem-quest:/usr/lib/python3/dist-packages/wheel/cli$ cat CUE
Tubular find!
The next clue is in: /usr/lib/python3/dist-packages/pygments/formatters

The next clue is **delayed** --- it will not become readable until you enter the directory with 'cd'.
hacker@commands~an-epic-filesystem-quest:/usr/lib/python3/dist-packages/wheel/cli$ cd /usr/lib/python3/dist-packages/pygments/formatters
hacker@commands~an-epic-filesystem-quest:/usr/lib/python3/dist-packages/pygments/formatters$ ls
README       _mapping.py  html.py  latex.py        rtf.py       terminal256.py
__init__.py  bbcode.py    img.py   other.py        svg.py
__pycache__  groff.py     irc.py   pangomarkup.py  terminal.py
hacker@commands~an-epic-filesystem-quest:/usr/lib/python3/dist-packages/pygments/formatters$ cat README
Lucky listing!
The next clue is in: /usr/lib/python3/dist-packages/pwnlib/data/elf

The next clue is **hidden** --- its filename starts with a '.' character. You'll need to look for it using special options to 'ls'.
hacker@commands~an-epic-filesystem-quest:/usr/lib/python3/dist-packages/pwnlib/data/elf$ ls -a
.  ..  .SNIPPET  __init__.py  __pycache__  fmtstr  relro  ret2dlresolve
hacker@commands~an-epic-filesystem-quest:/usr/lib/python3/dist-packages/pwnlib/data/elf$ cat .SNIPPET
Lucky listing!
The next clue is in: /usr/lib/python3/dist-packages/pkg_resources/_vendor/packaging/__pycache__

The next clue is **delayed** --- it will not become readable until you enter the directory with 'cd'.
hacker@commands~an-epic-filesystem-quest:/usr/lib/python3/dist-packages/pwnlib/data/elf$ cd /usr/lib/python3/dist-packages/pkg_resources/_vendor/packaging/__pycache__
hacker@commands~an-epic-filesystem-quest:/usr/lib/python3/dist-packages/pkg_resources/_vendor/packaging/__pycache__$ ls
MEMO                         markers.cpython-312.pyc
__init__.cpython-312.pyc     metadata.cpython-312.pyc
_elffile.cpython-312.pyc     requirements.cpython-312.pyc
_manylinux.cpython-312.pyc   specifiers.cpython-312.pyc
_musllinux.cpython-312.pyc   tags.cpython-312.pyc
_parser.cpython-312.pyc      utils.cpython-312.pyc
_structures.cpython-312.pyc  version.cpython-312.pyc
_tokenizer.cpython-312.pyc
hacker@commands~an-epic-filesystem-quest:/usr/lib/python3/dist-packages/pkg_resources/_vendor/packaging/__pycache__$ cat MEMO
Congratulations, you found the clue!
The next clue is in: /usr/share/dpkg
hacker@commands~an-epic-filesystem-quest:/usr/lib/python3/dist-packages/pkg_resources/_vendor/packaging/__pycache__$ cd /usr/share/dpkg
hacker@commands~an-epic-filesystem-quest:/usr/share/dpkg$ ls
BRIEF            buildopts.mk          no-pie-link.specs  sh
abitable         buildtools.mk         ostable            tupletable
architecture.mk  cputable              pie-compile.specs  vendor.mk
buildapi.mk      default.mk            pie-link.specs
buildflags.mk    no-pie-compile.specs  pkg-info.mk
hacker@commands~an-epic-filesystem-quest:/usr/share/dpkg$ cat BRIEF
Lucky listing!
The next clue is in: /usr/share/doc/libgnutls30t64

The next clue is **delayed** --- it will not become readable until you enter the directory with 'cd'.
hacker@commands~an-epic-filesystem-quest:/usr/share/dpkg$ cd /usr/share/doc/libgnutls30t64
hacker@commands~an-epic-filesystem-quest:/usr/share/doc/libgnutls30t64$ ls
AUTHORS.gz  NEWS.gz       THANKS.gz            copyright
INFO        README.md.gz  changelog.Debian.gz
hacker@commands~an-epic-filesystem-quest:/usr/share/doc/libgnutls30t64$ cat INFO
Lucky listing!
The next clue is in: /usr/lib/python3/dist-packages/pwnlib/shellcraft/templates/powerpc/linux/syscalls

Watch out! The next clue is **trapped**. You'll need to read it out without 'cd'ing into the directory; otherwise, the clue will self destruct!
hacker@commands~an-epic-filesystem-quest:/usr/share/doc/libgnutls30t64$ ls /usr/lib/python3/dist-packages/pwnlib/shellcraft/templates/powerpc/linux/syscalls
CLUE-TRAPPED                olduname.asm
__doc__                     open.asm
_llseek.asm                 open_by_handle_at.asm
_newselect.asm              open_tree.asm
_sysctl.asm                 openat.asm
accept.asm                  openat2.asm
accept4.asm                 pause.asm
access.asm                  pciconfig_iobase.asm
acct.asm                    pciconfig_read.asm
add_key.asm                 pciconfig_write.asm
adjtimex.asm                perf_event_open.asm
afs_syscall.asm             personality.asm
alarm.asm                   pidfd_getfd.asm
arch_prctl.asm              pidfd_open.asm
arch_specific_syscall.asm   pidfd_send_signal.asm
arm_fadvise64_64.asm        pipe.asm
arm_sync_file_range.asm     pipe2.asm
bdflush.asm                 pivot_root.asm
bind.asm                    pkey_alloc.asm
bpf.asm                     pkey_free.asm
break_.asm                  pkey_mprotect.asm
brk.asm                     poll.asm
cachectl.asm                ppoll.asm
cacheflush.asm              ppoll_time64.asm
capget.asm                  prctl.asm
capset.asm                  pread.asm
chdir.asm                   pread64.asm
chmod.asm                   preadv.asm
chown.asm                   preadv2.asm
chown32.asm                 prlimit64.asm
chroot.asm                  process_vm_readv.asm
clock_adjtime.asm           process_vm_writev.asm
clock_adjtime64.asm         prof.asm
clock_getres.asm            profil.asm
clock_getres_time64.asm     pselect6.asm
clock_gettime.asm           pselect6_time64.asm
clock_gettime64.asm         ptrace.asm
clock_nanosleep.asm         putpmsg.asm
clock_nanosleep_time64.asm  pwrite.asm
clock_settime.asm           pwrite64.asm
clock_settime64.asm         pwritev.asm
clone.asm                   pwritev2.asm
clone3.asm                  query_module.asm
close.asm                   quotactl.asm
connect.asm                 read.asm
copy_file_range.asm         readahead.asm
creat.asm                   readdir.asm
create_module.asm           readlink.asm
delete_module.asm           readlinkat.asm
dup.asm                     readv.asm
dup2.asm                    reboot.asm
dup3.asm                    recv.asm
epoll_create.asm            recvfrom.asm
epoll_create1.asm           recvmmsg.asm
epoll_ctl.asm               recvmmsg_time64.asm
epoll_ctl_old.asm           recvmsg.asm
epoll_pwait.asm             remap_file_pages.asm
epoll_wait.asm              removexattr.asm
epoll_wait_old.asm          rename.asm
eventfd.asm                 renameat.asm
eventfd2.asm                renameat2.asm
execve.asm                  request_key.asm
execveat.asm                reserved221.asm
exit.asm                    reserved82.asm
exit_group.asm              restart_syscall.asm
faccessat.asm               rmdir.asm
fadvise64.asm               rseq.asm
fadvise64_64.asm            sched_get_priority_max.asm
fallocate.asm               sched_get_priority_min.asm
fanotify_init.asm           sched_getaffinity.asm
fanotify_mark.asm           sched_getattr.asm
fchdir.asm                  sched_getparam.asm
fchmod.asm                  sched_getscheduler.asm
fchmodat.asm                sched_rr_get_interval.asm
fchown.asm                  sched_rr_get_interval_time64.asm
fchown32.asm                sched_setaffinity.asm
fchownat.asm                sched_setattr.asm
fcntl.asm                   sched_setparam.asm
fcntl64.asm                 sched_setscheduler.asm
fdatasync.asm               sched_yield.asm
fgetxattr.asm               seccomp.asm
finit_module.asm            security.asm
flistxattr.asm              select.asm
flock.asm                   semctl.asm
fork.asm                    semget.asm
fremovexattr.asm            semop.asm
fsconfig.asm                semtimedop.asm
fsetxattr.asm               semtimedop_time64.asm
fsmount.asm                 send.asm
fsopen.asm                  sendfile.asm
fspick.asm                  sendfile64.asm
fstat.asm                   sendmmsg.asm
fstat64.asm                 sendmsg.asm
fstatat.asm                 sendto.asm
fstatat64.asm               set_mempolicy.asm
fstatfs.asm                 set_robust_list.asm
fstatfs64.asm               set_thread_area.asm
fsync.asm                   set_tid_address.asm
ftime.asm                   setdomainname.asm
ftruncate.asm               setfsgid.asm
ftruncate64.asm             setfsgid32.asm
futex.asm                   setfsuid.asm
futex_time64.asm            setfsuid32.asm
futimesat.asm               setgid.asm
get_kernel_syms.asm         setgid32.asm
get_mempolicy.asm           setgroups.asm
get_robust_list.asm         setgroups32.asm
get_thread_area.asm         sethostname.asm
getcpu.asm                  setitimer.asm
getcwd.asm                  setns.asm
getdents.asm                setpgid.asm
getdents64.asm              setpriority.asm
getegid.asm                 setregid.asm
getegid32.asm               setregid32.asm
geteuid.asm                 setresgid.asm
geteuid32.asm               setresgid32.asm
getgid.asm                  setresuid.asm
getgid32.asm                setresuid32.asm
getgroups.asm               setreuid.asm
getgroups32.asm             setreuid32.asm
getitimer.asm               setrlimit.asm
getpeername.asm             setsid.asm
getpgid.asm                 setsockopt.asm
getpgrp.asm                 settimeofday.asm
getpid.asm                  setuid.asm
getpmsg.asm                 setuid32.asm
getppid.asm                 setxattr.asm
getpriority.asm             sgetmask.asm
getrandom.asm               shmat.asm
getresgid.asm               shmctl.asm
getresgid32.asm             shmdt.asm
getresuid.asm               shmget.asm
getresuid32.asm             shutdown.asm
getrlimit.asm               sigaction.asm
getrusage.asm               sigaltstack.asm
getsid.asm                  signal.asm
getsockname.asm             signalfd.asm
getsockopt.asm              signalfd4.asm
gettid.asm                  sigpending.asm
gettimeofday.asm            sigprocmask.asm
getuid.asm                  sigqueueinfo.asm
getuid32.asm                sigreturn.asm
getxattr.asm                sigsuspend.asm
gtty.asm                    sigtimedwait.asm
ia32_arch_prctl.asm         sigtimedwait_time64.asm
ia32_io_pgetevents.asm      socket.asm
ia32_rseq.asm               socketcall.asm
ia32_statx.asm              socketcall_accept.asm
idle.asm                    socketcall_bind.asm
init_module.asm             socketcall_connect.asm
inotify_add_watch.asm       socketcall_getpeername.asm
inotify_init.asm            socketcall_getsockname.asm
inotify_init1.asm           socketcall_getsockopt.asm
inotify_rm_watch.asm        socketcall_listen.asm
io_cancel.asm               socketcall_recv.asm
io_destroy.asm              socketcall_recvfrom.asm
io_getevents.asm            socketcall_recvmsg.asm
io_pgetevents.asm           socketcall_send.asm
io_pgetevents_time64.asm    socketcall_sendmsg.asm
io_setup.asm                socketcall_sendto.asm
io_submit.asm               socketcall_setsockopt.asm
io_uring_enter.asm          socketcall_shutdown.asm
io_uring_register.asm       socketcall_socket.asm
io_uring_setup.asm          socketcall_socketpair.asm
ioctl.asm                   socketpair.asm
ioperm.asm                  splice.asm
iopl.asm                    ssetmask.asm
ioprio_get.asm              stat.asm
ioprio_set.asm              stat64.asm
ipc.asm                     statfs.asm
kcmp.asm                    statfs64.asm
kexec_file_load.asm         statx.asm
kexec_load.asm              stime.asm
keyctl.asm                  stty.asm
kill.asm                    swapoff.asm
lchown.asm                  swapon.asm
lchown32.asm                symlink.asm
lgetxattr.asm               symlinkat.asm
link.asm                    sync.asm
linkat.asm                  sync_file_range.asm
listen.asm                  sync_file_range2.asm
listxattr.asm               syncfs.asm
llistxattr.asm              sys_kexec_load.asm
lock.asm                    syscall.asm
lookup_dcookie.asm          sysfs.asm
lremovexattr.asm            sysinfo.asm
lseek.asm                   syslog.asm
lsetxattr.asm               sysmips.asm
lstat.asm                   tee.asm
lstat64.asm                 tgkill.asm
madvise.asm                 tgsigqueueinfo.asm
madvise1.asm                time.asm
mbind.asm                   timer_create.asm
membarrier.asm              timer_delete.asm
memfd_create.asm            timer_getoverrun.asm
migrate_pages.asm           timer_gettime.asm
mincore.asm                 timer_gettime64.asm
mkdir.asm                   timer_settime.asm
mkdirat.asm                 timer_settime64.asm
mknod.asm                   timerfd.asm
mknodat.asm                 timerfd_create.asm
mlock.asm                   timerfd_gettime.asm
mlock2.asm                  timerfd_gettime64.asm
mlockall.asm                timerfd_settime.asm
mmap.asm                    timerfd_settime64.asm
mmap2.asm                   times.asm
modify_ldt.asm              tkill.asm
mount.asm                   truncate.asm
move_mount.asm              truncate64.asm
move_pages.asm              tuxcall.asm
mprotect.asm                ugetrlimit.asm
mpx.asm                     ulimit.asm
mq_getsetattr.asm           umask.asm
mq_notify.asm               umount.asm
mq_open.asm                 umount2.asm
mq_timedreceive.asm         uname.asm
mq_timedreceive_time64.asm  unlink.asm
mq_timedsend.asm            unlinkat.asm
mq_timedsend_time64.asm     unshare.asm
mq_unlink.asm               uselib.asm
mremap.asm                  userfaultfd.asm
msgctl.asm                  ustat.asm
msgget.asm                  utime.asm
msgrcv.asm                  utimensat.asm
msgsnd.asm                  utimensat_time64.asm
msync.asm                   utimes.asm
munlock.asm                 vfork.asm
munlockall.asm              vhangup.asm
munmap.asm                  vm86.asm
name_to_handle_at.asm       vm86old.asm
nanosleep.asm               vmsplice.asm
newfstatat.asm              vserver.asm
nfsservctl.asm              wait4.asm
nice.asm                    waitid.asm
oldfstat.asm                waitpid.asm
oldlstat.asm                write.asm
oldolduname.asm             writev.asm
oldstat.asm
hacker@commands~an-epic-filesystem-quest:/usr/share/doc/libgnutls30t64$ cat /usr/lib/python3/dist-packages/pwnlib/shellcraft/templates/powerpc/linux/syscalls/CLUE-TRAPPED
Tubular find!
The next clue is in: /usr/share/doc/ncurses-bin

Watch out! The next clue is **trapped**. You'll need to read it out without 'cd'ing into the directory; otherwise, the clue will self destruct!
hacker@commands~an-epic-filesystem-quest:/usr/share/doc/libgnutls30t64$ ls /usr/share/doc/ncurses-bin
MESSAGE-TRAPPED  changelog.Debian.gz  copyright
hacker@commands~an-epic-filesystem-quest:/usr/share/doc/libgnutls30t64$ cat /usr/share/doc/ncurses-bin/MESSAGE-TRAPPED
CONGRATULATIONS! Your perserverence has paid off, and you have found the flag!
It is: pwn.college{8UHgP8V9xv31IL7xn7X7rAmtAs-.QX5IDO0wiNyUDN0EzW}
```

### New Learnings
Learned how multiple Linux commands work together to navigate and explore the filesystem systematically. Reinforced the use of cd, ls, ls -a, and cat for discovering files, reading clues, and traversing directories. Also gained experience handling special challenge conditions such as hidden files, delayed clues that require entering a directory, and trapped clues that must be accessed through absolute paths without changing directories.
