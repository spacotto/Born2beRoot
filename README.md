>[!CAUTION]
>This is a work in progress.

# Overview
Born2beRoot is a system administration project that introduces the fundamentals of virtualisation and server configuration. The goal is to create and configure a [**Virtual Machine (VM)**](https://github.com/spacotto/Born2beRoot/blob/main/srcs/vm-overview.md) following strict security guidelines and best practices. This project aims to teach essential skills in operating system installation, partitioning, user management, security policies, and service configuration. 

>[!CAUTION]
>Since this project serves as an introduction to virtualisation, I will focus on installing the minimum of services. For this reason, **I will not provide sources concerning the graphical interface**.

## Requirements
### Host Operating System (Host OS)
- **OS:** Ubuntu
- **Version:** 22.04.4 LTS
- **Codename:** jammy

### Virtualisation Software ([**Hypervisor**](https://github.com/spacotto/Born2beRoot/blob/main/srcs/vm-hypervisor.md))
- **Software:** VirtualBox
- **Version:** 7.0.20

### Guest [Operating System](https://github.com/spacotto/Born2beRoot/blob/main/srcs/os-choice.md) (Guest OS)
- **OS:** Debian
- **Version:** 13.2.0 (amd64)
- **Codename:** trixie

# Features
>[!CAUTION]
>Keep in mind this documentation concerns the creation of a **minimalist** VM and server. I am going to discuss **exclusively** the implementation of the **essential elements**. I am NOT going to address the implementation of UI or other additional features.

- [Create a Virtual Machine](https://github.com/spacotto/Born2beRoot/blob/main/srcs/vm-creation.md)
- Debian Installation
  - [Configure Locals](https://github.com/spacotto/Born2beRoot/blob/main/srcs/debian-install-config-locals.md)
  - [Configure the Network](https://github.com/spacotto/Born2beRoot/blob/main/srcs/debian-install-config-network.md)
  - [Partition Disk](https://github.com/spacotto/Born2beRoot/blob/main/srcs/debian-install-disk-partitioning.md)

### Configure the package manager & Software Selection
>[!IMPORTANT]
>[Here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/debian-install-config-pckg.md) you can find the details concerning the package manager configuration and the software selection.

### Install the GRUB boot loader
>[!IMPORTANT]
>[Here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/debian-install-grub.md) you can find the details concerning the installation of GRUB boot loader.

## Server Features (Services, Packages, Utilities)
>[!CAUTION]
>Before starting to interact with your new VM terminal, I recommend checking what shell you are using. You can find this out by running the following command in the terminal:
>```
>echo $0
>```

### Package Manager: `apt` and `aptitude`
>[!IMPORTANT]
>[Here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/debian-ft-apt-aptitude.md) you can find the details concerning `apt` and `aptitude`.

### `sudo` Installation 
>[!IMPORTANT]
>[Here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/debian-ft-sudo.md) you can find the details concerning the setup of `sudo` command.

### AppArmor
>[!IMPORTANT]
>[Here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/debian-ft-apparmor.md) you can find the details concerning the setup of SSH.

### SSH
>[!IMPORTANT]
>[Here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/debian-ft-ssh.md) you can find the details concerning the setup of SSH.

### UFW
>[!IMPORTANT]
>[Here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/debian-ft-ufw.md) you can find the details concerning the setup of UFW.

### Strong Password Policy Implementation
>[!IMPORTANT]
>[Here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/debian-ft-password-policy-config.md) you can find the details concerning the implementation of the Strong Password Policy.

### Users & Groups Management
>[!IMPORTANT]
>[Here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/debian-ft-network.md) you can find the details concerning the setup of group management.

### Monitoring Script
>[!IMPORTANT]
>[Here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/debian-ft-monitoring-script.md) you can find the details concerning the setup of the Monitoring Script and Cron service.

### Website Hosting: WordPress, lighttpd, MariaDB, PHP, Fail2Ban
>[!IMPORTANT]
>[Here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/debian-ft-website-hosting.md) you can find the details concerning the setup of a website on a Debian server.
