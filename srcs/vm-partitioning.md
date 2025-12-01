# Partitioning
>[!IMPORTANT]
>[Here](https://wiki.debian.org/Partition) you can find the **official Debian documentation** concerning partitioning.

## Definition
Partitioning in VMs refers to the **process of dividing physical resources** (such as CPU, memory, storage, and network) **into isolated, dedicated segments for individual VMs**, enabling **efficient resource allocation** and **enhanced security**. This is typically managed by a **hypervisor**, which acts as a **virtualisation layer** to allocate specific portions of the physical hardware to each VM, ensuring that multiple VMs can share the underlying resources without contention.

## Applications
Each VM operates in its own **isolated** environment, **independent** of others running on the same physical server, which prevents issues in one VM from affecting others and **reduces the risk of security breaches by containing vulnerabilities** within individual VMs. This isolation enhances system **stability**, **reliability**, and **security**, allowing administrators to manage and troubleshoot VMs individually.

In addition to resource allocation, partitioning supports **dynamic resource management**, where the hypervisor can adjust CPU, memory, and storage allocations in real time based on workload demands, improving performance and cost-effectiveness. It also enables resource **pooling** across multiple physical servers, allowing for greater **scalability** and **flexibility** in managing IT infrastructure.

A specific application of partitioning is **GPU partitioning**, which allows **a single physical GPU to be shared among multiple VMs** by assigning each VM a dedicated fraction of the GPU’s resources using hardware-backed security boundaries like Single Root I/O Virtualisation (SR-IOV). This is particularly useful for **workloads requiring GPU acceleration**, such as Virtual Desktop Infrastructure (VDI) and Artificial Intelligence (AI) inference, enabling higher density and scalability while reducing total cost of ownership.

## Hardware Partitioning vs. VM Partitioning
It is important to distinguish this from **hardware-level partitioning**, where partitions run directly on the hardware **without a hypervisor**, which is not virtualized and thus **less portable** but can offer **better performance and scalability**. 

In contrast, **VM-based partitioning** is fully virtualized and transparent to the guest operating system, allowing for greater **flexibility**, **portability**, and features like **live migration and fault tolerance**.

VMs do not use physical partitions on the host disk. Instead, they use virtual disks (e.g., `.vmdk` or `.vhdx` files) that are **stored as files** on the host’s filesystem. These virtual disks function as **independent storage units** within the VM, allowing for easy backup, migration, and resizing without affecting the host system.

## Terminology
### Physical Layer
Physical Disk (`sda`)
>A storage device recognised by the system (physical drive or virtual disk in VMs). Named sequentially: `sda`, `sdb`, `sdc`, etc. The foundation for all partitions and volumes.

CD-ROM Drive (`sr0`)
>Optical drive or virtual ISO mount. Read-only storage device. `sr` = SCSI CD-ROM device.

### Partition Layer
Primary Partition (`sda1`)
>Direct division of the physical disk. Limited to 4 primary partitions per disk (`MBR`). Typically used for boot partition (`/boot`).

Extended Partition (`sda2`)
>Special primary partition that acts as a container. Allows creation of multiple logical partitions beyond the 4-partition limit. Cannot store data directly

Logical Partition (`sda5`)
>Partition created **inside an extended partition**. Numbered starting from `5` (even if fewer than 4 primary partitions exist). Can be used for **data** or as **base for encryption/LVM**.

### Encryption Layer
LUKS Encrypted Container (`sda5_crypt`).
>**Linux Unified Key Setup**, encryption standard. Sits on top of a partition, encrypting all data within. Must be unlocked with a **passphrase** before accessing contents. Named with `_crypt` suffix by convention.

### LVM Layer (Logical Volume Manager)
Volume Group (LVMGroup)
>Pool of storage space created from one or more physical volumes. Acts as a container for logical volumes. Allows flexible space allocation.

Logical Volume (LVMGroup-root, LVMGroup-home, etc.)
>Virtual partition created from volume group space. Can be resized, moved, and snapshotted without unmounting. Mounted to specific directories in the filesystem.

### Common Logical Volumes (LVs)
root (`/`)
>Core system files and installed software

swap (`[SWAP]`)
>Virtual memory extension for RAM

home (`/home`)
>User personal files and settings

var (`/var`)
>Variable data (caches, databases, mail)

srv (`/srv`)
>Data served by system services

tmp (`/tmp`)
>Temporary files, cleared on reboot

var--log (`/var/log`)
>System and application logs

### Device Types
disk
>Physical or virtual storage device

part
>Partition on a disk

crypt
>Encrypted container

lvm
>Logical Volume Manager volume

rom
>Read-only optical media

### Typical Setup Flow
1. Physical disk identified (sda)
2. Partitioned into boot, extended, and logical partitions
3. Logical partition encrypted with LUKS
4. Encrypted space used as LVM physical volume
5. Logical volumes created for different system directories

## Sources
- [GPU partitioning](https://learn.microsoft.com/en-us/windows-server/virtualization/hyper-v/gpu-partitioning)
- [Understanding Partitioning, BROADCOM](https://techdocs.broadcom.com/us/en/vmware-tanzu/data-solutions/tanzu-gemfire/10-1/gf/developing-partitioned_regions-how_partitioning_works.html)
- [VM, It Is Not What You Think!](https://www.packtpub.com/en-us/learning/how-to-tutorials/vm-it-not-what-you-think/)
