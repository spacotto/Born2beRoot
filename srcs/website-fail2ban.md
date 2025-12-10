# About Fail2Ban
Fail2Ban **monitors log files for suspicious activity** (like repeated failed login attempts) and **temporarily bans IP addresses** by adding firewall rules. It helps protect your server from brute-force attacks.

## Installation
```
sudo apt update
sudo apt install fail2ban
sudo systemctl status fail2ban
```

>[!TIP]
>If Fail2Ban is NOT active, run the floowing commands:
>```
>sudo systemctl enable fail2ban
>sudo systemctl start fail2ban
>```
