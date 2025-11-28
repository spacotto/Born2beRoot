>[!CAUTION]
>This is a work in progress.

# About Born2beRoot
As part of my 42 journey, I am creating my first Virtual Machine (VM). Since this project does not produce source code or traditional archives to add to my portfolio, I have chosen to develop comprehensive documentation. This guide is intended to serve both as a personal reference and as a resource for others who are embarking on similar VM setup tasks, providing clear, step-by-step instructions and lessons learned throughout the process.

>[!CAUTION]
>Since this project serves as an introduction to virtualisation, I will focus on installing the minimum of services. For this reason, **I will not provide a graphical interface**.

## What is Virtualisation?
**Virtualisation** is a technology that uses a software layer called a **hypervisor** to create **virtual versions of physical computing resources**, such as servers, storage, memory, and networks. This process **abstracts hardware components** like processors, memory, and storage, allowing them to be divided into multiple isolated Virtual Machines (VMs), each capable of running its own operating system and applications as if they were separate physical computers. The hypervisor acts as an **intermediary between the physical hardware and the virtual machines**, managing resource allocation and ensuring that **each VM operates independently without interfering with others**. This enables organisations to **maximise hardware utilisation**, **reduce costs**, **simplify IT management**, and **improve scalability and disaster recovery capabilities**.
 
## Benefits of Using Virtual Machines
Virtual machines (VMs) offer numerous benefits that make them a cornerstone of modern IT infrastructure. 

>[!NOTE]
>Find out more about the benefits of using VMs [here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/vm-benefits.md).

# Choosing Virtualisation Software
When choosing virtualisation software for your first VM, consider factors such as **compatibility with your OS**, **ease of use**, and **available documentation or community support** for beginners. Ensure the software is **actively maintained**, **supports the type of guest operating systems** you plan to use, and offers the **core features you need**, like snapshotting, resource management, and portability. **Cost** may also be important: many popular tools like VirtualBox are free and open-source, making them excellent starting points. Selecting user-friendly and reliable software will help simplify the learning process and avoid unnecessary technical issues.

## Overview of Popular Virtualisation Tools
Several widely used virtualisation tools make it easy to create and manage virtual machines. 
- **VirtualBox** is a free, open-source option that supports major operating systems and is great for beginners.
- **VMware Workstation Player** and **VMware Fusion** offer user-friendly interfaces and advanced features, popular among both personal and professional users.
- **UTM** is designed for Mac users seeking a simple virtualisation solution.
- For Linux, **KVM (Kernel-based Virtual Machine)** provides high efficiency and integration with the system.

These tools differ in terms of cost, platform support, and features, but all allow users to run multiple operating systems on a single physical machine.

## Why VirtualBox?
**VirtualBox** is an excellent choice for creating your **first VM** because it is **free**, **open-source**, and **works on all major operating systems**, including Windows, macOS, and Linux. Its **user-friendly interface** makes setup straightforward, even for those with no prior experience in virtualisation. VirtualBox also offers a wide range of **features**, supports **many guest operating systems**, and has an **active community** that provides helpful **documentation** and troubleshooting support.

>[!NOTE]
>Find out more about VirtualBox [here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/virtualbox-vs-utm.md).

# Choosing an Operating System (OS)
When selecting the OS for your VM, consider its **compatibility** with your **hardware** and **virtualisation software**, as well as the **ease of installation and use**. Look for systems that are **well-documented** and have **strong community support**, as this makes **troubleshooting** much easier for beginners. It's also important to think about your **goals**: choose an OS that aligns with what you want to learn or accomplish, whether it's getting comfortable with Linux, testing software, or developing projects. Opting for a **widely used, stable, and beginner-friendly OS** (such as Ubuntu or Debian) can make the entire process smoother and less overwhelming.

## What is a "Guest" Operating System?
A **Guest Operating System** (Guest OS) is **software installed within a VM that runs on a virtualised environment created by a host operating system**. It operates as a **secondary OS**, providing an **independent environment** for running applications, particularly those incompatible with the host OS. The guest OS **interacts with virtual hardware provided** by the hypervisor rather than the physical hardware directly, and it manages its own resources within the VM. **Multiple guest operating systems can run simultaneously** on a single physical machine, each isolated within its own VM, enabling the execution of diverse applications requiring different OS environments on the same hardware.

## Introduction to Debian 13 (Trixie)
Debian 13, codenamed "Trixie," is the **latest release** (November 2025) of the **Debian Linux OS**, known for its **stability**, **security**, and **reliability**. Like previous Debian versions, Trixie is a **free**, **open-source** OS that can be used on servers, desktops, and VMs. It features a **wide selection of software packages**, **robust community support**, and **regular security updates**, making it a popular choice for users seeking a dependable and well-documented Linux experience.

## Why Choose Debian Over Other Distributions?
I chose **Debian 13 (Trixie)** over Rocky Linux because, as a beginner, I wanted a system that is simple to set up, well-documented, and widely supported by the community. Debian is known for its stability and ease of use, making it ideal for learning the basics of Linux without being overwhelmed by complexity. 

Moreover, since **I'm not specifically interested in working with Red Hat Enterprise Linux (RHEL)** environments or their derivatives, Rocky Linux's enterprise focus didn't match my needs. Debian 13 lets me explore, learn, and customise my VM with confidence, while providing plenty of helpful resources for newcomers.

>[!NOTE]
>Find out more about Debian vs. Rocky Linux [here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/debian-vs-rocky.md).

# Creating Your First Virtual Machine
>[!CAUTION]
>Remember that this is a guide to creating a **basic** VM. We're going to discuss the implementation of the essential, minimum elements. We will not address the implementation of UI or other additional features.

## Creating a New VM
Open VirtualBox > Click on `Machine` > Click on `New`
![step1](https://github.com/spacotto/Born2beRoot/blob/main/imgs/vm000.png)

Set up the name and OS
![step2](https://github.com/spacotto/Born2beRoot/blob/main/imgs/vm001.png)

>[!IMPORTANT]
>You can download the [ISO](https://github.com/spacotto/Born2beRoot/blob/main/srcs/iso.md) [here](https://www.debian.org/distrib/netinst). I used the `amd64` version. If you don't have much space, I recommend downloading it into the `tmp` folder.

## Partitioning
