# About Cron Script Monitoring Service
>[!IMPORTANT]
>A cron monitoring service **tracks scheduled jobs and alerts** you when they fail to run, run unsuccessfully, or produce unexpected output.

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

## Setting Up a Local Monitoring Service
### 1. Install Monitoring Tools
```
apt update
apt install monitoring-plugins mailutils
```

### 2. Create a Monitoring Script
Save as `/usr/local/bin/cron-monitor.sh`:
```
#!/bin/bash

SCRIPT="$1"
LOG="/var/log/cron-monitor.log"
ALERT_EMAIL="admin@example.com"

echo "$(date): Running $SCRIPT" >> "$LOG"

if $SCRIPT >> "$LOG" 2>&1; then
    echo "$(date): SUCCESS - $SCRIPT" >> "$LOG"
    exit 0
else
    echo "$(date): FAILED - $SCRIPT" >> "$LOG"
    echo "Cron job failed: $SCRIPT" | mail -s "Cron Failure Alert" "$ALERT_EMAIL"
    exit 1
fi
```

### 3. Make executable
```
chmod 700 /usr/local/bin/cron-monitor.sh    # chmod +x gives the same result
```

### 4. Use in Crontab
```
0 2 * * * /usr/local/bin/cron-monitor.sh /path/to/your-script.sh
```

## Basic Cron Commands
### View Crontabs
- View current user's crontab
```
crontab -l
```

- View specific user's crontab (as root)
```
crontab -l -u username
```

- View system-wide cron jobs
```
ls /etc/cron.d/
cat /etc/crontab
```

### Edit Crontabs
- Edit current user's crontab
```
crontab -e
```

- Edit specific user's crontab (as root)
```
crontab -e -u username
```

### Enable/Disable Cron Service
- Check cron service status
```
systemctl status cron
```

- Start cron service
```
systemctl start cron
```

- Stop cron service
```
systemctl stop cron
```

- Enable cron at boot
```
systemctl enable cron
```

- Disable cron at boot
```
systemctl disable cron
```

- Restart cron service
```
systemctl restart cron
```

### Verify Cron is Working
- Check if cron daemon is running
```
ps aux | grep cron
```

- View recent cron execution logs
```
grep CRON /var/log/syslog | tail -20
```

- Test with a simple cron job (runs every minute)
```
* * * * * echo "Test at $(date)" >> /tmp/crontest.log
```
