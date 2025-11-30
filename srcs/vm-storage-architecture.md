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
└─sda5                   xxx:x     0  xxxxx   0  part               # Logical partition
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

## 1. Partition Disks (`sda`)
>[!NOTE]
>[Here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/vm-partitioning.md) you can find more details on what partitioning is.

### 1.1 Select Manual 
[select-manual]

>[!IMPORTANT]
>Since our goal is to set up a specific architecture, we shall select the `Manual` option.

### 1.2 Create New Partition Table (`sda`)
[create-new-partition-table]

>[!NOTE]
>Since we are at the beginning of the setup, we do not have partitions and mount points yet. Thus, we shall select `SCSI3 (0,0,0) (sda)` to start the partitioning process, which **represents the entire device**.

## 2. Primary Partition (`sda1`)
### 2.1 Select Select Partition Table (`sda`)
[select-sda]

>[!NOTE]
>Now that we have created our partition table, we can select `pri/log` from the disk partition overview.

### 2.2 Create a Primary Partition (`sda1`)
[create-sda1]

[allocate-sda1]

>[!TIP]
>`512 MB` is the ideal size because the `/boot` partition stores (1) the kernel(s), (2) initramfs images, and (3) the GRUB bootloader files. A typical Debian kernel + initramfs pair takes around `70–90 MB`. With multiple kernels installed (updates keep at least 2), you usually see (1) `~250–300 MB` used at most, and (2) leaving plenty of space for updates and recovery. `512 MB` comfortably avoids `/boot is full` errors during kernel upgrades.

>[!CAUTION]
>Don’t go below `200 MB`! This leads to frequent issues with kernel updates.

[select-type]

>[!NOTE]
>Select `Primary`. This is the partition where we want to install the OS (Debian).

[select-beginning]

>[!NOTE]
>The partition shall be created at the beginning of the disk as requested by the scheme we want to obtain.

[select-mount-point]

>[!NOTE]
>As previewed in the scheme, we shall select root (`/`) as the mount point.

[select-boot]

>[!NOTE]
>As previewed in the scheme, mount point shall be `/boot`.

[finish-setup]

>[!NOTE]
>Now that our primary partition is in place, we can conclude the setup.

## 3. Logical Partition (`sda5`)
### 3.1 Select Partition Table (`sda`)
[select-sda]

>[!NOTE]
>Once again, we shall select the partition table (`pri/log`) from the disk partition overview.

### 3.2 Create a Logical Partition (`sda5`)
[create-sda5]

[allocate-sda5]

>[!TIP]
>Make sda5 use **all disk space available** (aka `max`). This is because, since we have already configured `sda1`, this is the only partition left. Moreover, here is where we are going to add our **LVM** partitions, which are designed to manage flexible allocation. Hence, leaving unallocated disk space outside the LVM serves no purpose.

[select-type]

>[!NOTE]
>Select `Logical`. This is the partition where we want to set up the LVM.

[select-mount-point]

>[!NOTE]
>As previewed in the scheme, we shall select root (`/`) as the mount point. `sda5` needs to be at the same level as `sda1`.

[select-nothing]

>[!NOTE]
>But we are not going to mount it yet.

[finish-setup]

>[!NOTE]
>Now that our logical partition is in place, we can conclude the setup.

## 4. Configure Encrypted Volumes

[configure-encrypted-volumes]

[confirm]

[created-encrypted-volumes]

[/dev/sda5]

[finish-setup]

## 5. Configure Logical Volume Manager (LVM)
>[!NOTE]
>[Here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/vm-lvm.md) you can find more information concerning the Logical Volume Manager (LVM).

[configure-lvm]

### 5.1 LVMGroup
[create-volume-group]

[enter-LVMGroup]

[/dev/mapper/sda5_crypt]

### 5.2 LVM root
[create-logical-volume]

[select-LVMGroup]

[enter-root]

[allocate-root]

>[!TIP]
>`4GB` should be large enough to hold (1) the base OS, (2) the installed packages, and (3) the system files in `/` (binaries, configs, libraries). The minimum should be around `3GB`: Debian minimal install (`~500–700 MB`) plus package updates & extra utilities (`~2GB`). `4GB` allows more packages without worrying and leaves plenty of space for the other LVM.

### LVM swap

### LVM home

### LVM var

### LVM srv

### LVM tmp

### LVM var--log

## Final Result (`lsblk`)
