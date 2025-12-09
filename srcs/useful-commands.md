# Useful Commands
Here is a list of the most used command lines to check the state of your VM server

## System Status
Graphical Interface (GUI) status:
```
ls /usr/bin/*session
```

UFW status:
```
sudo systemctl status UFW
```

SSH status:
```
sudo systemctl status ssh
```

Check chosen OS:
```
head -n 2 /etc/os-release
```

## Users & Groups
Check user groups:
```
groups username                          # Write the username of the user you want to check
```

Check group members:
```
getent group group1 group2 group3 ...    # Write the names of the groups you want to check
```

Check password policy configuration:
```
nano /etc/login.defs                     # Password Expiration Configuration
nano /etc/pam.d/common-password          # Password Complexity Configuration
```

Create user:
```
sudo adduser username
```

Create group:
```
sudo addgroup group_name
```

Add user to group:
```
sudo adduser usename group_name
```

## Hostname & Partitions
Check hostname:
```
hostname
```

Change hostname:
```
sudo nano /etc/hostname
sudo nano /etc/hosts
```

Check partition scheme:
```
lsblk
```

## SUDO
Check sudo status:
```
which sudo      # Locate sudo folder
sudo -V         # Check sudo version
```

Check sudo password policy configuration:
```
sudo nano /etc/sudoers.d/sudo_config    # sudo Password Configuration

```

Check `/var/log/sudo/`:
```
sudo ls /var/log/sudo/
sudo cat /var/log/sudo/
```

## UFW 
```
xxx
```

## SSH 
```
xxx
```

## Script monitoring
