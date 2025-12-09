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
nano /etc/sudoers.d/sudo_config          # sudo Password Configuration
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
```
xxx
```

## SUDO
```
xxx
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
