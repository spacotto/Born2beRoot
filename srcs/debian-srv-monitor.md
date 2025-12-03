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
---
```

### 2. Configure the script
```
---
```

### 3. Make the script executable
```
chmod 700 <script path>    # chmod +x gives the same result
```

### 4. Use in Crontab
```
---```
