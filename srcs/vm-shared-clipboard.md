# Sharing Clipboard Between Ubuntu Host and Debian VM in VirtualBox

## Prerequisites
- VirtualBox 7.0.20 installed on Ubuntu
- Debian VM running in VirtualBox
- Guest Additions installed in the Debian VM

## Sharing Instructions
### Step 1: Install Guest Additions (if not already installed)
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
