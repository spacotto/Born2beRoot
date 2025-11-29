# About Uncomplicated Firewall (UFW)
**Uncomplicated Firewall (UFW)** is a user-friendly **frontend or wrapper** (aka interface) for managing **iptables firewall rules** on Debian systems.

>[!NOTE]
>An **iptables** is the **command-line tool** traditionally used on Linux systems like Debian to **configure the kernel's Netfilter framework**. **Netfilter** is the underlying, low-level **packet filtering system** inside the Linux kernel that handles network traffic.

## Installation
```
sudo apt install ufw
```

## Basic Commands
- Enable UFW (Start firewall and enable on boot)
```
sudo ufw enable
```
- Disable UFW (Stop firewall)
```
sudo ufw disable
```
- Check Status
```
sudo ufw status           # Basic status
sudo ufw status verbose   # Detailed status
sudo ufw status numbered  # Show rule numbers
```
