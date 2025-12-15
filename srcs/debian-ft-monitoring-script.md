# About Monitoring Script Service
A monitoring service **tracks scheduled jobs and alerts** you when they fail to run, run unsuccessfully, or produce unexpected output.

## Monitoring Script Configuration
>[!IMPORTANT]
>[Here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/debian-ft-cron.md) you can find the details about cron.

### 1. Create a Monitoring Script
```
sudo nano /usr/local/bin/monitoring.sh
```

### 2. Configure the script
```
#!/bin/bash
# System Monitoring Script
# Displays system information

# OS Architecture and Kernel Version
ARCH=$(uname -a)

# CPU Stats
PCPU=$(grep "physical id" /proc/cpuinfo | sort -u | wc -l)               # Physical Processors
VCPU=$(grep "^processor" /proc/cpuinfo | wc -l)                          # Virtual Processors
CPU_LOAD=$(top -bn1 | grep '^%Cpu' | awk '{printf("%.1f%%"), $2 + $4}')  # CPU Load (%)

# RAM Stats
# Current available RAM and its utilization rate (%)
RAM_TOTAL=$(free -m | awk '/Mem:/ {print $2}')
RAM_USED=$(free -m | awk '/Mem:/ {print $3}')
RAM_PERCENT=$(free | awk '/Mem:/ {printf("%.2f"), $3/$2*100}')

# Disk Stats
# Current available storage and its utilization rate (%)
DISK_TOTAL=$(df -BG --total | grep total | awk '{print $2}')
DISK_USED=$(df -BM --total | grep total | awk '{print $3}')
DISK_PERCENT=$(df --total | grep total | awk '{print $5}')

# Last Reboot (Date & Time)
LAST_BOOT=$(who -b | awk '{print $3, $4}')

# LVM Status
LVM_STATUS=""
if [ $(lsblk | grep "lvm" | wc -l) -gt 0 ]; then 
    LVM_STATUS="ACTIVE"
else 
    LVM_STATUS="INACTIVE"
fi

# Active TCP Connections
TCP_CONN=$(ss -t | grep ESTAB | wc -l)

# Logged in Users
USER_COUNT=$(who | wc -l)

# Network Information (IPv4 & MAC)
IP_ADDR=$(hostname -I | awk '{print $1}')
MAC_ADDR=$(ip link show | grep "link/ether" | awk '{print $2}' | head -n1)

# Sudo Commands Count
# Number of commands executed with the sudo program
SUDO_CMDS=$(journalctl _COMM=sudo 2>/dev/null | grep COMMAND | wc -l)

# Broadcast to all terminals
MESSAGE="
==============================================================================
                            SYSTEM MONITORING REPORT
                              $(date '+%Y-%m-%d  %H:%M:%S')
==============================================================================
♦ ARCHITECTURE ♦ $ARCH

                          Physical CPUs: $PCPU
                           Virtual CPUs: $VCPU
                               CPU Load: $CPU_LOAD
                           Memory Usage: ${RAM_USED}MB / ${RAM_TOTAL}MB (${RAM_PERCENT}%)
                             Disk Usage: ${DISK_USED} / ${DISK_TOTAL} (${DISK_PERCENT})
                              Last Boot: $LAST_BOOT
                             LVM Status: $LVM_STATUS
                        TCP Connections: $TCP_CONN
                        Users Logged In: $USER_COUNT
                           IPv4 Address: $IP_ADDR
                            MAC Address: $MAC_ADDR
                          Sudo Commands: $SUDO_CMDS

==============================================================================
"
echo "$MESSAGE" | wall
```

### 3. Make the script executable
```
chmod 700 /usr/local/bin/monitoring.sh    # chmod +x gives the same result
```

### 4. Test if the script works
```
sudo /usr/local/bin/monitoring.sh
```

### 4. Set up cron
Open crontab as `root`
```
sudo crontab -e
```
>[!NOTE]
>Run the cron job as `root` to access all system information:
>- For the physical CPU count to work correctly, your VM needs to expose CPU topology information
>- The sudo command count uses `journalctl`, which requires appropriate permissions
>- The script uses standard Debian utilities that should already be installed

Add timer setting:
```
# Edit this file to introduce tasks to be run by cron.
# 
# Each task to run has to be defined through a single line
# indicating with different fields when the task will be run
# and what command to run for the task
# 
# To define the time you can provide concrete values for
# minute (m), hour (h), day of month (dom), month (mon),
# and day of week (dow) or use '*' in these fields (for 'any').
# 
# Notice that tasks will be started based on the cron's system
# daemon's notion of time and timezones.
# 
# Output of the crontab jobs (including errors) is sent through
# email to the user the crontab file belongs to (unless redirected).
# 
# For example, you can run a backup of all your user accounts
# at 5 a.m every week with:
# 0 5 * * 1 tar -zcf /var/backups/home.tgz /home/
# 
# For more information see the manual pages of crontab(5) and cron(8)
#
# .------------------ minute (0 - 59)
# | .---------------- hour (0 - 23)
# | |   .------------ day of month (1 - 31)
# | |   |   .-------- month (1 - 12) OR jan, feb, mar, etc.
# | |   |   |   .---- day of the week (0 - 6) (Sunday=0 or 7)
# | |   |   |   |
# m h  dom mon dow   command
*/10 * * * * /usr/local/bin/monitoring.sh
# Display every 10m the script found at the given path
```

>[!TIP]
>You can force the script output by running this command:
>```
>watch -n 600 /usr/local/bin/monitoring.sh    # 600 = 60s * 10 (aka you force the 10m)
>```

>[!TIP]
>If you don't want to broadcast everywhere and keep a log file instead, you can change the timer setting as follows:
>```
>*/10 * * * * /usr/local/bin/monitoring.sh >> /var/log/monitoring.log
>```

## Resources
- [5 Custom Bash Scripts to Monitor Your Linux Server Performance](https://dev.to/caffinecoder54/5-custom-bash-scripts-to-monitor-your-linux-server-performance-acj)
- [A Basic Bash Script for System Monitoring](https://medium.com/@wojtekszczerbinski/a-basic-bash-script-for-system-monitoring-b74deb59b7e4)
- [Bash Scripting: Create a Simple System Resource Monitor](https://www.eastagile.com/blogs/bash-system-resource-monitor)
- [Monitoring](https://bash.cyberciti.biz/shell/monitoring/)
