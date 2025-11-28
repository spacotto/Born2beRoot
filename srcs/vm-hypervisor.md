# About Virtualisation Software (Hypervisor)
Virtualisation has revolutionised modern computing by enabling multiple operating systems to run simultaneously on a single physical machine. At the heart of this technology lies the hypervisor, a critical piece of software that enables virtualisation. 

## What is a Hypervisor?
A **hypervisor**, also known as a **Virtual Machine Monitor (VMM)**, is specialised **software that creates and manages VMs by abstracting the physical hardware resources of a host computer**. It acts as an **intermediary layer** between the physical hardware and the virtual machines, allowing multiple guest operating systems to **share the same physical resources** such as CPU, memory, storage, and network interfaces.

Hypervisors operate by creating **isolated virtual environments**, each with its own virtual hardware configuration. This isolation ensures that processes running in one VM cannot interfere with those in another, providing security and stability. The hypervisor is responsible for allocating physical resources to each VM, scheduling CPU time, managing memory allocation, and handling input/output operations.

There are two primary types of hypervisors. 
1. **Type 1** hypervisors, often called **bare-metal hypervisors**, run **directly on the host's hardware** without requiring an underlying operating system. Examples include VMware ESXi, Microsoft Hyper-V, and Xen. These are typically used in **enterprise environments** and **data centres** due to their superior **performance and efficiency**.
2. **Type 2** hypervisors, conversely, run as **applications on top of a conventional operating system**. VirtualBox, VMware Workstation, and Parallels Desktop fall into this category. While they may have slightly **lower performance** compared to Type 1 hypervisors, they offer **greater flexibility and ease of use**, particularly for development, testing, and educational purposes.

## Popular Virtualisation Tools
- **VMware Workstation Pro.** One of the most feature-rich Type 2 virtualisation platforms available, offering advanced networking capabilities, comprehensive snapshot management, and excellent performance. Part of VMware's extensive ecosystem, including enterprise-grade solutions, makes skills transferable across professional environments. Requires a paid license for full functionality, which can be prohibitive for individual users and educational institutions.

- **Microsoft Hyper-V.** Integrated with Windows Pro, Enterprise, and Education editions, providing readily accessible virtualisation for Windows users. Offers native Windows integration, strong performance characteristics, and supports both Type 1 and Type 2 deployment models. Primary limitations include its Windows-centric approach and requirement for specific Windows editions, excluding users of Home versions or other operating systems.

- **KVM (Kernel-based Virtual Machine).** Transforms the Linux kernel into a Type 1 hypervisor, offering near-native performance on Linux systems. An open-source solution widely used in cloud infrastructure, including major providers like Google Cloud. The command-line interface and Linux-focused nature present a steeper learning curve for users unfamiliar with Linux environments.

- **VirtualBox.** Developed by Oracle as a free, open-source Type 2 hypervisor supporting Windows, macOS, Linux, and Solaris as host operating systems. Demonstrates remarkable cross-platform compatibility with an intuitive graphical interface while maintaining powerful features, including snapshots, shared folders, seamless mode, and extensive guest operating system support. Represents a compelling middle ground between accessibility and functionality.

# VirtualBox (and UTM)

## About VirtualBox
### What VirtualBox is
**VirtualBox** is a free, open-source virtualisation program that lets you run entire operating systems inside your current operating system. Think of it as a computer inside your computer.

### What it does
VirtualBox lets you create virtual machines (VMs). A VM behaves like a real computer, with:
- virtual CPU
- virtual RAM
- virtual disk
- virtual network

Inside that VM, without affecting your main system, you can install:
- Debian
- Rocky Linux
- Windows
- macOS (with restrictions)
- other OS

### What people use VirtualBox for
- Testing operating systems safely
- Learning Linux without touching the real machine
- Running older software
- Isolating risky apps
- Hosting small lab environments
- Trying server setups before doing them on real hardware

### Why it’s relevant to the project
If you want to practice setting up Debian or Rocky before touching your real server, VirtualBox is perfect. You can:
- Install Debian in a VM
- Practice configuring Nginx, SSH, and firewalls
- Break things and reinstall quickly
- Get confident before deploying the real server

## About UTM
### What UTM is
UTM is a **virtual machine manager** that lets you run operating systems inside your Mac. It uses **QEMU** under the hood, wrapped in a simple and friendly interface.

### Why UTM is offered as an alternative
If you're on a company Mac (especially Apple Silicon), your IT environment may block:
- kernel extensions
- hypervisor frameworks
- or security settings needed by VirtualBox

UTM, using Apple’s built-in virtualisation framework, doesn’t require kernel-level hacks, so it works in restricted environments.

## VirtualBox vs UTM
| Feature                    | VirtualBox        | UTM                                        |
| -------------------------- | ----------------- | ------------------------------------------ |
| Supported on Apple Silicon | ❌ No             | ✅ Yes                                     |
| Apple Intel support        | ✅ Yes            | ⚠️ Yes (slower)                            |
| Performance                | Good              | Good on Apple Silicon (via virtualisation) |
| Underlying tech            | VirtualBox engine | QEMU                                       |
| Ease of use                | Easy              | Easy                                       |
| Cost                       | Free              | Free                                       |

