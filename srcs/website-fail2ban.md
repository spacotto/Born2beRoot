# About Fail2Ban
Fail2Ban **monitors log files for suspicious activity** (like repeated failed login attempts) and **temporarily bans IP addresses** by adding firewall rules. It helps protect your server from brute-force attacks.

## Installation
```
sudo apt update
sudo apt install fail2ban
sudo systemctl status fail2ban
```

>[!TIP]
>If Fail2Ban is NOT active, run the following commands:
>```
>sudo systemctl enable fail2ban
>sudo systemctl start fail2ban
>```

## Core Concepts
- Jail: A service to monitor (SSH, lighttpd, WordPress, etc.)
- Filter: Regex patterns that identify malicious activity in logs
- Action: What to do when a match is found (usually ban the IP)
- Ban time: How long an IP stays blocked
- Max retry: Number of failed attempts before banning

## Configuration Files
Default config (don't edit directly)
```
/etc/fail2ban/jail.conf
```

Your custom config (overrides jail.conf)
```
/etc/fail2ban/jail.local
```

Filter definitions
```
/etc/fail2ban/filter.d/
```

Action definitions
```
/etc/fail2ban/action.d/
```
