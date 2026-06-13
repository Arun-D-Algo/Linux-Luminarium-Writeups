# Linux Luminarium
# Module 8: Data Manipulation

## Sorting Data
Files (or output lines of commands) aren't always in the order you need them! The sort command helps you organize data. It reads lines from input (or files) and outputs them in sorted order:

hacker@dojo:~$ cat names.txt
  hack
  the
  planet
  with
  pwn
  college
hacker@dojo:~$ sort names.txt
  college
  hack
  planet
  pwn
  the
  with
hacker@dojo:~$
By default, sort orders lines alphabetically. Arguments can change this:

-r: reverse order (Z to A)
-n: numeric sort (for numbers)
-u: unique lines only (remove duplicates)
-R: random order!
In this challenge, there's a file at /challenge/flags.txt containing 100 fake flags, with the real flag mixed among them. When sorted alphabetically, the real flag will be at the end (we made sure of this when generating fake flags). Go get it!


### Solve
**Flag:** `pwn.college{4bhDwJYC5GDHorNnjjNS5Mo6Kp-.0FM0MDOxwiNyUDN0EzW}`

This challenge focused on organizing data using the sort command. A file contained many fake flags mixed with the real one, and the key detail was that the real flag would appear last when the file was sorted alphabetically. By sorting the file and selecting the final line, the correct flag was isolated from the decoys. The task reinforced how sorting can be used strategically to reveal meaningful data hidden among noise.

```bash
hacker@data~sorting-data:~$ cat /challenge/flags.txt | sort -r
pwn.college{4bhDwJYC5GDHorNnjjNS5Mo6Kp-.0FM0MDOxwiNyUDN0EzW}
pwn.college{4bhDwJYC5GDHorNnjjNS5Mo6Kp-.0FM0MDOxwiNyUDN0EzW}
pwn.college{4bhDwJYC5GDHorNnjjNS5Mo6Kp-.0FM0MDOxwiNyUDN0EzW}
pwn.college{4bhDwJYC5GDHorNnjjNS5Mo6Kp-.0FM0MDNxwiNyTCN0EyW}
pwn.college{4bhDwJYC5GDHorNnjjNS5Mo6Jp-.0FM0MDOxwiNyUDN0EzW}
pwn.college{4bhDwJYC5GDHorNmjjNS5Mo6Kp-.0FM0MDOxwiNyUDN0EzW}
pwn.college{4bhDwJYC5GDHorMnjjNS5Mo6Kp-.0FM0MDOxwiNyUDN0EzW}
pwn.college{4bhDwJYC5GDHorMmjjNS5Mo6Kp-.0FM0MDOwwiNyUDN0EzW}
pwn.college{4bhDwJYC5GDHnrNnjjNS5Mn6Kp-.0FM0MDOxwiNyTDN0EzW}
pwn.college{4bhDwJYC5FDHorNnjjNS5Mo6Kp-.0FM0MDOxwiNyUDN0EzW}
pwn.college{4bhDwJYC4GDHorNnjjNS5Mo6Kp-.0FM0MDOxwiNxUDN0EzW}
pwn.college{4bhDwJYB5GDHorNnjjNS5Mo6Kp-.0FL0MDOxwiNyUCN0EzW}
pwn.college{4bhDwJXC5GDHorNnjiNS5Mo6Kp-.0FM0MDOxwiNyUDN0EzW}
pwn.college{4bhCwJYC5GDHorNnjjNS5Mo5Kp-.0FM0MCOwwiNyUDN0EzW}
pwn.college{4bgCvJYC5GDHorMmjjNR5Mn6Kp-.0FL0LDOxwiNxUCN0EzW}
pwn.college{4bgCvJYB5GCHorNmijNS4Mo6Kp-.0FL0MDOwwiMyUDN0EyW}
pwn.college{4agDvJXB5GDGorNmjjMS5Mo6Jo-.0FM0LCNxwiMyTDN0DyW}
pwn.college{3bhDwJYC5GDHorMnjiNS5Mo6Jp-.0FM0MDOxwiNyUDN0EzW}
pwn.collegd{4bhDwJYC5GDHorNnjjNS5Lo5Kp-.0FM0MDOxwiNxUDM0EzW}
pwn.collegd{4bhDvJYC5GDGorNnijNS5Mo6Kp-.0FM0MCOxwiNyUDM0EzV}
pwn.collegd{3agDvJYB5GDHorMnijNS4Mo6Jp-.0FM0MCNxvhNyTDN0EyW}
pwn.collefe{3bgDwIXC5GDGnrNnjjNS5Mo6Jp-.0FM0MDNxwhNyTDN0EzW}
pwn.collefd{4bhDwJYC5GDHorNnjjMS5Lo6Ko-.0FM0MDOxwiNyUCN0EzW}
pwn.colldge{4bhDwIYC4FDGorNnjjNS4Mo6Kp-.0FM0MDOxwhMyUDN0EzW}
pwn.colldge{4bhDvJYC5GDHnrNmjjMS5Mo6Kp-.0EM0MDOxwiNyUDN0EyW}
pwn.colldge{3bhDwJYB5GDGoqMnjjNS5Mo5Jp-.0EM0MDOxviNyTCN0DzW}
pwn.colkege{4bhDwIYC5GDHorNnjjNS5Lo6Kp-.0FM0MDOxviNyUDN0DzW}
pwn.colkege{4bgCvJYB4GDGorMnjjMS5Ln6Kp-.0FL0LDOxwiNyUDM0DyW}
pwn.colkege{3bhDvJYC5GCHnrNnjjMS4Mo6Kp-.0FM0MDOxwiNyTDN0DzW}
pwn.colkegd{3agDwIYB4GDHnrMmjjMS4Mo6Kp-.0EL0MDOwwhNxUCN0DyV}
pwn.colkefd{4bgDvJYB5GCGnrNnjiNS5Mo6Kp-.0FM0MDOxwiNyUCM0EzW}
pwn.colkdge{4bgDvIYC5GDHnqNmiiNS5Mo6Kp-.0FM0MDNxwiMyUDN0DyW}
pwn.coklege{4bhCwJYC5GCGnrMnjjNS5Mo5Kp-.0FM0MDNxwiNxUCM0DzW}
pwn.coklege{3ahDwIXC4GDGnqNnjiMR4Mo5Jp-.0EM0LCNxviNxUDN0DyV}
pwn.coklefe{3bhDwIYC4FCHnrMmijNS5Ln6Kp-.0EM0LCOwwhNyTCN0DzW}
pwn.cokldge{4ahCwIYB5GCHnrMmiiNR5Mn5Kp-.0EM0MDNxviNxUDM0EyW}
pwn.cokkegd{4bhDwIYB5FDGorNmijMS5Mo6Kp-.0FM0MDOwvhNyUDN0EzV}
pwn.cokkefd{4agDwIYC5FDGoqNnjjMS5Ln6Ko-.0FM0MCOxwiMyUDN0EyW}
pwn.cnllege{4bhDwJYC5GCHorNnjjMS5Mo6Kp-.0FL0MDOxwiNyTDN0EzW}
pwn.cnllege{4bhCwJYC5GDHoqNnjjNS5Mo6Jp-.0FL0MCOwwiNyUDN0DzW}
pwn.cnlkege{4bgDwJYC5GDGorMnjjNS5Mo6Kp-.0FL0MCNxviNyTCN0DzV}
pwn.cnkldge{4bhDwJYC5GDHorNnjjNS5Mo6Jp-.0FM0MDOxwiNyUDN0EzV}
pwn.bollege{4bhDwIYC5GDHorNnjjNS5Mo6Kp-.0FM0MDOxwiNyUDN0EzW}
pwn.bollege{4bhDvJYB5GDHnrNmijNS5Mo6Kp-.0FM0MDOxwiNxUDN0EzW}
pwn.bolldge{4bhDwIYB5GDHorNnjjNS5Mo5Kp-.0FM0LDOxwiMyUCN0EzW}
pwn.bolldfd{3bhDvJXC5FCGoqNnjjNR5Mo6Kp-.0EM0MDNxvhMyTDN0EyW}
pwn.bolkdfd{4bhDwIXC5FDHorMmjiMS5Mo5Jo-.0FM0LCOxvhNxTDN0EyW}
pwn.boklefe{4agDwJYB4GCHorNnjiMS5Mo6Ko-.0FL0MCOwwiNyTCM0EzW}
pwn.bokldgd{3bhDwIXC5FCGoqNmjiNS4Mo6Jp-.0FM0LDOxvhNxUDN0DzW}
pwn.bnlldge{4agDwJYB4GCGorNnjjNS5Mo6Ko-.0FM0MDOxviNyUDN0DzW}
pwn.bnlldfe{3bgDvJYB5GDHoqNnjjNS4Mn5Kp-.0FM0MDOwviNyTDN0EzW}
pwn.bnlkege{4ahDwIYC5FCHorNnjjMS5Lo6Kp-.0FM0MCOwwiMyUDN0EzV}
pwm.college{4bhDwJYC5GDHorNnjjNS5Mn6Kp-.0FM0MDOxwiNyUDN0EzW}
pwm.college{4bhDwJXB4GDHorMmijNS5Mo6Kp-.0FM0MDNxwiNyUDM0DzW}
pwm.college{4ahDvJYC5GCHorNmjjNS4Mn6Kp-.0FL0MDOxwiNyUDN0EzW}
pwm.colldge{4bhDwIYC5GDHorNnjjNS5Mo6Kp-.0EM0MDOxwiNyUDN0EzW}
pwm.colldgd{4bhCvIYC4GDGnrMnjiNS4Mo6Kp-.0FM0MDNwwiNyTDM0EzV}
pwm.colldgd{4bgDwIXB5GDHoqMmjjNS5Lo5Ko-.0EM0MDNwwiMxUCN0EzW}
pwm.cokkege{4bhDwJYC5GCGorNnjiNS5Mo5Jo-.0FM0LDNxviMxUDM0EzV}
pwm.cnklefe{4bhCwJYC5FDHorNmjjNS4Ln6Kp-.0FL0MDOxwiNyUDN0EzW}
pwm.cnklefe{3ahDwJYB5GDHorNnjjNS5Mo6Jp-.0FM0MDNxviNyTDN0EzV}
pwm.cnkldge{4bhDvJYC4FCHoqNniiNS5Lo6Kp-.0EM0MDOwviMyUDN0EzW}
pwm.bollege{4ahDvJYC5GDHorMnjjMS5Mo6Kp-.0FM0MDNxwiNyUCN0EzV}
pwm.boklege{3bgCwIYC4GDHoqNnjiNS5Mn5Kp-.0FM0LDNwwiNyUDM0EzW}
pwm.bnllege{4bhCwJXC5GDHnrNnjiNR5Mo6Ko-.0FL0MDOxwiMxUDN0DyW}
pvn.college{4bhDwIYC5GDHorNmjjNS5Mo6Kp-.0FM0MDOxwiNyUDN0EzW}
pvn.college{3bhDwJYC5GDHorNnjjNS5Mo6Ko-.0FM0MDNxwiNyUDN0EzW}
pvn.colldfe{4bgDvIYC5GDHoqNnjiNS5Mo5Jo-.0FM0LDOxwiNxUDM0DzW}
pvn.colkege{3bhDwJYC5GDHoqMnijNS5Mo6Kp-.0EM0MCOwwiNxUDN0EzW}
pvn.coklege{4ahDwJYC5FDHnrNniiNS4Mo6Kp-.0FM0MDOwwiNyUDN0DzW}
pvn.coklege{3bhCwJYC4GDHnrMniiNS4Mn6Ko-.0FM0MCOxvhNyUCN0EzW}
pvn.cnlldge{3bgDwIYB5GDHoqNmijNS4Mo6Kp-.0FM0MDNxwiMyUDN0EzV}
pvn.cnkldgd{4bgDwJYC5FDHnqMmijNS5Ln6Jo-.0FL0MDOwwiMyUDM0EzV}
pvn.bollege{4bhDwJYC5FDHorNnjjNS5Mo6Kp-.0FM0MCOxwiNyUDN0EzW}
pvn.boklege{3bgDvIYC4GDHnqMnjjMR4Mo6Kp-.0FM0MCNxwiMyUCN0EyV}
pvn.boklefe{4agDvIXC4FDGoqNnjjNS5Lo6Kp-.0FM0MCOwwiNxUDN0EzV}
pvn.bokldge{4ahDwJYC4FDHorNniiMS4Mo5Jo-.0FM0MDOxwiMyUDM0DzW}
pvn.bokldge{3ahDwIXC5GDHorNnjiMS4Mo5Jp-.0FM0LCOxviMyUCN0DzV}
pvn.bnlkdge{4bhCwJYB5FDHoqNnjiNS4Mo5Jp-.0FM0MDNwviNyTDN0EyW}
pvm.college{4bhDvJXC4GDHnrNnjjMS5Mo5Kp-.0FM0MDOwwiNxUDN0EzW}
pvm.colldfe{4bhDvIYB4FCHnrNniiNS4Mn6Jp-.0FM0LDOxwhNyUDM0EzW}
pvm.coklefe{4ahDwJYC5GDGoqMnjjMS5Lo6Ko-.0EM0MCOxvhNyUDN0EyV}
own.college{4bhDvJXB4GCHorNnjiNS5Mo5Kp-.0FM0LDOxwiNyUDN0EzV}
own.colkegd{4bhDwJYC5GDGorNmjiNS5Mo6Ko-.0FM0MCOxwiMyUDM0EzV}
own.colkdge{3ahDwJYB5FCHnrMnjiMR5Mo6Kp-.0EL0LDOxviNyUCN0EyV}
own.coklege{4bhDwJYB5GDHoqNnjjNS5Mo6Jp-.0FM0MDOxwiNyUDN0EzW}
own.cokldgd{4bgDwIXC4GDHoqMnijNS4Lo6Kp-.0FM0MCOxviNyTCM0EzW}
own.cnllege{4ahDvJYC5GDHoqNnijNR4Mo6Kp-.0FL0MDOxwiNxUDN0EzV}
own.cnllefd{3bhCwJYB4GDGoqNnjjNS5Mo6Kp-.0FM0MDOwviMyTDN0EyW}
own.cnlldfe{3bgDvJYB5GDHorMnjiMR4Mn6Jp-.0FL0MDOxwiMxUDN0EyW}
own.bollege{4bhDwJYC4GDHorNnjjMS4Mn6Kp-.0FL0LDOxwiNyUCN0EzW}
own.bollege{3bgCwJYC5GDHorMmjjNS5Mn6Jp-.0FL0LCOwviNyUCN0DzV}
owm.bolkege{3bhDwJYC5GCHnrNnijNS5Mo6Jp-.0FM0MDOxviNxUDM0EzW}
ovn.colkege{3bhDvJXC5FDHnrNnjjNR4Mo6Kp-.0FM0MDNwwhMyTDM0DzW}
ovn.bollege{4bhDvIXB4GDHnrNnjjNS5Ln5Kp-.0FM0MDNwwhNyTCM0EzV}
ovn.bollege{4ahDwJYC5GDHorNnjiNS5Mo6Kp-.0FM0MDOxwiNyUCN0EzW}
ovn.bokldgd{3bhDwJXC5GDHoqNmiiNS5Ln5Jp-.0FL0MCOxwiMyUDM0EyW}
ovn.bnklegd{4bgCvJYB5GDHnrNnjjMS5Lo6Kp-.0EM0MDOwwhNyTCM0EzV}
ovm.cnllege{4bhDwJYB4GCHnrNmjjMR5Mo6Kp-.0EL0LDOxwiNyUCM0EzV}
ovm.bollege{4bhCwJYC4GDHorNnjjMS5Mo6Ko-.0FM0MCNwwiNyUDN0EzW}
ovm.bolldgd{3ahDwIXB5GDGnqMmjjNS5Mo6Kp-.0EM0MDOwvhNyUDM0DyW}
```

### New Learnings
Learned how sort arranges text alphabetically by default and how understanding ordering behavior can be used to locate specific data. Reinforced that commands can operate directly on files without needing cat, and strengthened understanding of how combining sorting with other tools like tail enables precise extraction of desired results from large datasets.