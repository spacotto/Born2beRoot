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
### Install Monitoring Tools
```
apt update
apt install monitoring-plugins mailutils
```

### Create a Monitoring Script
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

### Make executable
```
chmod 700 /usr/local/bin/cron-monitor.sh    # chmod +x gives the same result
```

### Use in Crontab
```
0 2 * * * /usr/local/bin/cron-monitor.sh /path/to/your-script.sh
```
