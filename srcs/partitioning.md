# Partitioning
```
# lsblk
NAME                     MAJ:MIN RM   SIZE RO TYPE  MOUNTPOINTS
sda                        8:0    0  30.8G  0 disk
├─sda1                     8:1    0   243M  0 part  /boot       # primary         
├─sda2                     8:2    0     1K  0 part              # extended
└─sda5                     8:5    0 223.3G  0 part              # logical
  └─sda5_crypt           254:0    0  23.3G  0 crypt 
    ├─LVMGroup-root      254:0    0  23.3G  0 lvm   /
    ├─LVMGroup-swap      254:0    0  23.3G  0 lvm   [SWAP]
    ├─LVMGroup-home      254:0    0  23.3G  0 lvm   /home
    ├─LVMGroup-var       254:0    0  23.3G  0 lvm   /var
    ├─LVMGroup-srv       254:0    0  23.3G  0 lvm   /srv
    ├─LVMGroup-tmp       254:0    0  23.3G  0 lvm   /tmp
    └─LVMGroup-var--log  254:0    0  23.3G  0 lvm   /var/log
sr0                       11:0    1  1024M  0 rom
```
