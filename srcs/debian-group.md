# About Groups & Users Management

## Create a User
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

## Create a Group
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

## Add a User to Group
```
sudo add <user> <group>
```
>[!TIP]
>Run the following command to check that the user was successfully added to the group.
>```
>getent group <group> <user>
>```

## Check Group Members List
You can check the users belonging to a specific group by running this command in the terminal:
```
getent group <group>
```
For example:
```
getent group sudo
```
Output example:
```
sudo:x:27:spacotto
```
>[!TIP]
>If you want to display only the list, you can run:
>```
>getent group sudo | cut -d: -f4
>```
