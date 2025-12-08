>[!CAUTION]
>This is a work in progress.

_This project has been created as part of the 42 curriculum by spacotto._

# Description
Born2beRoot is a system administration project that introduces the fundamentals of virtualisation and server configuration. The goal is to create and configure a Virtual Machine (VM) following strict security guidelines and best practices. 

This aims to teach essential skills in operating system installation, partitioning, user management, security policies, and service configuration. 

>[!CAUTION]
>Since this project serves as an introduction to virtualisation, I will focus on installing the minimum of services. For this reason, **I will not provide sources concerning the graphical interface**.

>[!NOTE]
>[Here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/vm-overview.md) you can find more information on **virtualisation** and **VMs**.

# Project description
## My Choices
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

## Debian vs Rocky Linux
| Aspect             | Debian                                               | Rocky Linux                                          |
| :----------------- | :--------------------------------------------------- | :--------------------------------------------------- |
| Stability          | Highly stable, focuses on thoroughly tested packages | Enterprise-grade stability, RHEL binary compatible   |
| Documentation      | Extensive, beginner-friendly resources               | Strong enterprise documentation, RedHat-based guides |
| Package Management | APT – intuitive and widely used                      | DNF/YUM – powerful but less familiar to beginners    |
| Package Repository | Massive repository, wide software availability       | Smaller but curated for enterprise use               |
| Learning Curve     | Gentle, great for beginners                          | Steeper, more enterprise-focused                     |
| Update Cycle       | Packages may be older (stability focus)              | Conservative updates with enterprise focus           |
| Use Case           | General purpose, education, servers                  | Enterprise production environments                   |
| Community          | Large, diverse community                             | Growing community, backed by enterprise users        |

### Why Debian
I chose Debian 13 (Trixie) over Rocky Linux because, as a beginner, I wanted a system that is simple to set up, well-documented, and widely supported by the community. Debian is known for its stability and ease of use, making it ideal for learning the basics of Linux without being overwhelmed by complexity. Moreover, since I'm not specifically interested in working with Red Hat Enterprise Linux (RHEL) environments or their derivatives, Rocky Linux's enterprise focus didn't match my needs. Debian 13 lets me explore, learn, and customise my VM with confidence, while providing plenty of helpful resources for newcomers.

>[!NOTE]
>Find out more about my OS choice [here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/os-choice.md).

## AppArmor vs SELinux
| Aspect              | AppArmor                                         | SELinux                                                |
| :------------------ | :----------------------------------------------- | :----------------------------------------------------- |
| Complexity          | Simple to configure and understand               | Complex policy language, steep learning curve          |
| Security Model      | Path-based (uses file paths)                     | Label-based (uses security contexts)                   |
| Default On          | Debian and Ubuntu                                | Rocky, RHEL, Fedora                                    |
| Granularity         | Less granular control                            | Highly granular, comprehensive security                |
| Learning Curve      | Gentle, beginner-friendly                        | Steep, requires significant learning                   |
| Troubleshooting     | Easier to debug and fix issues                   | Difficult to troubleshoot, cryptic errors              |
| Security Robustness | Can be bypassed with hardlinks/symlinks          | More robust, label-based system                        |
| Industry Use        | Common in Debian-based systems                   | Industry standard in enterprise environments           |
| Profile Creation    | More intuitive, human-readable                   | Requires understanding of policy language              |

## UFW vs firewalld
| Aspect              | UFW (Uncomplicated Firewall)                     | firewalld                                              |
| :------------------ | :----------------------------------------------- | :----------------------------------------------------- |
| Full Name           | Uncomplicated Firewall                           | FirewallD                                              |
| Complexity          | Simple, straightforward syntax                   | More complex, feature-rich                             |
| Learning Curve      | Very easy, beginner-friendly                     | Moderate, requires understanding zones                 |
| Default On          | Debian and Ubuntu                                | Rocky, RHEL, Fedora                                    |
| Configuration       | Command-line with simple syntax                  | Zone-based configuration system                        |
| Dynamic Management  | Static rules (requires reload)                   | Dynamic, no restart needed for changes                 |
| Use Case            | Simple firewall needs, basic servers             | Complex networking, multiple interfaces                |
| Zones Concept       | No zone support                                  | Supports multiple trust zones                          |
| Features            | Basic but sufficient for most cases              | Advanced features for complex setups                   |
| Interface           | CLI only (simple commands)                       | CLI and GUI tools available                            |

## VirtualBox vs UTM
| Aspect              | VirtualBox                                       | UTM                                                    |
| :------------------ | :----------------------------------------------- | :----------------------------------------------------- |
| Platform Support    | Windows, Linux, Intel Mac                        | macOS (especially Apple Silicon)                       |
| Apple Silicon       | Not supported                                    | Native support, optimized performance                  |
| Maturity            | Highly mature, industry standard                 | Relatively new, growing ecosystem                      |
| Cost                | Free and open-source                             | Free and open-source                                   |
| Performance         | Excellent on supported platforms                 | Excellent on Apple Silicon, uses QEMU                  |
| Features            | Extensive (snapshots, shared folders, etc.)      | Growing feature set, simpler interface                 |
| Documentation       | Extensive, decades of resources                  | Less documentation, smaller community                  |
| Ease of Use         | User-friendly GUI, well-established              | Clean modern interface, intuitive                      |
| Snapshots           | Robust snapshot system                           | Supports snapshots                                     |
| Community           | Very large, widespread adoption                  | Smaller but growing                                    |
| Resource Usage      | Can be resource-intensive                        | Lightweight, efficient on M-series chips               |

# Instructions
>[!CAUTION]
>Keep in mind this documentation concerns the creation of a **minimalist** VM and server. I am going to discuss **exclusively** the implementation of the **essential elements**. I am NOT going to address the implementation of UI or other additional features.

## Create a Virtual Machine
>[!IMPORTANT]
>[Here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/vm-creation.md) you can find the details concerning the VM creation.

## Debian Installation
### Configure Locals
>[!IMPORTANT]
>[Here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/debian-install-config-locals.md) you can find the details concerning locals configuration.

### Configure the Network
>[!IMPORTANT]
>[Here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/debian-install-config-network.md) you can find the details concerning the network configuration.

### Partition Disk
>[!IMPORTANT]
>[Here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/debian-install-disk-partitioning.md) you can find the details concerning the disk (storage) partitioning process.

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

### Website Hosting: WordPress, lighttpd, MariaDB, PHP
>[!IMPORTANT]
>[Here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/debian-ft-website-hosting.md) you can find the details concerning the setup of a website on a Debian server.

## Resources
- [**Debian 13 (Trixie) Documentation**](https://www.debian.org/releases/trixie/release-notes/)
