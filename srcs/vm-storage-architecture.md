# About Storage Architecture
>[!WARNING]
>Despite being part of the [System Architecture](https://github.com/spacotto/Born2beRoot/blob/main/srcs/vm-system-architecture.md) (aka installation process), I have decided to dedicate a separate section to the Storage Architecture (aka the partitioning) due to the amount of information concerning this matter.

**Desired Outcome Sample:**
```
# lsblk
NAME                     MAJ:MIN  RM   SIZE  RO  TYPE  MOUNTPOINTS
sda                      xxx:x     0  xxxxx   0  disk               # Physical virtual disk
├─sda1                   xxx:x     0  xxxxx   0  part  /boot        # Primary partition (bootloader/kernel)
├─sda2                   xxx:x     0  xxxxx   0  part               # Reserved partition (LVM extended area)
└─sda5                   xxx:x     0  xxxxx   0  part               # Logical partition inside sda2
  └─sda5_crypt           xxx:x     0  xxxxx   0  crypt              # LUKS-encrypted container
    ├─LVMGroup-root      xxx:x     0  xxxxx   0  lvm   /            # Logical Volume: root filesystem
    ├─LVMGroup-swap      xxx:x     0  xxxxx   0  lvm   [SWAP]       # Logical Volume: swap space
    ├─LVMGroup-home      xxx:x     0  xxxxx   0  lvm   /home        # Logical Volume: user home directories
    ├─LVMGroup-var       xxx:x     0  xxxxx   0  lvm   /var         # Logical Volume: variable data
    ├─LVMGroup-srv       xxx:x     0  xxxxx   0  lvm   /srv         # Logical Volume: service data
    ├─LVMGroup-tmp       xxx:x     0  xxxxx   0  lvm   /tmp         # Logical Volume: temporary files
    └─LVMGroup-var--log  xxx:x     0  xxxxx   0  lvm   /var/log     # Logical Volume: persistent system logs
sr0                      xxx:x     1  xxxxx   0  rom                # Virtual CD-ROM drive (ISO)
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

## 2. Primary Partition
### 2.1 Select Primary Partition (`sda`)
[select-sda]

>[!NOTE]
>Now that we have created our primary partition, we can select it from the partition overview list (`pri/log`).

### 2.2 Create a New Partition (`sda1`)
[create-sda1-partition]

>[!TIP]
>`512 MB` is the ideal size because the `/boot` partition stores (1) the kernel(s), (2) initramfs images, and (3) the GRUB bootloader files. A typical Debian kernel + initramfs pair takes around `70–90 MB`. With multiple kernels installed (updates keep at least 2), you usually see (1) `~250–300 MB` used at most, and (2) leaving plenty of space for updates and recovery. `512 MB` comfortably avoids `/boot is full` errors during kernel upgrades.

>[!CAUTION]
>Don’t go below `200 MB`! This leads to frequent issues with kernel updates.

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
