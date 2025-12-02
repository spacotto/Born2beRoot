# About Groups & Users Management

# Create a User
Run the following command in the terminal and write the desired username instead of <username>:
```
sudo adduser <username>
```
For example:
```
sudo adduser spacotto
```
>[!TIP]
>If you want to make sure the user was successfully created, run the same command. If the user was created without issues, you will see the following error message:
>```
>fatal: The user `xxx` already exists.   # You will see the username instead of xxx
>```

# Create a Group
Run the following command in the terminal and write the desired group name instead of <group>:
```
sudo addgroup <group>
```
For example:
```
sudo addgroup user42
```
>[!TIP]
>If you want to make sure the group was successfully created, run the same command. If the group was created without issues, you will see the following error message:
>```
>fatal: The group `xxx` already exists.    # You will see the group name instead of xxx
>```
