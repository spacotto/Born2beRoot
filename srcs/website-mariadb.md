# About MariaDB
MariaDB is an open-source relational database management system (RDBMS) that forked from MySQL in 2009. It's designed to be a drop-in replacement for MySQL with improved performance, additional features, and a commitment to remaining open source.

## Installation (Ubuntu/Debian)
```
sudo apt update
sudo apt install mariadb-server
sudo mysql_secure_installation
```

## Basic Operations
- Starting and Stopping:
```
sudo systemctl start mariadb
sudo systemctl stop mariadb
sudo systemctl restart mariadb
```
- Connecting to MariaDB:
```
mysql -u username -p
```

## Database Management
- Create a database:
```
CREATE DATABASE mydb;
```
- List databases:
```
SHOW DATABASES;
```
- Select a database:
```
USE mydb;
```
- Delete a database:
```
DROP DATABASE mydb;
```

## User Management
- Create a user:
```
CREATE USER 'username'@'localhost' IDENTIFIED BY 'password';
```
- Grant privileges:
```
GRANT ALL PRIVILEGES ON mydb.* TO 'username'@'localhost';
FLUSH PRIVILEGES;
```
- Show user privileges:
```
SHOW GRANTS FOR 'username'@'localhost';
```
- Remove a user:
```
DROP USER 'username'@'localhost';
```
