# About Monitoring Script Service
>[!IMPORTANT]
>A monitoring service **tracks scheduled jobs and alerts** you when they fail to run, run unsuccessfully, or produce unexpected output.

## Basic Monitoring Approaches
### 1. Email Notifications (Built-in)
Cron automatically emails output to the user. Configure in crontab:
```
MAILTO=admin@example.com
```
>[!WARNING]
>All job output (`stdout`/`stderr`) will be emailed. To suppress emails for successful runs:
>```
>0 2 * * * /path/to/script.sh > /dev/null 2>&1
>```

### 2. Logging to Files
Add logging to your cron jobs:
```
0 2 * * * /path/to/script.sh >> /var/log/myscript.log 2>&1
```
>[!NOTE]
>Monitor logs with `logrotate` to prevent disk fills. Create `/etc/logrotate.d/myscript`:
>```
>/var/log/myscript.log {
>    weekly
>    rotate 4
>    compress
>    missingok
>    notifempty
>}
>```

### 3. External Monitoring Services
Healthchecks.io Pattern (works with any similar service):
```
# Successful run notification
0 2 * * * /path/to/script.sh && curl -m 10 --retry 5 https://hc-ping.com/YOUR-UUID
```
>[!NOTE]
>The service expects regular pings. Missing pings trigger alerts.

## Monitoring Script Configuration
>[!IMPORTANT]
>[Here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/debian-pckg-cron.md) you can find the details about cron.

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
LVM_ACTIVE=$(if [ $(lsblk | grep "lvm" | wc -l) -gt 0 ]; then echo "active"; else echo "inactive"; fi)

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

# Message to display
MESSAGE="
==============================================================
                   SYSTEM MONITORING REPORT
==============================================================

Date:            $(date '+%Y-%m-%d %H:%M:%S')

Architecture:    $ARCH

Physical CPUs:   $PCPU
Virtual CPUs:    $VCPU
CPU Load:        $CPU_LOAD

Memory Usage:    ${RAM_USED}MB / ${RAM_TOTAL}MB (${RAM_PERCENT}%)

Disk Usage:      ${DISK_USED} / ${DISK_TOTAL} (${DISK_PERCENT})

Last Boot:       $LAST_BOOT

LVM Active:      $LVM_ACTIVE

TCP Connections: $TCP_CONN

Users Logged In: $USER_COUNT

IPv4 Address:    $IP_ADDR
MAC Address:     $MAC_ADDR

Sudo Commands:   $SUDO_CMDS

==============================================================
"

# Broadcast to all terminals
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
*/10 * * * * /usr/local/bin/monitoring.sh | wall    # Display every 10m
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
