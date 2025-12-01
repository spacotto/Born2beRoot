# About Disk Partitioning
This is the third step of the OS installation process. In this instance, our goal is to obtain a specific partition scheme.

**Desired Disk Partitioning Scheme:**
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
>[!NOTE]
>[Here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/vm-partitioning.md) you can find more details on what partitioning is.

## 1. Create New Partition Table (`sda`)
>[!IMPORTANT]
>Since our goal is to set up a specific architecture, we shall select the `Manual` option.

![select-manual](https://github.com/spacotto/Born2beRoot/blob/main/imgs/vm016.png)

>[!NOTE]
>Since we are at the beginning of the setup, we do not have partitions and mount points yet. Thus, we shall select `SCSI3 (0,0,0) (sda)` to start the partitioning process, which **represents the entire device**.

![create-new-partition-table](https://github.com/spacotto/Born2beRoot/blob/main/imgs/vm017.png)

## 2. Create Primary Partition (`sda1`)
>[!NOTE]
>Now that we have created our partition table, we can select `pri/log` from the disk partition overview and create the primary partition.

![select-sda](https://github.com/spacotto/Born2beRoot/blob/main/imgs/vm018.png)

![create-sda1](https://github.com/spacotto/Born2beRoot/blob/main/imgs/vm019.png)

>[!TIP]
>`512 MB` is the ideal size because the `/boot` partition stores (1) the kernel(s), (2) initramfs images, and (3) the GRUB bootloader files. A typical Debian kernel + initramfs pair takes around `70–90 MB`. With multiple kernels installed (updates keep at least 2), you usually see (1) `~250–300 MB` used at most, and (2) leaving plenty of space for updates and recovery. `512 MB` comfortably avoids `/boot is full` errors during kernel upgrades.

>[!CAUTION]
>Don’t go below `200 MB`! This leads to frequent issues with kernel updates.

![allocate-sda1](https://github.com/spacotto/Born2beRoot/blob/main/imgs/vm020.png)

>[!NOTE]
>Select `Primary`. This is the partition where we want to install the OS (Debian).

![select-type](https://github.com/spacotto/Born2beRoot/blob/main/imgs/vm021.png)

>[!NOTE]
>The partition shall be created at the beginning of the disk as requested by the scheme we want to obtain.

![select-beginning](https://github.com/spacotto/Born2beRoot/blob/main/imgs/vm022.png)

>[!NOTE]
>As previewed in the scheme, we shall select root (`/`) as the mount point.

![select-mount-point](https://github.com/spacotto/Born2beRoot/blob/main/imgs/vm023.png)

>[!NOTE]
>As previewed in the scheme, mount point shall be `/boot`.

![select-boot](https://github.com/spacotto/Born2beRoot/blob/main/imgs/vm024.png)

>[!NOTE]
>Now that our primary partition is in place, we can finish the setup.

![finish-setup](https://github.com/spacotto/Born2beRoot/blob/main/imgs/vm025.png)

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

### 5.2 `root`
[create-logical-volume]

[select-LVMGroup]

[enter-name]

[allocate-space]

>[!TIP]
>`4GB` should be large enough to hold (1) the base OS, (2) the installed packages, and (3) the system files in `/` (binaries, configs, libraries). The minimum should be around `3GB`: Debian minimal install (`~500–700 MB`) plus package updates & extra utilities (`~2GB`). `4GB` allows more packages without worrying and leaves plenty of space for the other LVM.

### 5.3 `swap`

[create-logical-volume]

[select-LVMGroup]

[enter-name]

[allocate-space]

>[!TIP]
>`/swap` exists to extend memory safely. In minimal VMs (like this one), allocate around `2GB`. More swap is not harmful, but rarely necessary. Hibernation is the only reason to make swap larger than RAM.

### 5.4 `home`

[create-logical-volume]

[select-LVMGroup]

[enter-name]

[allocate-space]

>[!TIP]
>`/home` stores user data. Thus, the size depends on the expected files and the number of users. For our purposes (testing 1 user), `4GB` is sufficient.

### 5.5 `var`

[create-logical-volume]

[select-LVMGroup]

[enter-name]

[allocate-space]

>[!TIP]
>`/var` stores variable system data. Thus, its size depends on logs, caches, spools, and service files. For a small VM with minimal services, `2GB` is enough.

### 5.6 `srv`

[create-logical-volume]

[select-LVMGroup]

[enter-name]

[allocate-space]

>[!TIP]
>`/srv` stores service-specific data. Thus, in this instance, a small allocation (`2GB`) is enough. Anyway, LVM allows resizing later if needed.

### 5.7 `tmp`

[create-logical-volume]

[select-LVMGroup]

[enter-name]

[allocate-space]

>[!TIP]
>`/tmp` holds temporary files for the OS and applications. Thus, once again, a small allocation (`1GB`) is enough.

### 5.8 `var--log`

[create-logical-volume]

[select-LVMGroup]

[enter-name]

[allocate-space]

>[!TIP]
>`/var/log` stores persistent system/service logs. Thus, `1GB` should be enough. It is better to allocate it separately to prevent log growth from breaking other partitions.

## 6. Mount point

### 6.1 `home`
[select-partition]
[use-as-do-not-use]
[ext4-journaling-file-system]
[mount-point-none]
[select-mount-point]
[finish-setup]

### 6.2 `root`
[select-partition]
[use-as-do-not-use]
[ext4-journaling-file-system]
[mount-point-none]
[select-mount-point]
[finish-setup]

### 6.3 `srv`
[select-partition]
[use-as-do-not-use]
[ext4-journaling-file-system]
[mount-point-none]
[select-mount-point]
[finish-setup]

### 6.4 `swap`
[select-partition]
[use-as-do-not-use]
[swap-area]
[finish-setup]

### 6.5 `tmp`
[select-partition]
[use-as-do-not-use]
[ext4-journaling-file-system]
[mount-point-none]
[select-mount-point]
[finish-setup]### 6.6 `var`
[select-partition]
[use-as-do-not-use]
[ext4-journaling-file-system]
[mount-point-none]
[select-mount-point]
[finish-setup]

### 6.6 `var`
[select-partition]
[use-as-do-not-use]
[ext4-journaling-file-system]
[mount-point-none]
[select-mount-point]
[finish-setup]

### 6.7 `var-log`
[select-partition]
[use-as-do-not-use]
[ext4-journaling-file-system]
[mount-point-none]
[enter-manually]
[enter-/var/log]
[finish-setup]

## 7. Final Result (`lsblk`)
```
# lsblk
NAME                     MAJ:MIN  RM   SIZE  RO  TYPE  MOUNTPOINTS
sda                        8:0     0    20G   0  disk               
├─sda1                     8:1     0   487M   0  part  /boot        
├─sda2                     8:2     0     1K   0  part               
└─sda5                   254:0     0  19.5G   0  part               
  └─sda5_crypt           254:1     0  19.5G   0  crypt              
    ├─LVMGroup-root      254:2     0   3.7G   0  lvm   /            
    ├─LVMGroup-swap      254:3     0   1.9G   0  lvm   [SWAP]       
    ├─LVMGroup-home      254:4     0   3.7G   0  lvm   /home        
    ├─LVMGroup-var       254:5     0   1.9G   0  lvm   /var         
    ├─LVMGroup-srv       254:6     0   1.9G   0  lvm   /srv         
    ├─LVMGroup-tmp       254:7     0   952M   0  lvm   /tmp         
    └─LVMGroup-var--log  254:8     0   952M   0  lvm   /var/log     
sr0                       11:0     1  1024M   0  rom                
```
