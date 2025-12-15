## Overview
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

## Features
>[!CAUTION]
>Keep in mind this documentation concerns the creation of a **minimalist** VM and server. I am going to discuss **exclusively** the implementation of the **essential elements**. I am NOT going to address the implementation of UI or other additional features.

- [Create a Virtual Machine](https://github.com/spacotto/Born2beRoot/blob/main/srcs/vm-creation.md)
- Debian Installation
  - [Configure Locals](https://github.com/spacotto/Born2beRoot/blob/main/srcs/debian-install-config-locals.md)
  - [Configure the Network](https://github.com/spacotto/Born2beRoot/blob/main/srcs/debian-install-config-network.md)
  - [Partition Disk](https://github.com/spacotto/Born2beRoot/blob/main/srcs/debian-install-disk-partitioning.md)
  - [Configure the package manager & Software Selection](https://github.com/spacotto/Born2beRoot/blob/main/srcs/debian-install-config-pckg.md)
  - [Install the GRUB boot loader](https://github.com/spacotto/Born2beRoot/blob/main/srcs/debian-install-grub.md)
- Server Features (Services, Packages, Utilities)
  - [Package Manager: `apt` and `aptitude`](https://github.com/spacotto/Born2beRoot/blob/main/srcs/debian-ft-apt-aptitude.md)
  - [`sudo` Installation](https://github.com/spacotto/Born2beRoot/blob/main/srcs/debian-ft-sudo.md)
  - [AppArmor](https://github.com/spacotto/Born2beRoot/blob/main/srcs/debian-ft-apparmor.md)
  - [SSH](https://github.com/spacotto/Born2beRoot/blob/main/srcs/debian-ft-ssh.md)
  - [UFW](https://github.com/spacotto/Born2beRoot/blob/main/srcs/debian-ft-ufw.md)
  - [Strong Password Policy Implementation](https://github.com/spacotto/Born2beRoot/blob/main/srcs/debian-ft-password-policy-config.md)
  - [Users & Groups Management](https://github.com/spacotto/Born2beRoot/blob/main/srcs/debian-ft-network.md)
  - [Monitoring Script](https://github.com/spacotto/Born2beRoot/blob/main/srcs/debian-ft-monitoring-script.md)
    - [Cron: Time-based job scheduling](https://github.com/spacotto/Born2beRoot/blob/main/srcs/debian-ft-cron.md)
  - [Website Hosting](https://github.com/spacotto/Born2beRoot/blob/main/srcs/debian-ft-website-hosting.md):
    - [WordPress: Content Management System (CMS)](https://github.com/spacotto/Born2beRoot/blob/main/srcs/website-wordpress.md)
    - [lighttpd: Web Server](https://github.com/spacotto/Born2beRoot/blob/main/srcs/website-lighttpd.md)
    - [MariaDB: Database Management System](https://github.com/spacotto/Born2beRoot/blob/main/srcs/website-mariadb.md)
    - [PHP: Scripting Language](https://github.com/spacotto/Born2beRoot/blob/main/srcs/website-php.md)
    - [Fail2Ban: Bonus Service](https://github.com/spacotto/Born2beRoot/blob/main/srcs/website-fail2ban.md)
