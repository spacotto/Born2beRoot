# Virtual Machines (VMs): An Overview

## What is Virtualisation?
**Virtualisation** is a technology that allows you to **create multiple simulated environments or dedicated resources from a single physical hardware system**. At its core, virtualisation uses software to create an abstraction layer over physical hardware, enabling you to run multiple operating systems and applications simultaneously on the same physical machine. Think of it like dividing a large office building into separate units: while there's only one physical building with one foundation, electrical system, and structure, you can divide it into multiple independent offices, each functioning as if it were its own separate space. Similarly, virtualisation takes one physical computer and divides its resources (processor, memory, storage, and network) into multiple isolated virtual environments.

The key innovation of virtualisation is the **separation of the operating system and applications from the underlying physical hardware**. This separation is managed by a special layer of software called a **hypervisor** (or virtual machine monitor), which sits between the physical hardware and the virtual machines. The hypervisor allocates and manages the physical resources, distributing them among the various virtual machines as needed.

## About Virtual Machines (VMs)
A **Virtual Machine (VM)** is the **virtualisation or emulation of a computer system**. It's a software-based computer that runs inside your physical computer. 

Each VM includes its own **virtual hardware** (CPU, memory, hard drive, network interface) and runs a **complete operating system (OS)**, which can be different from the host operating system running on the physical machine. When you run a VM, it behaves like a completely independent computer. You can install software, save files, connect to networks, and perform virtually any task you could on a physical machine. The VM is isolated from the host system and other VMs, meaning that if something goes wrong in one VM (like a virus infection or system crash), it doesn't affect the host or other virtual machines.

## Application
Organisations use VMs extensively in data centres to run multiple server applications on shared hardware infrastructure. Cloud computing providers like AWS, Azure, and Google Cloud build their services on massive VM infrastructures, allowing customers to spin up virtual servers on demand.

Software developers rely on VMs to create consistent development and testing environments, ensuring that code works across different operating systems and configurations. 

IT professionals use VMs for training and education, creating safe sandbox environments where students can practice without risking production systems.

Individuals may use VMs to run legacy applications that require older operating systems, to test software before installing it on their primary system, or to maintain privacy by isolating specific activities within a VM.

## Benefits
**Resource efficiency and cost reduction.** Instead of running multiple physical servers that each use only a fraction of their capacity, you can consolidate many VMs onto fewer physical machines, maximising hardware utilisation and reducing costs for electricity, cooling, and physical space.

**Isolation and security.** Because each VM is completely separated from the others, you can safely test new software, run potentially risky applications, or experiment with different configurations without endangering your main system. This makes VMs ideal for software development, testing, and cybersecurity research.

**Flexibility and compatibility.** You can easily create, clone, move, or delete VMs, and you can run different operating systems side by side. A developer might run Windows on their physical machine while using Linux VMs for server development and a macOS VM for testing cross-platform compatibility.

**Simplified disaster recovery and business continuity.** You can take snapshots of a VM's entire state at any moment, creating a backup that captures not just the data but the complete system configuration. If something goes wrong, you can restore the VM to its previous state in minutes. VMs can also be migrated between physical hosts with minimal downtime, making maintenance and upgrades much easier.

## Limitations
**Performance overhead.** The hypervisor adds an extra layer between the hardware and the applications, creating a performance penalty. While modern virtualisation technology is highly efficient, VMs typically can't achieve 100% of bare-metal performance, particularly for graphics-intensive applications or tasks requiring direct hardware access.

**Significant resource consumption.** Each VM requires its own allocation of memory, storage, and processing power, and running the full guest operating system creates overhead. If you overload a physical host with too many VMs, performance can degrade substantially.
