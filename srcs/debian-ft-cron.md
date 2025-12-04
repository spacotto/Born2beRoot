# About Cron
**Time-based job scheduling** is an integral part of most operating systems. In the UNIX world, this is usually accomplished by a program called cron.

>[!IMPORTANT]
>[Here](https://wiki.debian.org/cron) you can find official Debian documentation on **cron**.

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
