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
