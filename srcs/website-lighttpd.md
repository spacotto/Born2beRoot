# About Lighttpd
Lighttpd (pronounced "lighty") is a **lightweight, high-performance web server** designed for speed and low resource usage. It's ideal for high-traffic sites and **resource-constrained environments**.

## Installation
Debian/Ubuntu:
```
sudo apt update
sudo apt install lighttpd
```
RHEL/CentOS:
```
sudo yum install lighttpd
```
macOS:
```
brew install lighttpd
```

## Basic Configuration
The main configuration file is typically located at `/etc/lighttpd/lighttpd.conf`.

### Minimal Configuration
```
server.document-root = "/var/www/html"
server.port = 80
server.username = "www-data"
server.groupname = "www-data"

mimetype.assign = (
  ".html" => "text/html",
  ".txt" => "text/plain",
  ".jpg" => "image/jpeg",
  ".png" => "image/png",
  ".css" => "text/css",
  ".js" => "application/javascript"
)
```

### Common Directives
```
server.document-root    # Path to website files
server.port             # Port to listen on (default: 80)
server.bind             # IP address to bind to
server.errorlog         # Path to error log file
accesslog.filename      # Path to access log file
```

## Service Management
Start:
```
sudo systemctl start lighttpd
```
Stop:
```
sudo systemctl stop lighttpd
```
Restart:
```
sudo systemctl restart lighttpd
```
Enable on boot:
```
sudo systemctl enable lighttpd
```
Check status:
```
sudo systemctl status lighttpd
```

## Enabling Modules
Lighttpd uses a modular architecture. Modules are enabled in the configuration file.

Load a module:
```
server.modules = (
  "mod_access",
  "mod_alias",
  "mod_compress",
  "mod_redirect"
)
```
Common modules:
```
mod_rewrite         # URL rewriting
mod_redirect        # HTTP redirects
mod_compress        # Gzip compression
mod_fastcgi         # FastCGI support for PHP, Python, etc.
mod_accesslog       # Access logging
mod_auth            # Authentication
```

## Virtual Hosts
```
$HTTP["host"] == "example.com" {
  server.document-root = "/var/www/example.com"
  accesslog.filename = "/var/log/lighttpd/example.com-access.log"
}

$HTTP["host"] == "another.com" {
  server.document-root = "/var/www/another.com"
}
```

## SSL/TLS Configuration
```
$SERVER["socket"] == ":443" {
  ssl.engine = "enable"
  ssl.pemfile = "/etc/lighttpd/certs/server.pem"
  ssl.ca-file = "/etc/lighttpd/certs/ca.crt"
}
```

## URL Rewriting
Enable mod_rewrite and configure:
```
url.rewrite-once = (
  "^/(.*)\.php$" => "/index.php/$1"
)
```

## PHP Support with FastCGI
Enable `mod_fastcgi`:
```
fastcgi.server = ( ".php" =>
  ((
    "bin-path" => "/usr/bin/php-cgi",
    "socket" => "/tmp/php.socket",
    "max-procs" => 2,
    "bin-environment" => (
      "PHP_FCGI_CHILDREN" => "4",
      "PHP_FCGI_MAX_REQUESTS" => "10000"
    )
  ))
)
```

## Directory Listings
```
dir-listing.activate = "enable"
dir-listing.encoding = "utf-8"
```

## Access Control
```
$HTTP["remoteip"] == "192.168.1.0/24" {
  url.access-deny = ( "" )
}
```

## Testing Configuration
Before restarting, test your configuration:
```
sudo lighttpd -t -f /etc/lighttpd/lighttpd.conf
```

## Performance Tuning
```
server.max-connections = 1024
server.max-keep-alive-requests = 128
server.max-keep-alive-idle = 30
server.event-handler = "linux-sysepoll"
server.network-backend = "write"
```

## Common Issues
### Port already in use
Check if another service is using port 80 with: 
```
sudo netstat -tulpn | grep :80
```

### Permission denied
Ensure lighttpd user has read access to document root and write access to log directories

### Configuration syntax errors
Run the test command to identify issues

## Log Files
```
/var/log/lighttpd/error.log    # Error log
/var/log/lighttpd/access.log   # Access log
```
View logs in real-time:
```
sudo tail -f /var/log/lighttpd/error.log
```

## Additional Resources
- [Official documentation](https://redmine.lighttpd.net/projects/lighttpd/wiki)
- [Configuration examples](https://redmine.lighttpd.net/projects/lighttpd/wiki/Docs_Configuration)
