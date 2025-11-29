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
### Enable/Disable UFW
```
sudo ufw enable                          # Start firewall and enable on boot
sudo ufw disable                         # Stop firewall
```
### Check Status
```
sudo ufw status                          # Basic status
sudo ufw status verbose                  # Detailed status
sudo ufw status numbered                 # Show rule numbers
```

## Managing Rules
### Allow/Deny Connections
```
sudo ufw allow 22                        # Allow port 22 (SSH)
sudo ufw allow ssh                       # Allow by service name
sudo ufw allow 80/tcp                    # Allow port 80, TCP only

sudo ufw allow from 192.168.1.100        # Allow specific IP
sudo ufw allow from 192.168.1.0/24       # Allow subnet
sudo ufw allow proto tcp to any port 80  # Specific protocol

sudo ufw deny 25                         # Deny port 25
```

### Delete Rules
```
sudo ufw delete allow 80                 # Delete by rule
sudo ufw status numbered                 # List numbered rules
sudo ufw delete 2                        # Delete rule number 2
```

### Common Service Ports
```
sudo ufw allow http                      # Port 80
sudo ufw allow https                     # Port 443
sudo ufw allow ssh                       # Port 22
sudo ufw allow ftp                       # Port 21
```

## Default Policies
```
sudo ufw default deny incoming           # Block all incoming
sudo ufw default allow outgoing          # Allow all outgoing
sudo ufw default deny outgoing           # Block all outgoing
```
