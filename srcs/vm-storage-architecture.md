# About Storage Architecture
>[!WARNING]
>Despite being part of the [System Architecture](https://github.com/spacotto/Born2beRoot/blob/main/srcs/vm-system-architecture.md) (aka installation process), I have decided to dedicate a separate section to the Storage Architecture (aka the partitioning) due to the amount of information concerning this matter.

**Desired Outcome Sample:**
```
# lsblk
NAME                     MAJ:MIN  RM   SIZE  RO  TYPE  MOUNTPOINTS
sda                      xxx:x     0  xxxxx   0  disk
├─sda1                   xxx:x     0  xxxxx   0  part  /boot
├─sda2                   xxx:x     0  xxxxx   0  part
└─sda5                   xxx:x     0  xxxxx   0  part
  └─sda5_crypt           xxx:x     0  xxxxx   0  crypt  
    ├─LVMGroup-root      xxx:x     0  xxxxx   0  lvm   /
    ├─LVMGroup-swap      xxx:x     0  xxxxx   0  lvm   [SWAP]
    ├─LVMGroup-home      xxx:x     0  xxxxx   0  lvm   /home
    ├─LVMGroup-var       xxx:x     0  xxxxx   0  lvm   /var
    ├─LVMGroup-srv       xxx:x     0  xxxxx   0  lvm   /srv
    ├─LVMGroup-tmp       xxx:x     0  xxxxx   0  lvm   /tmp
    └─LVMGroup-var--log  xxx:x     0  xxxxx   0  lvm   /var/log
sr0                      xxx:x     1  xxxxx   0  rom
```

# Partition Disks
>[!NOTE]
>[Here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/vm-partitioning.md) you can find more details on what partitioning is.

## 1. Select Manual 
[select-manual]

>[!IMPORTANT]
>Since our goal is to set up a specific architecture, we shall select the `Manual` option.

## 2. Create New Partition Table
[create-new-partition-table]

>[!NOTE]
>Since we are at the beginning of the setup, we do not have partitions and mount points yet. Thus, we shall select `SCSI3 (0,0,0) (sda)` to start the partitioning process, which **represents the entire device**.

## 3. Select Partition Table
[select-partition-table]

## Logical Volume Manager (LVM)
>[!NOTE]
>[Here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/vm-lvm.md) you can find more information concerning the Logical Volume Manager (LVM).

### LVM root

### LVM swap

### LVM home

### LVM var

### LVM srv

### LVM tmp

### LVM var--log

## Final Result (`lsblk`)
