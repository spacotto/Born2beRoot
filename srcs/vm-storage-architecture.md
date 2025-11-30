# About Storage Architecture
>[!WARNING]
>Despite being part of the [System Architecture](https://github.com/spacotto/Born2beRoot/blob/main/srcs/vm-system-architecture.md) (aka installation process), I have decided to dedicate a separate section to the Storage Architecture (aka the partitioning) due to the amount of information concerning this matter.

**Desired Outcome Sample:**
```
# lsblk
NAME                     MAJ:MIN  RM   SIZE  RO  TYPE  MOUNTPOINTS
sda                      xxx:x     0  xxxxx   0  disk             # Physical virtual disk
├─sda1                   xxx:x     0  xxxxx   0  part  /boot      # Primary partition (bootloader/kernel)
├─sda2                   xxx:x     0  xxxxx   0  part             # Reserved partition (LVM extended area)
└─sda5                   xxx:x     0  xxxxx   0  part             # Logical partition inside sda2
  └─sda5_crypt           xxx:x     0  xxxxx   0  crypt            # LUKS-encrypted container
    ├─LVMGroup-root      xxx:x     0  xxxxx   0  lvm   /          # Logical Volume: root filesystem
    ├─LVMGroup-swap      xxx:x     0  xxxxx   0  lvm   [SWAP]     # Logical Volume: swap space
    ├─LVMGroup-home      xxx:x     0  xxxxx   0  lvm   /home      # Logical Volume: user home directories
    ├─LVMGroup-var       xxx:x     0  xxxxx   0  lvm   /var       # Logical Volume: variable data
    ├─LVMGroup-srv       xxx:x     0  xxxxx   0  lvm   /srv       # Logical Volume: service data
    ├─LVMGroup-tmp       xxx:x     0  xxxxx   0  lvm   /tmp       # Logical Volume: temporary files
    └─LVMGroup-var--log  xxx:x     0  xxxxx   0  lvm   /var/log   # Logical Volume: persistent system logs
sr0                      xxx:x     1  xxxxx   0  rom              # Virtual CD-ROM drive (ISO)
```

## 1. Partition Disks 
>[!NOTE]
>[Here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/vm-partitioning.md) you can find more details on what partitioning is.

### 1.1 Select Manual 
[select-manual]

>[!IMPORTANT]
>Since our goal is to set up a specific architecture, we shall select the `Manual` option.

### 1.2 Create New Partition Table
[create-new-partition-table]

>[!NOTE]
>Since we are at the beginning of the setup, we do not have partitions and mount points yet. Thus, we shall select `SCSI3 (0,0,0) (sda)` to start the partitioning process, which **represents the entire device**.

### 1.3 Select Partition Table
[select-partition-table]

## 2. Partition

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
