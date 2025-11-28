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

## Why VirtualBox is the Best Choice for Academic Projects
When embarking on an academic project to create a first VM, several factors must be considered, including **cost**, **ease of use**, **documentation availability**, and **resource requirements**. VirtualBox excels in each of these areas, making it the optimal choice for students and educators.

**Accessible Cost.** VirtualBox is completely **free and open-source** under the GNU General Public License. This eliminates financial barriers that might prevent students from experimenting with virtualisation technology at home. Unlike commercial alternatives that require expensive licenses or limited trial periods, VirtualBox can be freely installed on personal computers, university lab machines, or any compatible device without licensing concerns.

**Accessible User Interface (UI).** VirtualBox UI prioritises **simplicity without sacrificing functionality**. The VM creation wizard guides users through the process step by step, asking intuitive questions about the intended guest operating system, memory allocation, and storage configuration. This guided approach reduces the likelihood of configuration errors that could frustrate beginners. The main window presents all VMs in a clear list format with easily accessible controls for starting, pausing, and managing VMs.

**Appropriate complexity.** For academic purposes where the goal is to understand fundamental virtualisation concepts rather than to deploy production infrastructure, VirtualBox provides precisely the right level of complexity. Students can focus on essential concepts such as **resource allocation**, **OS installation**, and **basic VM management** without being overwhelmed by enterprise-level features they won't immediately need.

**Vast Documentation & Support.** The **documentation** and **community support** surrounding VirtualBox are of great value. Oracle maintains comprehensive official documentation covering installation, configuration, and troubleshooting. Beyond official sources, VirtualBox's popularity has generated an enormous repository of tutorials, video guides, forum discussions, and blog posts addressing virtually every conceivable use case and problem. When students encounter difficulties, they can typically find solutions quickly through a simple web search.

**Cross-Platform Consistency.** VirtualBox's **cross-platform** nature ensures that all students can participate regardless of their host OS. Whether using Windows, macOS, or Linux, the VirtualBox interface and functionality remain consistent. This uniformity is invaluable in academic settings where students may use different personal computers but need to complete identical assignments. Instructors can provide universal guidance without needing to account for platform-specific variations.

**Accessible Requirements.** Academic projects typically focus on basic VMs running lightweight OS or Linux distributions. VirtualBox handles these scenarios efficiently, running comfortably on modest hardware. Students don't require high-end computers to create functional VMs, democratising access to virtualisation education.

**Snapshots.** The snapshot feature in VirtualBox proves particularly valuable for learning environments. Students can create snapshots before making system changes, conducting experiments, or installing software. If something goes wrong, they can instantly revert to a previous state without losing hours of work or needing to rebuild the entire VM from scratch. This safety net encourages experimentation and risk-taking, essential components of effective learning.

From a pedagogical perspective, VirtualBox aligns well with progressive learning objectives. Students begin with basic VM creation, then progressively explore more advanced topics such as networking configurations, storage management, cloning, and automation. The software scales with the learning journey without requiring migration to different platforms.

## VirtualBox vs. UTM
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
