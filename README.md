Common Linux Commands & Snippets
======

CRUD Users
------

## Adding a User with an SSH Key

The most **secure** way to create a user is using a public/private key pair. This is the code to go that route:

1. We'll add the user first.
```bash
adduser {username} --disabled-password
```

2. You'll need to change into that user's account so files have the correct ownership.

```bash
su - {username}
```
3. Create a `.ssh` directory and change permissions to 700 (only the owner can read/write):
```bash
mkdir .ssh
chmod 700 .ssh
```

4. Create the file `authorized_keys` so there is a list to compare the user's key with:
```bash
touch .ssh/authorized_keys
chmod 600 .ssh/authorized_keys
```

5. Paste the user's key into the `authorized_keys` file. If they don't already have a key, you can see the instructions on [how to create an ssh key](# "How to Create an SSH Key") below then come back.

```bash
echo "{public key from ssh-rsa through the end of the comment}" > .ssh/authorized_keys
```

## Adding an SFTP User
```bash
useradd -d {/path/to/home} -G apache {username}
```

## Showing All Local Users

```bash
cut -d: -f1 /etc/passwd
```

This comand just shows the list of user names for local users. If you want to see more details, such as groups, shells, home directories, etc then use this: 

```bash
cat /etc/passwd
```