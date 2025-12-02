# About Network Configuration
This is the second OS installation step.

## 1. Configure Hostname
>[!NOTE]
>The hostname is the **name of your computer on a network**.

![config-hostname](https://github.com/spacotto/Born2beRoot/blob/main/imgs/vm010.png)

## 2. Configure Domain Name
>[!NOTE]
>The domain name is the network domain your system belongs to.

![config-domain](https://github.com/spacotto/Born2beRoot/blob/main/imgs/vm011.png)

## 3. Configure Root
![root-pw](https://github.com/spacotto/Born2beRoot/blob/main/imgs/vm012.png)
>[!TIP]
>You can simulate the random strong password generation by running this command in the terminal:
>```
>< /dev/urandom tr -dc "[:alnum:]" | fold -w 16 | head -n 1 > root-password.txt
>```
>
>Output example:
>```
>gl0pmJlptF5p21O9
>```

>[!NOTE]
>Find out more about Strong Password Policy & Generation [here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/password-policy.md).

## 4. Configure User
>[!IMPORTANT]
>Besides `root`, you need to create at least one user: you. To do so, you need to provide your name and last name, choose a username, and set up a password account.

### Name & Last Name
![name](https://github.com/spacotto/Born2beRoot/blob/main/imgs/vm013.png)

### Username
![username](https://github.com/spacotto/Born2beRoot/blob/main/imgs/vm014.png)

### Password
![password](https://github.com/spacotto/Born2beRoot/blob/main/imgs/vm015.png)
>[!TIP]
>You can simulate the random strong password generation by running this command in the terminal:
>```
>< /dev/urandom tr -dc "[:alnum:]" | fold -w 16 | head -n 1 > root-password.txt
>```
>
>Output example:
>```
>niGRMvKP3NidHMGU
>```

>[!NOTE]
>Find out more about Strong Password Policy & Generation [here](https://github.com/spacotto/Born2beRoot/blob/main/srcs/password-policy.md).
