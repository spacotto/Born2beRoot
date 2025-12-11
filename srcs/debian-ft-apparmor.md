# About AppArmor (Debian)
**AppArmor** is a **Mandatory Access Control (MAC) security system** for Linux that **restricts programs' capabilities** using per-program profiles. It's enabled by default on Debian 10 and later. AppArmor **confines applications to a limited set of resources**, preventing them from accessing files, network ports, or system capabilities they shouldn't need. Each confined program has a **security** profile that defines what it can access.

## Installation
AppArmor comes **pre-installed** on modern Debian systems. Use this command to install utilities if needed:
```
sudo apt install apparmor-utils apparmor-profiles apparmor-profiles-extra
```

## Status
Use this command to check if it's running:
```
sudo systemctl status apparmor
```
Alternative command:
```
sudo aa-status
```
>[!NOTE]
>This shows loaded profiles and their enforcement modes.

## Profile Modes
- **Enforce mode.** Actively blocks policy violations and logs them.
- **Complain mode.** Allows violations but logs them for testing.
- **Unconfined.** No restrictions applied.

## Common Commands
- Put a profile in complain mode.
```
sudo aa-complain /path/to/program
```

- Put a profile in enforce mode.
```
sudo aa-enforce /path/to/program
```

- Disable a profile.
```
sudo aa-disable /path/to/program
```

- Reload all profiles.
```
sudo systemctl reload apparmor
```

## Profile Locations
- Active profiles
```
/etc/apparmor.d/
```

- Disabled profiles (symlinked here)
```
/etc/apparmor.d/disable/
```

- Additional available profiles
```
/usr/share/apparmor/extra-profiles/
```

## Creating or Modifying Profiles
- Generate a basic profile for an application:
```
sudo aa-genprof /path/to/program
```
This interactive tool runs the program, monitors its behaviour, and helps create rules.

- Update an existing profile:
```
sudo aa-logprof
```
This reviews log entries and suggests profile modifications.

- Edit profiles manually:
```
sudo nano /etc/apparmor.d/profile-name
```

- After editing, reload:
```
sudo systemctl reload apparmor
```

## Basic Profile Syntax
Profiles define allowed access. Common rules include:
```
/path/to/file r,           # read access
/path/to/file w,           # write access
/path/to/file rw,          # read and write
/path/to/file x,           # execute
/path/to/dir/** r,         # recursive read in directory
```

Capabilities grant specific privileges:
```
capability net_bind_service,  # bind to ports < 1024
capability dac_override,      # bypass file permissions
```

## Troubleshooting
- View AppArmor denials in the logs:
```
sudo dmesg | grep apparmor
sudo journalctl | grep AppArmor
```

- Or check audit logs:
```
sudo grep apparmor /var/log/audit/audit.log
```

>[!TIP]
>If a program breaks after confinement, switch to complain mode, reproduce the issue, then use `aa-logprof` to update the profile.

## Disable AppArmor
>[!CAUTION]
>It is NOT recommended to disable AppArmor!

For a single profile, use:
```
aa-disable
```

To disable completely:
```
sudo systemctl stop apparmor
sudo systemctl disable AppArmor
```
Or add `apparmor=0` to kernel boot parameters in `/etc/default/grub`, then run `sudo update-grub`.

## Best Practices
- Start new profiles in **complain mode** to avoid breaking functionality. 
- Use the **built-in profiles** from `apparmor-profiles` and `apparmor-profiles-extra` packages when available.
- **Review logs regularly** to catch issues early.
- **Test thoroughly before moving profiles** to enforce mode in production.

>[!NOTE]
>AppArmor provides strong security with minimal performance impact when profiles are properly configured.

## Resources
- [AppArmor](https://wiki.debian.org/AppArmor)
