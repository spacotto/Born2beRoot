# About System Architecture
This section is dedicated to the first part of the **installation process**. Herein, I am going to explain how to attach the ISO of the chosen Debian distros and configure locals, network, users, and passwords. You can find the second part of the installation (aka the configuration of the storage architecture) in its dedicated section.

>[!IMPORTANT]
>Before starting, you need to get the [ISO](https://github.com/spacotto/Born2beRoot/blob/main/srcs/iso.md). You can download the ISO [here](https://cdimage.debian.org/debian-cd/current/amd64/iso-dvd/). I used the `debian-13.2.0-amd64-DVD-1.iso`. If you don't have much space, I recommend downloading it into the `tmp` folder.

## 1. Creating a New VM
### 1.1 Start the config process 
```
Open VirtualBox
Click on < Machine >
Click on < New >
```
![create-the-vm](https://github.com/spacotto/Born2beRoot/blob/main/imgs/vm000.png)

### 1.2 Configure VM name and OS:
```
VM Name    # The name you want to use for your VM (like a file name).
VM Folder  # The folder path where your VM is going to be placed.
ISO Image  # The ISO image of the OS.
```
[vm-name-and-os]

>[!WARNING]
>Concerning the `VM Folder`, make sure to have enough space to store you VM!

>[!CAUTION]
>Since we want to set up the VM ourselves, we need to **CHECK "Skip Unattended Installation."** In other VirtualBox version they changed from opt-in to opt-out. In the opt-out instance, you have to **UNCHECK "Proceed with Unattended Installation."**

## Configure Locals

## Configure Network

## Set Up Users & Passswords
