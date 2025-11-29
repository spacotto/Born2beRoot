# About AppArmor (Debian)
**AppArmor** is a **Mandatory Access Control (MAC) security system** for Linux that **restricts programs' capabilities** using per-program profiles. It's enabled by default on Debian 10 and later.

>[!IMPORTANT]
>[Here](https://wiki.debian.org/AppArmor) you can find the official Debian documentation about AppArmor.

AppArmor **confines applications to a limited set of resources**, preventing them from accessing files, network ports, or system capabilities they shouldn't need. Each confined program has a **security** profile that defines what it can access.

## Installation
AppArmor comes **pre-installed** on modern Debian systems. Use this command to install utilities if needed:
```
sudo apt install apparmor-utils apparmor-profiles apparmor-profiles-extra
```

## Status
Use this command to check if it's running:
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
- View status and loaded profiles.
```
sudo aa-status
```

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
capability dac_override,       # bypass file permissions
```
