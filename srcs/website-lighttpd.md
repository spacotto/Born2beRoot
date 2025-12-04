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
