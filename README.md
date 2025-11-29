>[!CAUTION]
>This is a work in progress.

# Born2beRoot: Project Overview
As part of my 42 journey, I am creating my first Virtual Machine (VM). Since this project does not produce source code or traditional archives to add to my portfolio, I have chosen to develop comprehensive documentation. This guide is intended to serve both as a personal reference and as a resource for others who are embarking on similar VM setup tasks, providing clear, step-by-step instructions and lessons learned throughout the process.

>[!CAUTION]
>Since this project serves as an introduction to virtualisation, I will focus on installing the minimum of services. For this reason, **I will not provide sources concerning the graphical interface**.

# Born2beRoot: Project Features
>[!IMPORTANT]
>[Here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/vm-overview.md) you can find more information on **virtualisation** and **VMs**.

>[!CAUTION]
>Keep in mind this documentation concerns the creation of a **minimalist** VM. I am going to discuss **exclusively** the implementation of the **essential elements**. I am NOT going to address the implementation of UI or other additional features.

## System Architecture
>[!IMPORTANT]
>[Here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/vm-installation.md) you can find the details concerning the installation of the OS through VirtualBox.

### Virtualisation Software (Hypervisor): VirtualBox
- **Software:** VirtualBox
- **Version:** 7.0.20

>[!NOTE]
>Find out more about hypervisors [here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/vm-hypervisor.md).

### Operating System (OS): Debian (Trixie)
- **OS:** Debian
- **Version:** 13.2.0 (amd64)

>[!NOTE]
>Find out more about OS [here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/vm-os.md).

## Storage Architecture
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
>[!IMPORTANT]
>[Here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/vm-storage-architecture.md) you can find the details concerning the disk (storage) partitioning process.

## Users Management
### sudo

## Services
### SSH
### Cron
