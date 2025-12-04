# About Hosting WordPress on Debian VM
**Prerequisites:**
- Debian VM with `root` or `sudo` access
- Domain name (optional, but recommended)
- Basic command line knowledge

## Host WordPress on Debian VM
>[!IMPORTANT]
>[Here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/website-wordpress.md) you can find more details concerning WordPress.

### Step 1: Update System
```
sudo apt update
sudo apt upgrade -y
```

### Step 2: Install Lighttpd
>[!IMPORTANT]
>Here you can find more details concerning Lighttpd.

```
sudo apt install lighttpd -y
sudo systemctl enable lighttpd
sudo systemctl start lighttpd
```

### Step 3: Install MariaDB
>[!IMPORTANT]
>Here you can find more details concerning MariaDB.

```
sudo apt install mariadb-server -y
sudo systemctl enable mariadb
sudo systemctl start mariadb
sudo mysql_secure_installation
```
>[!NOTE]
>Follow the prompts to secure MariaDB:
>1. set root password
>2. remove anonymous users
>3. disallow remote root login
>4. remove test database

### Step 4: Install PHP
>[!IMPORTANT]
>Here you can find more details concerning PHP.

```
sudo apt install php-fpm php-mysql php-curl php-gd php-mbstring php-xml php-xmlrpc php-zip php-imagick -y
sudo systemctl enable php8.2-fpm
sudo systemctl start php8.2-fpm
```
>[!NOTE]
>PHP version may vary (8.1, 8.2, etc.). Adjust commands accordingly.

### Step: Configure Lighttpd for PHP
Enable FastCGI modules:
```
sudo lighttpd-enable-mod fastcgi
sudo lighttpd-enable-mod fastcgi-php
```
Edit the PHP configuration:
```
sudo nano /etc/lighttpd/conf-available/15-fastcgi-php.conf
```
Ensure it contains:
```
fastcgi.server += ( ".php" =>
        ((
                "socket" => "/run/php/php8.2-fpm.sock",
                "broken-scriptfilename" => "enable"
        ))
)
```
Restart Lighttpd:
```
sudo systemctl restart lighttpd
```

### Step 5: Create WordPress Database
```
sudo mysql -u root -p
```
Inside MariaDB:
```
CREATE DATABASE wordpress;
CREATE USER 'wpuser'@'localhost' IDENTIFIED BY 'strong_password';
GRANT ALL PRIVILEGES ON wordpress.* TO 'wpuser'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```

### Step 6: Download and Install WordPress
```
cd /tmp
wget https://wordpress.org/latest.tar.gz
tar -xvzf latest.tar.gz
sudo mv wordpress /var/www/html/
sudo chown -R www-data:www-data /var/www/html/wordpress
sudo chmod -R 755 /var/www/html/wordpress
```

### Step 7: Configure Lighttpd for WordPress
Create or edit the Lighttpd configuration:
```
sudo nano /etc/lighttpd/lighttpd.conf
```
Ensure these settings are present:
```
server.document-root = "/var/www/html/wordpress"
server.upload-dirs = ( "/var/cache/lighttpd/uploads" )
server.errorlog = "/var/log/lighttpd/error.log"
server.pid-file = "/run/lighttpd.pid"
server.username = "www-data"
server.groupname = "www-data"
server.port = 80

index-file.names = ( "index.php", "index.html" )

url.rewrite-if-not-file = (
    "^/(.*)$" => "/index.php/$1"
)
```
Enable URL rewriting module:
```
sudo lighttpd-enable-mod rewrite
sudo systemctl restart lighttpd
```

### Step 8: Configure WordPress
Create WordPress Configuration
```
cd /var/www/html/wordpress
sudo cp wp-config-sample.php wp-config.php
sudo nano wp-config.php
```

Update these lines with your database details:
```
define('DB_NAME', 'wordpress');
define('DB_USER', 'wpuser');
define('DB_PASSWORD', 'strong_password');
define('DB_HOST', 'localhost');
```
Generate and add security keys. Visit `https://api.wordpress.org/secret-key/1.1/salt/` and replace the placeholder keys in wp-config.php.

Set proper permissions:
```
sudo chown -R www-data:www-data /var/www/html/wordpress
sudo find /var/www/html/wordpress -type d -exec chmod 755 {} \;
sudo find /var/www/html/wordpress -type f -exec chmod 644 {} \;
```

### Step 9: Set Up Firewall
```
sudo apt install ufw -y
sudo ufw allow OpenSSH
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
sudo ufw enable
```

### Step 10: Complete WordPress Installation
Visit `http://your-server-ip` in your browser and follow the WordPress installation wizard:
1. Select language
2. Enter site title, username, password, and email
3. Click "Install WordPress"
4. Log in to admin panel at /wp-admin

### Step 11: Install SSL Certificate (Optional)
```
sudo apt install certbot -y
sudo systemctl stop lighttpd
sudo certbot certonly --standalone -d yourdomain.com -d www.yourdomain.com
```
Edit Lighttpd SSL configuration:
```
sudo nano /etc/lighttpd/conf-available/10-ssl.conf
```
Add:
```
$SERVER["socket"] == ":443" {
    ssl.engine = "enable"
    ssl.pemfile = "/etc/letsencrypt/live/yourdomain.com/fullchain.pem"
    ssl.privkey = "/etc/letsencrypt/live/yourdomain.com/privkey.pem"
}
```
Enable SSL module:
```
sudo lighttpd-enable-mod ssl
sudo systemctl start lighttpd
```

## Troublshooting
### PHP files downloading instead of executing
Check if FastCGI-PHP is enabled:
```
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
