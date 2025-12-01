# About Grub boot loader

![grub](https://github.com/spacotto/Born2beRoot/blob/main/imgs/vm083.png)

![grub](https://github.com/spacotto/Born2beRoot/blob/main/imgs/vm084.png)

>[!IMPORTANT]
>GRUB (GRand Unified Bootloader) is the boot loader used by Debian and most Linux distributions. It **loads the OS kernel when your computer starts**.

## Key Files and Directories

```
/boot/grub/grub.cfg  # Main configuration file (auto-generated, don't edit directly)
```

```
/etc/default/grub    # User configuration settings
```

```
/etc/grub.d/          # Scripts that generate grub.cfg
```

```
/boot/                # Contains kernel images and initrd files
```

