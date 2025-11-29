# About Uncomplicated Firewall (UFW)
**Uncomplicated Firewall (UFW)** is a user-friendly **frontend or wrapper** (aka interface) for managing **iptables firewall rules** on Debian systems.

>[!NOTE]
>An **iptables** is the **command-line tool** traditionally used on Linux systems like Debian to **configure the kernel's Netfilter framework**. **Netfilter** is the underlying, low-level **packet filtering system** inside the Linux kernel that handles network traffic.

>[!IMPORTANT]
> [Here](https://wiki.debian.org/Uncomplicated%20Firewall%20%28ufw%29) you can find the official Debian documentation about UFW.

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

## Managing Rules
- Allow Connections
```
sudo ufw allow 22                        # Allow port 22 (SSH)
sudo ufw allow ssh                       # Allow by service name
sudo ufw allow 80/tcp                    # Allow port 80, TCP only

sudo ufw allow from 192.168.1.100        # Allow specific IP
sudo ufw allow from 192.168.1.0/24       # Allow subnet
sudo ufw allow proto tcp to any port 80  # Specific protocol
```

- Deny Connections
```
sudo ufw deny 25                         # Deny port 25
```
