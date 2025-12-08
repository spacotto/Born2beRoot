>[!CAUTION]
>This is a work in progress.

# Born2beRoot
_This project has been created as part of the 42 curriculum by spacotto._

## Description
As part of my 42 journey, I am creating my first Server in a Virtual Machine (VM). Since this project does not produce source code or traditional archives, I shall provide comprehensive documentation.

>[!IMPORTANT]
>[Here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/vm-overview.md) you can find more information on **virtualisation** and **VMs**.

>[!CAUTION]
>Since this project serves as an introduction to virtualisation, I will focus on installing the minimum of services. For this reason, **I will not provide sources concerning the graphical interface**.

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

## Project description
### Debian vs Rocky Linux
-

### AppArmor vs SELinux
-

### UFW vs firewalld
-

### VirtualBox vs UTM
-

## Instructions
>[!CAUTION]
>Keep in mind this documentation concerns the creation of a **minimalist** VM and server. I am going to discuss **exclusively** the implementation of the **essential elements**. I am NOT going to address the implementation of UI or other additional features.

### Create a Virtual Machine
>[!IMPORTANT]
>[Here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/vm-creation.md) you can find the details concerning the VM creation.

### Debian Installation
#### Configure Locals
>[!IMPORTANT]
>[Here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/debian-install-config-locals.md) you can find the details concerning locals configuration.

#### Configure the Network
>[!IMPORTANT]
>[Here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/debian-install-config-network.md) you can find the details concerning the network configuration.

#### Partition Disk
>[!IMPORTANT]
>[Here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/debian-install-disk-partitioning.md) you can find the details concerning the disk (storage) partitioning process.

#### Configure the package manager & Software Selection
>[!IMPORTANT]
>[Here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/debian-install-config-pckg.md) you can find the details concerning the package manager configuration and the software selection.

#### Install the GRUB boot loader
>[!IMPORTANT]
>[Here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/debian-install-grub.md) you can find the details concerning the installation of GRUB boot loader.

### Server Features (Services, Packages, Utilities)
>[!CAUTION]
>Before starting to interact with your new VM terminal, I recommend checking what shell you are using. You can find this out by running the following command in the terminal:
>```
>echo $0
>```

#### Package Manager: `apt` and `aptitude`
>[!IMPORTANT]
>[Here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/debian-ft-apt-aptitude.md) you can find the details concerning `apt` and `aptitude`.

#### `sudo` Installation 
>[!IMPORTANT]
>[Here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/debian-ft-sudo.md) you can find the details concerning the setup of `sudo` command.

#### AppArmor
>[!IMPORTANT]
>[Here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/debian-ft-apparmor.md) you can find the details concerning the setup of SSH.

#### SSH
>[!IMPORTANT]
>[Here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/debian-ft-ssh.md) you can find the details concerning the setup of SSH.

#### UFW
>[!IMPORTANT]
>[Here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/debian-ft-ufw.md) you can find the details concerning the setup of UFW.

#### Strong Password Policy Implementation
>[!IMPORTANT]
>[Here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/debian-ft-password-policy-config.md) you can find the details concerning the implementation of the Strong Password Policy.

#### Users & Groups Management
>[!IMPORTANT]
>[Here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/debian-ft-network.md) you can find the details concerning the setup of group management.

#### Monitoring Script
>[!IMPORTANT]
>[Here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/debian-ft-monitoring-script.md) you can find the details concerning the setup of the Monitoring Script and Cron service.

#### Website Hosting: WordPress, lighttpd, MariaDB, PHP
>[!IMPORTANT]
>[Here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/debian-ft-website-hosting.md) you can find the details concerning the setup of a website on a Debian server.

## Resources
- [**Debian 13 (Trixie) Documentation**](https://www.debian.org/releases/trixie/release-notes/)
