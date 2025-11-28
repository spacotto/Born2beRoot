>[!CAUTION]
>This is a work in progress.

# About Born2beRoot
As part of my 42 journey, I am creating my first Virtual Machine (VM). Since this project does not produce source code or traditional archives to add to my portfolio, I have chosen to develop comprehensive documentation. This guide is intended to serve both as a personal reference and as a resource for others who are embarking on similar VM setup tasks, providing clear, step-by-step instructions and lessons learned throughout the process.

>[!CAUTION]
>Since this project serves as an introduction to virtualisation, I will focus on installing the minimum of services. For this reason, **I will not provide sources concerning the graphical interface**.

## VM Characteristics
### Hypervisor: VirtualBox
>[!NOTE]
>Find out more about hypervisors [here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/vm-hypervisor.md)

### Operating System (OS): Debian 13
>[!NOTE]
>Find out more about OS [here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/vm-hypervisor.md)

### Features
#### Installation
#### Partitioning

# Creating Your First Virtual Machine
>[!CAUTION]
>Remember that this is a guide to creating a **basic** VM. We're going to discuss the implementation of the essential, minimum elements. We will not address the implementation of UI or other additional features.

## Creating a New VM
Open VirtualBox > Click on `Machine` > Click on `New`
![step1](https://github.com/spacotto/Born2beRoot/blob/main/imgs/vm000.png)

Set up the name and OS

>[!IMPORTANT]
>You can download the [ISO](https://github.com/spacotto/Born2beRoot/blob/main/srcs/iso.md) [here](https://cdimage.debian.org/debian-cd/current/amd64/iso-dvd/). I used the `debian-13.2.0-amd64-DVD-1.iso`. If you don't have much space, I recommend downloading it into the `tmp` folder.

## Partitioning
