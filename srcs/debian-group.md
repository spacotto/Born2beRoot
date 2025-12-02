# About Groups & Users Management

## Create User
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

## Remove User
```
sudo deluser <username> 
```
For example:
```
sudo deluser spacotto
```
>[!TIP]
>If you want to make sure the user was successfully removed, run the same command. If the user was removed without issues, you will see the following error message:
>```
>fatal: The user `xxx` does not exist.   # You will see the username instead of xxx
>```

## Create Group
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

## Remove Group
```
sudo delgroup <group> 
```
For example:
```
sudo delgroup user42
```
>[!TIP]
>If you want to make sure the group was successfully removed, run the same command. If the group was removed without issues, you will see the following error message:
>```
>warn: The group `xxx` does not exist.   # You will see the group name instead of xxx
>```

## Add User to Group
```
sudo add <user> <group>
```
>[!TIP]
>Run the following command to check that the user was successfully added to the group.
>```
>getent group <group> <user>
>```

## Check User Groups
You can check the groups a user belongs to by running the following command in the terminal:
```
groups <username>
```
For example:
```
groups spacotto
```
Output example:
```
spacotto: spacotto cdrom floppy sudo audio dip video plugdev users natdev user42
```

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
