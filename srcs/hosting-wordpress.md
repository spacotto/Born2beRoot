# About Hosting WordPress on Debian VM
**Prerequisites:**
- Debian VM with `root` or `sudo` access
- Domain name (optional, but recommended)
- Basic command line knowledge

## Step 1: Update System
```
sudo apt update
sudo apt upgrade -y
```

## Step 2: Install Lighttpd
```
sudo apt install lighttpd -y
sudo systemctl enable lighttpd
sudo systemctl start lighttpd
```

## Step 3: Install MariaDB
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

## Step 4: Install PHP
```
sudo apt install php-fpm php-mysql php-curl php-gd php-mbstring php-xml php-xmlrpc php-zip php-imagick -y
sudo systemctl enable php8.2-fpm
sudo systemctl start php8.2-fpm
```
>[!NOTE]
>PHP version may vary (8.1, 8.2, etc.). Adjust commands accordingly.
