# Partitioning
>[!IMPORTANT]
>[Here](https://wiki.debian.org/Partition) you can find the **official Debian documentation** concerning partitioning.

## Definition
Partitioning in VMs refers to the **process of dividing physical resources** (such as CPU, memory, storage, and network) **into isolated, dedicated segments for individual VMs**, enabling **efficient resource allocation** and **enhanced security**. This is typically managed by a **hypervisor**, which acts as a **virtualization layer** to allocate specific portions of the physical hardware to each VM, ensuring that multiple VMs can share the underlying resources without contention.

## Applications
Each VM operates in its own **isolated** environment, **independent** of others running on the same physical server, which prevents issues in one VM from affecting others and **reduces the risk of security breaches by containing vulnerabilities** within individual VMs. This isolation enhances system **stability**, **reliability**, and **security**, allowing administrators to manage and troubleshoot VMs individually.

In addition to resource allocation, partitioning supports **dynamic resource management**, where the hypervisor can adjust CPU, memory, and storage allocations in real time based on workload demands, improving performance and cost-effectiveness. It also enables resource **pooling** across multiple physical servers, allowing for greater **scalability** and **flexibility** in managing IT infrastructure.

A specific application of partitioning is **GPU partitioning**, which allows **a single physical GPU to be shared among multiple VMs** by assigning each VM a dedicated fraction of the GPU’s resources using hardware-backed security boundaries like Single Root I/O Virtualization (SR-IOV). This is particularly useful for **workloads requiring GPU acceleration**, such as Virtual Desktop Infrastructure (VDI) and Artificial Intelligence (AI) inference, enabling higher density and scalability while reducing total cost of ownership.

## Hardware Partitioning vs. VM Partitioning
It is important to distinguish this from **hardware-level partitioning**, where partitions run directly on the hardware **without a hypervisor**, which is not virtualized and thus **less portable** but can offer **better performance and scalability**. 

In contrast, **VM-based partitioning** is fully virtualized and transparent to the guest operating system, allowing for greater **flexibility**, **portability**, and features like **live migration and fault tolerance**.

VMs do not use physical partitions on the host disk. Instead, they use virtual disks (e.g.: `.vmdk` or `.vhdx` files) that are **stored as files** on the host’s filesystem. These virtual disks function as **independent storage units** within the VM, allowing for easy backup, migration, and resizing without affecting the host system.

```
# lsblk
NAME                     MAJ:MIN RM   SIZE RO TYPE  MOUNTPOINTS
sda                        8:0    0  30.8G  0 disk
├─sda1                     8:1    0   243M  0 part  /boot       # primary         
├─sda2                     8:2    0     1K  0 part              # extended
└─sda5                     8:5    0 223.3G  0 part              # logical
  └─sda5_crypt           254:0    0  23.3G  0 crypt 
    ├─LVMGroup-root      254:0    0  23.3G  0 lvm   /
    ├─LVMGroup-swap      254:0    0  23.3G  0 lvm   [SWAP]
    ├─LVMGroup-home      254:0    0  23.3G  0 lvm   /home
    ├─LVMGroup-var       254:0    0  23.3G  0 lvm   /var
    ├─LVMGroup-srv       254:0    0  23.3G  0 lvm   /srv
    ├─LVMGroup-tmp       254:0    0  23.3G  0 lvm   /tmp
    └─LVMGroup-var--log  254:0    0  23.3G  0 lvm   /var/log
sr0                       11:0    1  1024M  0 rom
```

## Sources
- [GPU partitioning](https://learn.microsoft.com/en-us/windows-server/virtualization/hyper-v/gpu-partitioning)
- [Understanding Partitioning, BROADCOM](https://techdocs.broadcom.com/us/en/vmware-tanzu/data-solutions/tanzu-gemfire/10-1/gf/developing-partitioned_regions-how_partitioning_works.html)
- [VM, It Is Not What You Think!](https://www.packtpub.com/en-us/learning/how-to-tutorials/vm-it-not-what-you-think/)
