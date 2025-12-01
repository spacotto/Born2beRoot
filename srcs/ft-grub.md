# About Grub boot loader

![grub](https://github.com/spacotto/Born2beRoot/blob/main/imgs/vm083.png)

![grub](https://github.com/spacotto/Born2beRoot/blob/main/imgs/vm084.png)

>[!IMPORTANT]
>GRUB (GRand Unified Bootloader) is the boot loader used by Debian and most Linux distributions. It **loads the OS kernel when your computer starts**.

## Key Files and Directories

- Main configuration file
```
/boot/grub/grub.cfg  # Auto-generated, don't edit directly
```

- User configuration settings
```
/etc/default/grub
```

- Scripts that generate grub.cfg
```
/etc/grub.d/
```

- Contains kernel images and initrd files
```
/boot/
```

## Basic Configuration
### Edit GRUB Settings
1. Open the configuration file
```
sudo nano /etc/default/grub
```

2. Common settings
```
GRUB_TIMEOUT=5                               # Boot menu timeout in seconds
GRUB_DEFAULT=0                               # Default boot entry (0 = first entry)
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"    # Kernel parameters
GRUB_CMDLINE_LINUX=""                        # Additional kernel parameters
```

3. Apply changes
```
sudo update-grub
```

### Useful GRUB_DEFAULT Options
```
GRUB_DEFAULT=0                                                         # Boot first menu entry
GRUB_DEFAULT=saved                                                     # Remember last booted entry
GRUB_DEFAULT="Advanced options>Debian GNU/Linux, with Linux 6.1.0-10"  # Specific entry by name
```

## Common Tasks
### Update GRUB Configuration
After editing `/etc/default/grub` or installing a new kernel:
```
sudo update-grub
```

### Install/Reinstall GRUB
To install GRUB to a disk (e.g., /dev/sda):
```
sudo grub-install /dev/sda
sudo update-grub
```

### List Available Boot Entries
```
grep menuentry /boot/grub/grub.cfg
```

### Change Boot Order
Edit `/etc/default/grub` and set `GRUB_DEFAULT` to the desired entry number (counting from 0), then run:
```
sudo update-grub
```

### Hide GRUB Menu
To skip the boot menu and boot immediately:
```
GRUB_TIMEOUT=0
GRUB_TIMEOUT_STYLE=hidden
```

### Show More Verbose Boot
Remove "quiet" and "splash" from `GRUB_CMDLINE_LINUX_DEFAULT`:
```
GRUB_CMDLINE_LINUX_DEFAULT=""
```
