# Sharing Clipboard Between Ubuntu Host and Debian VM in VirtualBox

## Prerequisites
- VirtualBox 7.0.20 installed on Ubuntu
- Debian VM running in VirtualBox

## Step 1: Install Guest Additions (if not already installed)
In your Debian VM:
```
sudo apt update
sudo apt install build-essential dkms linux-headers-$(uname -r)
```
From VirtualBox menu: 
```
Devices → Insert Guest Additions CD Image
```
Mount and install:
```
sudo mount /dev/cdrom /mnt
sudo /mnt/VBoxLinuxAdditions.run
sudo reboot
```

## Step 2: Enable Shared Clipboard
Configure while VM is running:
1. Go to Devices → Shared Clipboard
2. Select your preferred mode:
  - Bidirectional - copy/paste works both ways
  - Host to Guest - paste from Ubuntu to Debian only
  - Guest to Host - paste from Debian to Ubuntu only

Configure while VM is powered off:
1. Select your Debian VM in VirtualBox Manager
2. Click Settings → General → Advanced
3. Set Shared Clipboard dropdown to Bidirectional
4. Click OK
5. Start the VM

## Step 3: Verify It Works
Copy text on Ubuntu host and paste in Debian VM or vice versa

## Troubleshooting
### Verify Guest Additions are running in the VM
```
lsmod | grep vbox
```
You should see `vboxguest` listed.

### Restart the VBoxClient processes in the VM
```
killall VBoxClient
VBoxClient --clipboard
```

### Ensure the service is running
```
sudo systemctl status vboxadd-service
```

### Reboot the VM after any Guest Additions installation or update
