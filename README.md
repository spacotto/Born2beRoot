>[!CAUTION]
>This is a work in progress.

>[!NOTE]
>As part of my 42 journey, I am creating my first Virtual Machine (VM). Since this project does not produce source code or traditional archives to add to my portfolio, I have chosen to provide comprehensive documentation. This documentation is intended to serve both as a personal reference and as a resource for others who are embarking on similar VM setup tasks, providing clear, step-by-step instructions and lessons learned throughout the process.

>[!CAUTION]
>Since this project serves as an introduction to virtualisation, I will focus on installing the minimum of services. For this reason, **I will not provide sources concerning the graphical interface**.

# Born2beRoot: Projects Tools
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

# Born2beRoot: Project Features
>[!IMPORTANT]
>[Here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/vm-overview.md) you can find more information on **virtualisation** and **VMs**.

>[!CAUTION]
>Keep in mind this documentation concerns the creation of a **minimalist** VM. I am going to discuss **exclusively** the implementation of the **essential elements**. I am NOT going to address the implementation of UI or other additional features.

## Create a Virtual Machine
>[!IMPORTANT]
>[Here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/ft-create-vm.md) you can find the details concerning the VM creation.

## OS Installation
### Configure Locals
>[!IMPORTANT]
>[Here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/ft-config-locals.md) you can find the details concerning locals configuration.

### Configure the Network
>[!IMPORTANT]
>[Here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/ft-config-network.md) you can find the details concerning the network configuration.

### Partition Disk
>[!IMPORTANT]
>[Here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/ft-disk-partitioning.md) you can find the details concerning the disk (storage) partitioning process.

### Configure the package manager & Software Selection
>[!IMPORTANT]
>[Here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/ft-config-pckg-mngr.md) you can find the details concerning the package manager configuration and the software selection.

### Install the GRUB boot loader
>[!IMPORTANT]
>[Here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/ft-grub.md) you can find the details concerning the installation of GRUB boot loader.

## Users Management
### `sudo`
>[!IMPORTANT]
>[Here]() you can find the details concerning the setup of `sudo` command.

### Groups
>[!IMPORTANT]
>[Here]() you can find the details concerning the setup of groups management.

### Password Policy
>[!IMPORTANT]
>[Here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/password-policy.md) you can find the details concerning the Strong Password Policy.

## Services
### UFW
>[!IMPORTANT]
>[Here]() you can find the details concerning the setup of UFW.

### SSH
>[!IMPORTANT]
>[Here]() you can find the details concerning the setup of SSH.

### Script Monitoring (Cron)
>[!IMPORTANT]
>[Here]() you can find the details concerning the setup of the Monitoring Script and Cron service.

## Hosting: WordPress
>[!IMPORTANT]
>[Here]() you can find the details concerning the setup of.
