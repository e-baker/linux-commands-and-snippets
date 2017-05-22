Common Linux Commands & Snippets
======

CRUD Users
------

## Adding a Regular User


## Adding an SFTP User
```bash
useradd -d {/path/to/home} -G apache {username}
```

## Showing All Local Users

```bash
**cut -d: -f1 /etc/passwd**
```

This comand just shows the list of user names for local users. If you want to see more details, such as groups, shells, home directories, etc then use this: 

```bash
**cat /etc/passwd**
```