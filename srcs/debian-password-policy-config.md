# About Password Policy Configuration
>[!IMPORTANT]
>[Here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/password-policy.md) you can find the details concerning the Strong Password Policy.

## Password Expiration Configuration
### 1. Open login definitions file
```
nano /etc/login.defs
```

### 2. Setup parameters
#### Expiration date
Set the number of days after which the users shall change their passwords:
```
PASS_MAX_DAYS  xxx
```
For example:
```
PASS_MAX_DAYS  30  # Users shall change the pw every 30 days
```

#### Minimum password age
Set the minimum number of days allowed between password changes:
```
PASS_MIN_DAYS  xxx
```
For example:
```
PASS_MIN_DAYS  2  # Users shall wait at least 2 days before changing a password again
```

#### Expiration warning
Set the number of days a warning is given before a password expires:
```
PASS_WARN_AGE  xxx
```
For example:
```
PASS_WARN_AGE  7  # The user will receive a warning 7 days before the password expiration date
```

## Password Complexity Configuration
### 1. Install password quality library
```
sudo apt install libpam-pwquality
```

### 2. Open PAM configuration file
```
nano /etc/pam.d/common-password
```

### 3. Set up password validity parameters
You shall add the following additional parameters on the line (after retry 3):
```
password  requisite  pam_pwquality.so retry=3
```

>[!TIP]
>If you want to test the parameters, I recommend changing the last parameter from `retry=3` to `retry=9999`.

#### Length
```
minlen=10  # The password must be at least 10 characters long
```

#### Characters
```
# The password must contain an uppercase letter, a lowercase letter, and a number
```

#### Consecutive identical characters
```
# The password must NOT contain more than 3 consecutive identical characters
```

#### Vocabulary restrictions
```
# The password must NOT include the name of the user
```


## `sudo` Configuration
### 1. Switch to Root
```
su
```

### 2. Create Log Folder
For example:
```
mkdir /var/log/sudo
```

### 3. Create Configuration files
```
nano /etc/sudoers.d/sudo_config
```

### 4. Setup Configuration files
#### Incorrect password attempts
Authentication is limited to 3 attempts in the event of an incorrect password:
```
Defaults  passwd_tries=3
```

#### Wrong sudo password error message
An error message occurs when a wrong password is entered when using sudo:
```
Defaults  error_message="Invalid sudo password: try again."
```

#### sudo commands log
Archive each action using sudo (both inputs and outputs) in a dedicated log file:
```
Defaults  iolog_dir="/var/log/sudo"
Defaults  logfile="/var/log/sudo/sudo_config"
Defaults  log_input, log_output
```
#### TTY mode
For security reasons, TTY mode shall be enabled:
```
Defaults  requiretty
```

#### Path restriction
For security reasons, the paths used by `sudo` shall be restricted
```
Defaults  secure_path="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin"
```
