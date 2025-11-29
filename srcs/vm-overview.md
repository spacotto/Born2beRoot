# Virtual Machines (VMs): An Overview

## What is Virtualisation?
**Virtualisation** is a technology that allows you to **create multiple simulated environments or dedicated resources from a single physical hardware system**. At its core, virtualisation uses software to create an abstraction layer over physical hardware, enabling you to run multiple operating systems and applications simultaneously on the same physical machine. Think of it like dividing a large office building into separate units: while there's only one physical building with one foundation, electrical system, and structure, you can divide it into multiple independent offices, each functioning as if it were its own separate space. Similarly, virtualisation takes one physical computer and divides its resources (processor, memory, storage, and network) into multiple isolated virtual environments.

The key innovation of virtualisation is the **separation of the operating system and applications from the underlying physical hardware**. This separation is managed by a special layer of software called a **hypervisor** (or virtual machine monitor), which sits between the physical hardware and the virtual machines. The hypervisor allocates and manages the physical resources, distributing them among the various virtual machines as needed.

## What is a Virtual Machine (VM)?
A **Virtual Machine (VM)** is the **virtualisation or emulation of a computer system**. It's a software-based computer that runs inside your physical computer. 

Each VM includes its own **virtual hardware** (CPU, memory, hard drive, network interface) and runs a **complete operating system (OS)**, which can be different from the host OS running on the physical machine. When you run a VM, it behaves like a completely independent computer. You can install software, save files, connect to networks, and perform virtually any task you could on a physical machine. The VM is isolated from the host system and other VMs, meaning that if something goes wrong in one VM (like a virus infection or system crash), it doesn't affect the host or other virtual machines.

## Purpose
A VM's purpose is to let you **run an isolated OS without affecting your main one**. This makes it ideal for experimenting, testing, learning, and running services safely. VMs also improve portability and reproducibility, because you can create, configure, or delete them without changing your actual machine. In short, a VM provides a controlled, flexible, and secure space to work on systems or projects without risk.

## Application
Organisations use VMs extensively in data centres to run multiple server applications on shared hardware infrastructure. Cloud computing providers like AWS, Azure, and Google Cloud build their services on massive VM infrastructures, allowing customers to spin up virtual servers on demand.

Software developers rely on VMs to create consistent development and testing environments, ensuring that code works across different operating systems and configurations. 

IT professionals use VMs for training and education, creating safe sandbox environments where students can practice without risking production systems.

Individuals may use VMs to run legacy applications that require older operating systems, to test software before installing it on their primary system, or to maintain privacy by isolating specific activities within a VM.

## Pros & Cons of Using Virtual Machines
### Pros 
- **Resource efficiency & cost reduction.** Multiple VMs can run on a single physical machine, maximising hardware usage.
- **Isolation & security.** Each VM is separated from others, reducing the impact of system failures or security breaches.
- **Flexibility & compatibility** Run different operating systems, test configurations, or replicate environments easily.
- **Simplified disaster recovery & business continuity** — VMs can be snapshotted, cloned, and restored quickly. 

### Cons 
- **Performance overhead.** VMs are slower than bare metal because resources are shared and virtualised.
- **Higher resource demands.** Each VM needs its own OS, which consumes CPU, RAM, and storage.
- **Possible hardware limitations** — Host systems with limited resources may struggle to support multiple VMs.
- **Complexity at scale** — Managing many VMs can require additional tools and expertise (e.g., hypervisor management).

### Summary Table
| 👍 Pros               | 👎 Cons              |
| :-------------------- | :------------------- |
| Cost reduction        | Performance overhead |
| Security              | Resource demands     |
| Flexibility           | hardware limitations |
| Recovery & Continuity | Complexity at scale  |
