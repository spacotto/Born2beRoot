# About `sudo`
>[!IMPORTANT]
>`sudo` is a **shell command** on Unix-like operating systems that **enables a user to run a program with the security privileges of another user**, by default the **superuser**.

>[!NOTE]
>It originally stood for `superuser do`, as that was all it did, and this remains its most common usage. However, the official **Sudo project page** lists it as `su 'do'`. The current Linux manual pages define `su` as `substitute user`, making the modern meaning of sudo `substitute user, do`, because `sudo` can **run a command as other users as well** (not only `root`).

## 💻 Essential `sudo` Commands

| Command | Description |
| :--- | :--- |
| `sudo <command>` | Executes the specified `<command>` with root privileges (after prompting for the user's password). |
| `sudo -l` | Lists the commands the user is allowed (and forbidden) to run on the current host. |
| `sudo -v` | Extends the time limit for which you can run `sudo` without re-entering your password (a "keep-alive" for your credentials). |
| `sudo -k` | Invalidates the user's cached credentials. The next time `sudo` is used, the user will be prompted for their password. |
| `sudo -u <user> <command>` | Executes `<command>` as the specified `<user>` instead of root. |

---

## 🛠️ Installing `sudo` on Debian 13

If your Debian 13 system does not have `sudo` installed (e.g., if you set up the system without a regular user and only used the root account initially), you can install it using the root account with the following steps:

1.  **Log in as root:** Access the system console or SSH terminal and log in using the `root` username and password.

2.  **Update package lists:**
    ```bash
    apt update
    ```

3.  **Install the `sudo` package:**
    ```bash
    apt install sudo
    ```

4.  **Add your user to the `sudo` group** (replace `username` with your actual username):
    ```bash
    usermod -aG sudo username
    ```
    * The `-a` flag means "append."
    * The `-G` flag specifies the group to append to.
    * The `sudo` group grants users the permission to use the `sudo` command.

5.  **Reboot or log out and log back in:** For the group change to take effect for your user, you must log out of your current session and log back in, or simply **reboot** the system:
    ```bash
    reboot
    ```

After logging back in, you should be able to execute administrative commands using `sudo`.
