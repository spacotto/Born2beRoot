# About Creating a Virtual Machine (VM)
Text

## 1. Creating a New VM
```
Open VirtualBox
Click on [ Machine ]
Click on [   New   ]
```
![create-the-vm](https://github.com/spacotto/Born2beRoot/blob/main/imgs/vm000.png)

## 2. Configure VM name and OS
```
VM Name    # The name you want to use for your VM (like a file name).
VM Folder  # The folder path where your VM is going to be placed.
ISO Image  # The ISO image of the OS.
```
![vm-name-and-os](https://github.com/spacotto/Born2beRoot/blob/main/imgs/vm001.png)

>[!WARNING]
>When choosing the `VM Folder`, make sure to have enough space to store your VM!

>[!CAUTION]
>Since we want to set up the VM ourselves, we need to **CHECK "Skip Unattended Installation."** In other VirtualBox versions, the default changed from opt-in to opt-out. In the opt-out instance, you shall **UNCHECK "Proceed with Unattended Installation."**

## 3 Configure Virtual Hardware
>[!IMPORTANT]
>[Here](https://www.debian.org/releases/forky/s390x/ch03s04.en.html) you can find the **Minimum Hardware Requirements** for Debian. 

>[!WARNING]
>Since we are using a VM, **we do not care about allocating resources following the power-of-2 alignment**. Virtualisation is hardware abstraction. In other words, the physical hardware cares about proper binary alignment, the virtualised one does not.

![vm-hardware-ram-cpu](https://github.com/spacotto/Born2beRoot/blob/main/imgs/vm002.png)

![vm-hardware-disk](https://github.com/spacotto/Born2beRoot/blob/main/imgs/vm003.png)

### RAM
>[!TIP]
>I have allocated `4GB` to provide plenty of extra space: it is more than the minimum, and **compatible with the specs of my host machine**.

>[!CAUTION]
>Given the RAM minimum requirements (`512MB`), the recommended RAM (`1GB`), to which we need to add the space for the services (around `1GB`), the **recommended total minimum** is `2GB`. Do not go less than that!

### CPUs
>[!TIP]
>A minimal Debian server with no GUI, no heavy apps, and only basic services runs perfectly **on a single virtual CPU**. I have allocated **2 for extra responsiveness**.

>[!CAUTION]
>More than 2 CPUs isn’t useful for this project. And remember: **never allocate 100% of your host’s cores!**

### Disk Size
>[!TIP]
>The minimum recommended size is `10GB`. `20GB` is the optimal, balanced choice. Allocate `30GB` if you never want to think about disk space.

>[!IMPORTANT]
>VirtualBox and QEMU use **dynamic virtual disks**. In other words, A `20GB` virtual disk does not reserve `20GB` physically. Instead, it **expands gradually as data is written**.

## 4. Summary
![hardware-summary](https://github.com/spacotto/Born2beRoot/blob/main/imgs/vm004.png)
### 1.4 Confirm the Summary
[vm-specs-summary]
