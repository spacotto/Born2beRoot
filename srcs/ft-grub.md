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

## Recovery and Troubleshooting
### Boot from GRUB Command Line
If GRUB drops to a command line, you can boot manually:
```
grub> ls                              # List available partitions
grub> set root=(hd0,1)                # Set your boot partition
grub> linux /vmlinuz root=/dev/sda1
grub> initrd /initrd.img
grub> boot
```

### Boot from Live USB and Reinstall GRUB
1. Boot from Debian Live USB

2. Mount your root partition:
```
sudo mount /dev/sda1 /mnt
sudo mount --bind /dev /mnt/dev
sudo mount --bind /proc /mnt/proc
sudo mount --bind /sys /mnt/sys
```

3. Chroot and reinstall:
```
sudo chroot /mnt
grub-install /dev/sda
update-grub
exit
```

4. Reboot

### Check GRUB Version
```
grub-install --version
```

### Custom Menu Entries
To add custom entries, create a file in `/etc/grub.d/`:
```
sudo nano /etc/grub.d/40_custom
```

Example custom entry:
```
#!/bin/sh
exec tail -n +3 $0
menuentry "My Custom Linux" {
    set root='hd0,1'
    linux /vmlinuz-custom root=/dev/sda1
    initrd /initrd.img-custom
}
```
Make it executable and update:
```
sudo chmod +x /etc/grub.d/40_custom
sudo update-grub
```

## Good Practices
- Always run `sudo update-grub` after making configuration changes.
- Never directly edit `/boot/grub/grub.cfg`: your changes will be overwritten.
- Use `/dev/sdX` (disk) for grub-install, not `/dev/sdX1` (partition).
- Keep backups before making major changes to boot configuration.
- If dual-booting, `os-prober` must be enabled to detect other operating systems.
