# About SSH
**Secure Shell (SSH)** is a cryptographic network protocol used to operate network services securely over an unsecured network. The most common applications are **remote command-line login** and **remote command execution**. It provides strong authentication and secure encrypted communication.

---

### Installation on Debian 13

SSH is typically installed and configured in two parts: the **server** (where you want to connect to) and the **client** (the machine you are connecting *from*).

#### 1. Installing the SSH Client (for connecting to other machines)

The client is usually installed by default on Debian. If it's not, you can install it using the following command:

```bash
sudo apt update
sudo apt install openssh-client

2. Installing the SSH Server (to allow remote connections to your machine)
To allow other machines to connect to your Debian 13 system, install the server package, which includes the sshd daemon:
sudo apt update
sudo apt install openssh-server

The SSH service will start automatically after installation. You can check its status with:
sudo systemctl status ssh

Basic Usage
The standard command structure for connecting is:
ssh [username]@[hostname_or_IP_address]

 * username: The account you want to log into on the remote machine.
 * hostname_or_P_address: The network address of the remote machine.
Example:
ssh user_alice@192.168.1.10

When connecting for the first time, you'll be prompted to verify and accept the remote host's key fingerprint. This adds the host to your $HOME/.ssh/known_hosts file.
⚙️ Key Concepts 
 * Port 22: The standard TCP port that the SSH daemon (sshd) listens on. This can be changed for security reasons in the server's configuration file.
 * Authentication: SSH supports two main methods:
   * Password Authentication: The user provides their system password.
   * Public Key Authentication: This is the more secure and recommended method. It involves a pair of keys:
     * Private Key: Kept secret on the client machine.
     * Public Key: Stored on the server in the ~/.ssh/authorized_keys file.
Generating an SSH Key Pair
Use the ssh-keygen utility on your client machine to create the key pair:
ssh-keygen -t ed25519

 * You'll be prompted for a passphrase. Always use a strong passphrase to protect your private key.
Copying the Public Key to the Server
The easiest way to set up key-based login is with ssh-copy-id:
ssh-copy-id user_alice@192.168.1.10

This command securely transfers your public key to the remote server and configures the authorized_keys file. You will need to enter your password one last time to complete this process.

🛡️ Essential Security (Server Configuration)
The main configuration file for the SSH server is located at /etc/ssh/sshd_config.
| Setting | Recommended Value | Description |
|---|---|---|
| PermitRootLogin | no | Prevents direct login as the root user. Connect with a regular user and then use su or sudo. |
| PasswordAuthentication | no | Disables password-based login after you have set up public key authentication. |
| Port | [Non-standard port] | Changing the port from 22 helps reduce automated attack attempts (script kiddies). |
Remember to restart the SSH service after any configuration changes:
sudo systemctl restart ssh
