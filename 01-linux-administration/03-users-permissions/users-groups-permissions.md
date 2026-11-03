# Linux Users, Groups and Permissions

## 1. Introduction

Linux is a multi-user operating system. Multiple users can access the same server while having different permissions and levels of access.

Linux uses users, groups and permissions to control:

- Who can access files and directories.
- Who can modify files.
- Who can execute programs.
- Which users can administer the system.
- How teams share resources securely.

Understanding users, groups and permissions is essential for Linux administration, cloud infrastructure and DevOps engineering.

## 2. Linux User Accounts

Linux supports different types of user accounts.

### Root user

The root account is the superuser. It has administrative privileges and can perform almost any operation on the system.

Example prompt:

```
root@vps3652394:~#
```

The `#` symbol indicates a root shell.

### Regular users

Regular users have individual accounts and normally operate with restricted permissions.

Examples:

- developer1
- developer2
- ubuntu

### System users

System users are generally created to run services and applications.

Examples include accounts used by web servers, databases and other background services.

## 3. Identifying Users

Useful commands for inspecting Linux users include:

```bash
whoami
```

Displays the current username.

```bash
id
```

Displays the current user's UID, primary group and supplementary groups.

```bash
who
```

Shows users currently logged into the system.

```bash
cat /etc/passwd
```

Displays user account information.

```bash
cat /etc/group
```

Displays group information.

The `/etc/shadow` file stores password-related account information and is restricted to privileged users. Avoid exposing its contents.

## 4. Creating Users

The `adduser` command creates a new user account.

Example:

```bash
adduser developer1
```

Create another user:

```bash
adduser developer2
```

Check the accounts:

```bash
id developer1
id developer2
```

Switch to another user:

```bash
su - developer1
```

The `-` starts a login shell and loads that user's environment.

Return to the previous account:

```bash
exit
```

## 5. Linux Groups

Groups allow administrators to manage permissions for multiple users collectively.

Instead of assigning permissions individually, users can be placed into a shared group.

For example, a development team can have a group called `developers`.

### Create a group

```bash
groupadd developers
```

### Add users to the group

```bash
usermod -aG developers developer1
usermod -aG developers developer2
```

The options mean:

- `-a`: Append the group without removing existing supplementary groups.
- `-G`: Specify supplementary groups.

The `-a` option is important. Using `-G` without `-a` can replace existing supplementary group memberships.

### Verify group membership

```bash
groups developer1
groups developer2
```

Or:

```bash
id developer1
id developer2
```

### Practical output

The following was obtained during the practical exercise:

```
uid=1001(developer1) gid=1001(developer1) groups=1001(developer1),100(users),1000(developers)

uid=1002(developer2) gid=1002(developer2) groups=1002(developer2),100(users),1000(developers)
```

Both users are members of the `developers` group.

This makes it possible to manage their shared access through one group.

## 6. Linux File Permissions

Linux uses three basic permission types:

| Permission | Symbol | Meaning |
|---|---|---|
| Read | r | View file contents |
| Write | w | Modify file contents |
| Execute | x | Execute a file or access a directory |

Permissions are assigned to three categories:

| Category | Symbol | Meaning |
|---|---|---|
| User | u | File owner |
| Group | g | Members of the assigned group |
| Others | o | Everyone else |

### Understanding permission output

Example:

```
-rwxr-xr--
```

Breakdown:

- `-`: Regular file.
- `rwx`: Owner can read, write and execute.
- `r-x`: Group can read and execute.
- `r--`: Others can only read.

For directories, the first character is `d` instead of `-`.

## 7. Numeric Permissions

Linux also supports numeric permission notation.

Each permission has a numeric value:

| Permission | Value |
|---|---|
| Read (r) | 4 |
| Write (w) | 2 |
| Execute (x) | 1 |

Values are added together.

| Number | Permissions |
|---|---|
| 7 | rwx |
| 6 | rw- |
| 5 | r-x |
| 4 | r-- |
| 0 | --- |

### Common permission combinations

**755** — `rwxr-xr-x`

Owner has full permissions. Group and others can read and execute.

**644** — `rw-r--r--`

Owner can read and write. Group and others can only read.

**700** — `rwx------`

Only the owner has access.

**600** — `rw-------`

Only the owner can read and write.

**775** — `rwxrwxr-x`

Owner and group have full permissions. Others can read and execute.

## 8. Changing Permissions with chmod

The `chmod` command changes file and directory permissions.

Create a test directory:

```bash
mkdir -p ~/linux-lab/permissions
touch ~/linux-lab/permissions/backup.sh
```

Inspect its permissions:

```bash
ls -l ~/linux-lab/permissions/
```

Give the owner execute permission:

```bash
chmod u+x ~/linux-lab/permissions/backup.sh
```

Set numeric permissions:

```bash
chmod 755 ~/linux-lab/permissions/backup.sh
```

Change to read/write for the owner and read-only for others:

```bash
chmod 644 ~/linux-lab/permissions/backup.sh
```

Restrict access to the owner:

```bash
chmod 700 ~/linux-lab/permissions/backup.sh
```

Verify:

```bash
ls -l ~/linux-lab/permissions/backup.sh
```

## 9. Changing Ownership with chown

The `chown` command changes the owner and optionally the group assigned to a file or directory.

Change the file owner:

```bash
chown developer1 ~/linux-lab/permissions/backup.sh
```

Change both owner and group:

```bash
chown developer1:developers ~/linux-lab/permissions/backup.sh
```

Verify:

```bash
ls -l ~/linux-lab/permissions/backup.sh
```

### Difference between chmod and chown

| Command | Purpose |
|---|---|
| `chmod` | Changes permissions |
| `chown` | Changes ownership |
| `chgrp` | Changes group ownership |

These commands are important when managing application files, deployment directories and shared server resources.

## 10. Sudo and Administrative Privileges

`sudo` allows authorized users to execute commands with elevated privileges.

Check the current user's privileges:

```bash
sudo -l
```

On Ubuntu, users can be added to the `sudo` group:

```bash
usermod -aG sudo developer1
```

Group membership changes generally require a new login session to take effect.

Always grant administrative privileges carefully.

## 11. Practical Lab: Shared Development Directory

### Scenario

Imagine a company has two developers who need access to a shared development directory.

Instead of configuring permissions separately for each user, we can create a group and assign the directory to that group.

### Step 1: Create the group

```bash
groupadd developers
```

### Step 2: Create users

```bash
adduser developer1
adduser developer2
```

### Step 3: Add both users to the group

```bash
usermod -aG developers developer1
usermod -aG developers developer2
```

### Step 4: Create a shared directory

```bash
mkdir -p /opt/development
```

### Step 5: Assign ownership

```bash
chown root:developers /opt/development
```

This assigns:

- Owner: root
- Group: developers

### Step 6: Configure permissions

```bash
chmod 2770 /opt/development
```

The permission value `2770` consists of:

- `2`: Setgid bit.
- `7`: Owner has read, write and execute.
- `7`: Group has read, write and execute.
- `0`: Others have no permissions.

### Understanding the setgid bit

The setgid bit on a directory causes new files and subdirectories created inside it to inherit the directory's group.

This is useful when multiple developers work inside the same directory.

### Step 7: Verify the configuration

```bash
ls -ld /opt/development
```

Actual practical output:

```
drwxrws--- 2 root developers 4096 Nov  3 12:25 /opt/development
```

This confirms:

- The directory owner is `root`.
- The assigned group is `developers`.
- The group has full permissions.
- Other users have no permissions.
- The setgid bit is enabled.

## 12. Verifying Group Inheritance

A test file was inspected using:

```bash
ls -l /opt/development/
```

Actual output:

```
-rw-r--r-- 1 root developers 0 Nov  3 12:30 test-file.txt
```

This confirms that the file belongs to the `developers` group.

The file's owner is `root`, however, so this output alone does not establish which user created it.

**Important distinction:** Setgid controls group inheritance. It does not automatically make every new file group-writable.

The default permissions of new files are also affected by the user's `umask`. Default ACLs can be configured when a team needs consistent shared write access.

## 13. Real-World Applications

These concepts are used extensively in infrastructure and DevOps environments.

### Application deployment

A deployment directory can be assigned to a dedicated application user and group.

### Team collaboration

Multiple developers can share access to a project directory through group permissions.

### Server security

Sensitive files can be restricted to authorized users.

For example:

```bash
chmod 600 private-key
```

### Web server administration

Web server processes often run under dedicated service accounts with controlled access to application files.

### Automation

Deployment scripts and configuration management tools frequently use `chown` and `chmod` to establish the correct ownership and permissions.

## 14. Security Best Practices

1. Avoid using the root account for routine operations.
2. Give users only the permissions they require.
3. Avoid using `chmod 777` as a general solution.
4. Use groups to manage shared access.
5. Protect SSH private keys and sensitive configuration files.
6. Be careful when changing ownership of production application directories.
7. Review administrative privileges regularly.
8. Test permission changes in a safe environment before applying them to production.

## 15. Useful Commands Reference

| Command | Description |
|---|---|
| `whoami` | Display current user |
| `id` | Display user and group IDs |
| `who` | Show logged-in users |
| `adduser username` | Create a user |
| `groupadd groupname` | Create a group |
| `usermod -aG group user` | Add user to supplementary group |
| `groups username` | Display group membership |
| `su - username` | Switch user |
| `chmod 755 file` | Change permissions |
| `chown user file` | Change file owner |
| `chown user:group file` | Change owner and group |
| `chgrp group file` | Change group ownership |
| `sudo -l` | List allowed sudo commands |
| `ls -l` | Display file permissions |
| `ls -ld directory` | Display directory permissions |

## Conclusion

Linux users, groups and permissions form a fundamental part of server security and administration.

Understanding how to create users, organize groups, assign ownership and configure permissions makes it easier to manage multi-user environments.

These skills are essential when working with Linux servers, cloud infrastructure, application deployments and DevOps automation.
