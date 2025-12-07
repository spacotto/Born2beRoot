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

## Table Operations
- Create a table:
```
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(50) NOT NULL,
    email VARCHAR(100) UNIQUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```
- Show tables:
```
SHOW TABLES;
```
- Describe table structure:
```
DESCRIBE users;
```
- Modify a table:
```
ALTER TABLE users ADD COLUMN age INT;
ALTER TABLE users DROP COLUMN age;
ALTER TABLE users MODIFY COLUMN username VARCHAR(100);
```
- Delete a table:
```
DROP TABLE users;
```

## Data Manipulation
- Insert data:
```
INSERT INTO users (username, email) VALUES ('john', 'john@example.com');
INSERT INTO users (username, email) VALUES 
    ('alice', 'alice@example.com'),
    ('bob', 'bob@example.com');
```
- Select data:
```
SELECT * FROM users;
SELECT username, email FROM users WHERE id = 1;
SELECT * FROM users ORDER BY created_at DESC LIMIT 10;
```
- Update data:
```
UPDATE users SET email = 'newemail@example.com' WHERE id = 1;
```
- Delete data:
```
DELETE FROM users WHERE id = 1;
```

## Indexes
- Create an index:
```
CREATE INDEX idx_username ON users(username);
CREATE UNIQUE INDEX idx_email ON users(email);
```
- Show indexes:
```
SHOW INDEX FROM users;
```
- Remove an index:
```
DROP INDEX idx_username ON users;
```

## Backup and Restore
- Backup a database:
```
mysqldump -u username -p mydb > backup.sql
```
- Backup all databases:
```
mysqldump -u username -p --all-databases > all_backup.sql
```
- Restore a database:
```
mysql -u username -p mydb < backup.sql
```

## Configuration
The main configuration file is typically located at `/etc/mysql/mariadb.conf.d/50-server.cnf` on Linux.

### Key settings
- Controls which network interfaces MariaDB listens on (default: 127.0.0.1):
```
bind-address
```
- Maximum number of concurrent connections:
```
max_connections
```
- Memory allocated for InnoDB cache (set to 70-80% of RAM for dedicated servers):
```
innodb_buffer_pool_size
```
- Reload configuration:
```
sudo systemctl restart mariadb
```
