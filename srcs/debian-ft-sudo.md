# About `sudo`
>[!IMPORTANT]
>`sudo` is a **shell command** on Unix-like operating systems that **enables a user to run a program with the security privileges of another user**, by default the **superuser**.

>[!NOTE]
>It originally stood for `superuser do`, as that was all it did, and this remains its most common usage. However, the official **Sudo project page** lists it as `su 'do'`. The current Linux manual pages define `su` as `substitute user`, making the modern meaning of sudo `substitute user, do`, because `sudo` can **run a command as other users as well** (not only `root`).

## Install `sudo` on Debian 13
1. **Log in as root.** Access the system console or SSH terminal and log in using the `root` username and password. If you are connected with another user, you can switch to `root` by running the following command in the terminal:
```
su  # You will have to enter the root password.
```

2. **Install the `sudo` package.**
```
apt install sudo
```

3. **Reboot or log out and log back in.** For the group change to take effect for your user, you must log out of your current session and log back in, or simply **reboot** the system:
```
sudo reboot    # sudo or su > reboot since root can't reboot
```

### Installation Troubleshooting
You might get an error like this one:
```
Media change: please insert the disc labeled 'xxx' in the drive 'path' and press [Enter]
```
If this happens, switch to root (if you didn't already) and open the following file:
```
nano /etc/apt/sources.list 
```
Then, hide the 1st line with `#`, and add the following line:
```
deb https://deb.debian.org/debian/ trixie contrib main non-free-firmware
```

## Essential `sudo` Commands
>[!IMPORTANT]
>Check `man sudo` for the complete list of commands.

Add user to `sudo` group as `root`
```
sudo usermod -aG sudo username
```

Execute the specified `<command>` with root privileges (after prompting for the user's password):
```
sudo <command>
```

List the commands the user is allowed (and forbidden) to run on the current host:
```
sudo -l
```

Print the sudo version string as well as the version string of any configured plugins:q
```
sudo -V
```

Extend the time limit for which you can run `sudo` without re-entering your password (a "keep-alive" for your credentials):
```
sudo -v
``` 

Invalidate the user's cached credentials:
```
sudo -k    # The next time sudo is used, the user will be prompted for their password
```

Execute `<command>` as the specified `<user>` instead of `root`:
```
sudo -u <user> <command>
```
