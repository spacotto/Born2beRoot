# About Password Policy Implementation
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
PASS_MAX_DAYS  30  # Users shall change the pw every 30 days
```

#### Minimum password age
Set the minimum number of days allowed between password changes:
```
PASS_MIN_DAYS  2  # Users shall wait at least 2 days before changing a password again
```

#### Expiration warning
Set the number of days a warning is given before a password expires:
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
minlen=10                           # The password must be at least 10 characters long
```

#### Characters
```
ucredit=-1 lcredit=-1 dcredit=-1    # The password must contain an uppercase letter, a lowercase letter, and a number
```

#### Consecutive Identical Characters
```
maxrepeat=3                          # The password must NOT contain more than 3 consecutive identical characters
```

#### Vocabulary Restrictions
```
reject_username                      # The password must NOT include the name of the user
```

#### Repetitions Restrictions
```
# difok=7                            # The password must have at least 7 characters that are not part of the former password
```
>[!IMPORTANT]
>The module will return error on failed check even if the user changing the password is root. This option is off by default which means that just the message about the failed check is printed but root can change the password anyway. **Note that root is not asked for an old password so the checks that compare the old and new password are not performed.** (Debian man)

#### Enforce Policy For Root
```
enforce_for_root                     # The password policy shall apply to root as well
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
Defaults  badpass_message="Invalid sudo password: try again."
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

## Resources
- [libpam-pwquality](https://packages.debian.org/trixie/libpam-pwquality)
- [man login.defs](https://manpages.debian.org/trixie/login.defs/login.defs.5.en.html)
- [man pam_pwquality](https://manpages.debian.org/testing/libpam-pwquality/pam_pwquality.8.en.html)
