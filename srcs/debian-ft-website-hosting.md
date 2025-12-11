# About Hosting WordPress on Debian VM
**Prerequisites:**
- Debian VM with `root` or `sudo` access
- Domain name (optional, but recommended)
- Basic command line knowledge

## Host WordPress on Debian VM
### Update System
```
sudo apt update
sudo apt upgrade -y
```

### Install Lighttpd
>[!IMPORTANT]
>[Here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/website-lighttpd.md#basic-configuration) you can find more details concerning Lighttpd.

```
sudo apt install lighttpd -y
sudo ufw allow 80                        # Default port for web services
sudo ufw status                          # Remember to include port 80 (VM Settings → Network → Port forwarding 80:81)
sudo systemctl status lighttpd
```
>[!TIP]
>If lighttpd is not active, run these commands:
>```
>sudo systemctl enable lighttpd
>sudo systemctl start lighttpd
>```

### Install WordPress
>[!IMPORTANT]
>[Here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/website-wordpress.md) you can find more details concerning WordPress.

```
cd /tmp
wget https://wordpress.org/latest.tar.gz                        # Use wget to retrieve files, create mirrors of websites, and handle downloads in the background
tar -xvzf latest.tar.gz
sudo mv wordpress /var/www/html/
sudo chown -R www-data:www-data /var/www/html/wordpress
sudo chmod -R 755 /var/www/html/wordpress
```

### Install MariaDB
>[!IMPORTANT]
>[Here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/website-mariadb.md) you can find more details concerning MariaDB.

Install MariaDB:
```
sudo apt install mariadb-server -y
sudo systemctl status mariadb
```

>[!TIP]
>If MariaDB is not active, run these commands:
>```
>sudo systemctl enable mariadb
>sudo systemctl start mariadb
>```

Secure the installation:
```
sudo mariadb-secure-installation        # This will trigger the WARNING mentioned below
```

>[!WARNING]
>MariaDB is secure by default in Debian. Running this script is useless at best, and misleading at worst. This script will be removed in a future MariaDB release in Debian. Please read `mariadb-server.README.Debian` for details.

Follow these steps to secure MariaDB:
```
Enter root password
Switch to unix_socket authentication?        # Enter N (You already have your root account protected, so you can safely answer 'n'.)
Change the root password?                    # Enter N (You already have your root account protected, so you can safely answer 'n'.)
Remove anonymous users?                      # Enter Y (By default, a MariaDB installation has an anonymous user, allowing anyone to log into MariaDB without having to have a user account created for them. This is intended only for testing, and to make the installation go a bit smoother.  You should remove them before moving into a production environment.)
Disallow root login remotely?                # Enter Y (Normally, root should only be allowed to connect from 'localhost'. This ensures that someone cannot guess at the root password from the network.)
Remove test database and access to it?       # Enter Y (By default, MariaDB comes with a database named 'test' that anyone can access. This is also intended only for testing, and should be removed before moving into a production environment.)
Reload privilege tables now?                 # Enter Y (Reloading the privilege tables will ensure that all changes made so far will take effect immediately.)
```

### Install PHP
>[!IMPORTANT]
>[Here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/website-php.md) you can find more details concerning PHP.

```
sudo apt install php-fpm php-mysql php-curl php-gd php-mbstring php-xml php-xmlrpc php-zip php-imagick php-cgi -y
sudo systemctl enable php8.4-fpm
sudo systemctl start php8.4-fpm
```
>[!NOTE]
>PHP version may vary (8.1, 8.2, etc.). Adjust commands accordingly.

>[!TIP]
>Check your PHP version by running this command:
>```
>php -v
>```

### Create WordPress Database with MariaDB
```
sudo mariadb
```

Inside MariaDB:
```
CREATE DATABASE wp_database;
CREATE USER 'user'@'localhost' IDENTIFIED BY 'password';        # Enter your user instead of "user" and enter your chosen password instead of "password".
GRANT ALL PRIVILEGES ON wp_database.* TO 'user'@'localhost';
FLUSH PRIVILEGES;
exit
```

### Configure Lighttpd for WordPress
Create or edit the Lighttpd configuration:
```
sudo nano /etc/lighttpd/lighttpd.conf
```
Ensure these settings are present:
```
server.document-root = "/var/www/html"
server.upload-dirs = ( "/var/cache/lighttpd/uploads" )
server.errorlog = "/var/log/lighttpd/error.log"
server.pid-file = "/run/lighttpd.pid"
server.username = "www-data"
server.groupname = "www-data"
server.port = 80

index-file.names = ( "index.php", "index.html" )
```
Enable URL rewriting module:
```
sudo lighttpd-enable-mod rewrite
sudo systemctl restart lighttpd
```

### Configure WordPress
Create WordPress Configuration
```
cd /var/www/html/
sudo cp wp-config-sample.php wp-config.php
sudo nano /var/www/html/wp-config.php
```

Update these lines with your database details:
```
define( 'DB_NAME', 'database_name_here' );
define( 'DB_USER', 'username_here' );
define( 'DB_PASSWORD', 'password_here' );
define( 'DB_HOST', 'localhost' );
```
Generate and add security keys. Visit `https://api.wordpress.org/secret-key/1.1/salt/` and replace the placeholder keys in wp-config.php.

Set proper permissions:
```
sudo chown -R www-data:www-data /var/www/html/wordpress
sudo find /var/www/html/wordpress -type d -exec chmod 755 {} \;
sudo find /var/www/html/wordpress -type f -exec chmod 644 {} \;
```

### Complete WordPress Installation
In your browser, visit:
```
http://localhost:host_port
```

Complete WordPress installation:
![wordpress](https://github.com/spacotto/Born2beRoot/blob/main/imgs/Screenshot%20from%202025-12-11%2011-15-24.png)

### Install & Configure Fail2Ban
Install Fail2Ban:
```
sudo aptitude install fail2ban
```

## Troublshooting
### PHP files downloading instead of executing
Check if FastCGI-PHP is enabled:
```
sudo lighttpd-enable-mod fastcgi
sudo lighttpd-enable-mod fastcgi-php
sudo systemctl restart lighttpd
```

### Permission errors
Reset WordPress permissions:
```
sudo chown -R www-data:www-data /var/www/html/wordpress
```

### Can't access site
Check if Lighttpd is running:
```
sudo systemctl status lighttpd
```

### Database connection error
Verify credentials in `wp-config.php` and `MariaDB` user privileges.

## Security Tips
- Keep WordPress, themes, and plugins updated
- Use strong passwords for database and admin account
- Install security plugins (Wordfence, Sucuri)
- Regular backups of database and files
- Disable file editing in wp-config.php:
```
define('DISALLOW_FILE_EDIT', true);
```
- Limit login attempts
- Keep PHP and MariaDB updated

## Maintenance
Restart Lighttpd:
```
sudo systemctl restart lighttpd
```
Restart PHP-FPM:
```
sudo systemctl restart php8.2-fpm
```
Backup database:
```
mysqldump -u wpuser -p wordpress > wordpress_backup_$(date +%Y%m%d).sql
```
Backup WordPress files:
```
sudo tar -czf wordpress_files_$(date +%Y%m%d).tar.gz /var/www/html/wordpress
```
Update system:
```
sudo apt update && sudo apt upgrade -y
```
Check Lighttpd configuration:
```
sudo lighttpd -t -f /etc/lighttpd/lighttpd.conf
```
View Lighttpd logs:
```
sudo tail -f /var/log/lighttpd/error.log
```
