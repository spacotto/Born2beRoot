# Choosing an Operating System (OS)
When selecting the OS for your VM, consider its **compatibility** with your **hardware** and **virtualisation software**, as well as the **ease of installation and use**. Look for systems that are **well-documented** and have **strong community support**, as this makes **troubleshooting** much easier for beginners. It's also important to think about your **goals**: choose an OS that aligns with what you want to learn or accomplish, whether it's getting comfortable with Linux, testing software, or developing projects. Opting for a **widely used, stable, and beginner-friendly OS** (such as Ubuntu or Debian) can make the entire process smoother and less overwhelming.

## What is a "Guest" Operating System?
A **Guest Operating System** (Guest OS) is **software installed within a VM that runs on a virtualised environment created by a host operating system**. It operates as a **secondary OS**, providing an **independent environment** for running applications, particularly those incompatible with the host OS. The guest OS **interacts with virtual hardware provided** by the hypervisor rather than the physical hardware directly, and it manages its own resources within the VM. **Multiple guest operating systems can run simultaneously** on a single physical machine, each isolated within its own VM, enabling the execution of diverse applications requiring different OS environments on the same hardware.

## Debian vs. Rocky
**Debian** and **Rocky Linux** are free, open-source Linux distributions: complete operating systems that include the Linux kernel, system utilities, and thousands of pre-packaged software applications ready to install and use.

### Common Traits
1. **Strong reputation for stability.** Both are known for being **reliable and predictable** (aka ideal for servers where you don’t want surprises).
2. **Long-Term Support (LTS) philosophy.** Each distribution provides many years of **security updates**, making them safe for production systems.
3. **Community-driven, not corporate-controlled.** Debian is fully community-developed. Rocky Linux was created by the community after CentOS shifted direction. Both aim to remain **independent** and stable.
4. **Excellent documentation and large user communities.** Lots of tutorials, forum discussions, and troubleshooting guides exist for both.
5. **Security-focused by design.** Secure defaults, quick security patches, and compatibility with hardened configurations (like SELinux or AppArmor, depending on the distro).
6. **Suitable for similar workloads.** Both can run: web servers (Apache, Nginx); databases (PostgreSQL, MySQL); containers (Docker, Podman); virtualisation tools; development stacks.
7. **Free and open-source.** No licensing fees, freely redistributable.

>[!WARNING]
>What’s not the same: **Debian** uses the `APT` package manager and `.deb` packages, while **Rocky Linux** is a **Red Hat Enterprise Linux clone** and uses `DNF/YUM` with `.rpm` packages.

### Comparison Table: Debian vs Rocky Linux
|                    | Debian                                               | Rocky Linux                                          |
| :----------------- | :--------------------------------------------------- | :--------------------------------------------------- |
| Stability          | Highly stable, focuses on thoroughly tested packages | Enterprise-grade stability, RHEL binary compatible   |
| Documentation      | Extensive, beginner-friendly resources               | Strong enterprise documentation, RedHat-based guides |
| Package Management | APT – intuitive and widely used                      | DNF/YUM – powerful but less familiar to beginners    |
| Package Repository | Massive repository, wide software availability       | Smaller but curated for enterprise use               |
| Learning Curve     | Gentle, great for beginners                          | Steeper, more enterprise-focused                     |
| Update Cycle       | Packages may be older (stability focus)              | Conservative updates with enterprise focus           |
| Use Case           | General purpose, education, servers                  | Enterprise production environments                   |
| Community          | Large, diverse community                             | Growing community, backed by enterprise users        |

### Comparison Table: AppArmor vs SELinux
| Aspect              | AppArmor                                         | SELinux                                                |
| :------------------ | :----------------------------------------------- | :----------------------------------------------------- |
| Complexity          | Simple to configure and understand               | Complex policy language, steep learning curve          |
| Security Model      | Path-based (uses file paths)                     | Label-based (uses security contexts)                   |
| Default On          | Debian and Ubuntu                                | Rocky, RHEL, Fedora                                    |
| Granularity         | Less granular control                            | Highly granular, comprehensive security                |
| Learning Curve      | Gentle, beginner-friendly                        | Steep, requires significant learning                   |
| Troubleshooting     | Easier to debug and fix issues                   | Difficult to troubleshoot, cryptic errors              |
| Security Robustness | Can be bypassed with hardlinks/symlinks          | More robust, label-based system                        |
| Industry Use        | Common in Debian-based systems                   | Industry standard in enterprise environments           |
| Profile Creation    | More intuitive, human-readable                   | Requires understanding of policy language              |

### Comparison Table: UFW vs firewalld
| Aspect              | UFW (Uncomplicated Firewall)                     | firewalld                                              |
| :------------------ | :----------------------------------------------- | :----------------------------------------------------- |
| Full Name           | Uncomplicated Firewall                           | FirewallD                                              |
| Complexity          | Simple, straightforward syntax                   | More complex, feature-rich                             |
| Learning Curve      | Very easy, beginner-friendly                     | Moderate, requires understanding zones                 |
| Default On          | Debian and Ubuntu                                | Rocky, RHEL, Fedora                                    |
| Configuration       | Command-line with simple syntax                  | Zone-based configuration system                        |
| Dynamic Management  | Static rules (requires reload)                   | Dynamic, no restart needed for changes                 |
| Use Case            | Simple firewall needs, basic servers             | Complex networking, multiple interfaces                |
| Zones Concept       | No zone support                                  | Supports multiple trust zones                          |
| Features            | Basic but sufficient for most cases              | Advanced features for complex setups                   |
| Interface           | CLI only (simple commands)                       | CLI and GUI tools available                            |

## Your Choice
### Choose Debian if...
You are a beginner. Debian is generally easier for a first server due to several reasons.
1. **Simpler defaults.** Debian comes with fewer vendor-specific tools, less SELinux complexity (it uses `AppArmor` by default), and a cleaner base system. Fewer moving parts mean fewer surprises.
2. **Package management is beginner-friendly.** APT commands are intuitive, dependencies resolve cleanly, and most guides on the internet assume Debian/Ubuntu-style commands.
3. **Documentation is extremely thorough but easy to digest.** Debian’s official docs are high quality, and the community is vast.
4. **Predictable, stable environment.** Debian favours stability over novelty, which is ideal for someone setting up a first server.

>[!IMPORTANT]
>Debian is highly recommended if you are new to system administration.

### Choose Rocky if...
You are interested in **Red Hat Enterprise Linux**. For example:
1. you want to work in environments that use **Red Hat Enterprise Linux** (corporate IT, enterprise data centres);
2. you’ll eventually need **SELinux** in enforcing mode, which is the default and deeply integrated in the RHEL ecosystem;
3. you want access to **RHEL-specific tooling** (Cockpit, system roles, etc.).

## My Choice: Debian 13 (Trixie)
Debian 13, codenamed "Trixie," is the **latest release** (November 2025) of the **Debian Linux OS**, known for its **stability**, **security**, and **reliability**. Like previous Debian versions, Trixie is a **free**, **open-source** OS that can be used on servers, desktops, and VMs. It features a **wide selection of software packages**, **robust community support**, and **regular security updates**, making it a popular choice for users seeking a dependable and well-documented Linux experience.

I chose **Debian 13 (Trixie)** over Rocky Linux because, as a beginner, I wanted a system that is simple to set up, well-documented, and widely supported by the community. Debian is known for its stability and ease of use, making it ideal for learning the basics of Linux without being overwhelmed by complexity. Moreover, since **I'm not specifically interested in working with Red Hat Enterprise Linux (RHEL)** environments or their derivatives, Rocky Linux's enterprise focus didn't match my needs. Debian 13 lets me explore, learn, and customise my VM with confidence, while providing plenty of helpful resources for newcomers.
