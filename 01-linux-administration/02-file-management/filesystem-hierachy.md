# Linux Filesystem and Directory Management

## 1. Objective

The objective of this exercise is to understand the Linux filesystem hierarchy, learn how directories are organised, understand file paths and practise basic directory navigation.

## 2. Understanding the Linux Filesystem

Linux uses a hierarchical filesystem structure that starts from a single root directory represented by `/`.

All files, directories, devices and mounted filesystems are organised under this root.

Unlike Windows, Linux does not use drive letters such as `C:` or `D:` to organise its filesystem.

## 3. Important Linux Directories

| Directory | Purpose |
|-----------|---------|
| `/` | Root of the entire filesystem |
| `/root` | Home directory of the root user |
| `/home` | Home directories of regular users |
| `/etc` | System configuration files |
| `/var` | Variable data such as logs and application data |
| `/var/log` | System and application logs |
| `/tmp` | Temporary files |
| `/usr` | User-space applications and utilities |
| `/opt` | Optional third-party applications |
| `/boot` | Boot-related files |
| `/dev` | Device files |
| `/proc` | Virtual filesystem containing process and kernel information |
| `/mnt` | Temporary filesystem mount points |

### Real-world application

When administering a Linux server running a web application:

- `/etc/nginx/` contains Nginx configuration.
- `/var/log/` contains system and application logs.
- `/home/` contains regular users' files.
- `/etc/ssh/` contains SSH server configuration.

Understanding these locations helps with server administration and troubleshooting.

## 4. Absolute and Relative Paths

### Absolute paths

An absolute path starts from the root directory `/`.

Example:

```bash
cd /var/log
```

This takes the user directly to `/var/log`, regardless of the current working directory.

### Relative paths

A relative path is interpreted based on the current working directory.

Example:

```bash
cd documents
```

This attempts to enter a directory called `documents` inside the current directory.

### Special path references

| Symbol | Meaning |
|--------|---------|
| `.` | Current directory |
| `..` | Parent directory |
| `~` | Current user's home directory |

## 5. Commands Practised

| Command | Purpose |
|---------|---------|
| `pwd` | Displays current working directory |
| `ls` | Lists directory contents |
| `ls -a` | Displays hidden files |
| `ls -l` | Displays detailed file information |
| `ls -lah` | Displays hidden files in detailed, human-readable format |
| `cd` | Changes directory |
| `mkdir` | Creates directories |
| `mkdir -p` | Creates nested directories |
| `touch` | Creates empty files |
| `cat` | Displays file contents |
| `less` | Views files page by page |
| `file` | Identifies file types |
| `tree` | Displays directory structures |

## 6. Practical Exercise: Creating a Linux Project Structure

### Objective

Create a directory structure for organising documents, logs, scripts and backups.

### Commands executed

Create the directories:

```bash
mkdir -p ~/linux-lab/{documents,logs,scripts,backups}
```

Create files:

```bash
touch ~/linux-lab/documents/notes.txt
touch ~/linux-lab/logs/application.log
touch ~/linux-lab/scripts/backup.sh
```

Inspect the directory structure:

```bash
tree ~/linux-lab
```

### Actual terminal output

```text
/root/linux-lab
├── backups
├── documents
│   └── notes.txt
├── logs
│   └── application.log
└── scripts
    └── backup.sh

5 directories, 3 files
```

### Result

The exercise completed successfully.

Created:

- 1 main directory (`linux-lab`).
- 4 subdirectories.
- 3 empty files.

The structure separates documents, application logs, scripts and backups into different directories.

## 7. Troubleshooting and System Administration Relevance

Understanding the Linux filesystem is important when:

- Locating application configuration files.
- Investigating server logs.
- Organising application files.
- Managing backups.
- Troubleshooting disk space.
- Navigating Linux servers remotely through SSH.

For example:

```bash
df -h
```

Displays filesystem disk usage.

```bash
du -sh ~/linux-lab
```

Displays the total disk space used by the `linux-lab` directory.

## 8. Knowledge Review

1. `/` represents the root filesystem.
2. `/root` is the root user's home directory.
3. `/etc/nginx/` contains Nginx configuration files.
4. `df -h` displays filesystem disk usage.
5. `cd ..` moves to the parent directory.
6. `ls -la` displays hidden files and detailed directory information.

## 9. Conclusion

This exercise introduced the Linux filesystem hierarchy, directory navigation, absolute and relative paths, and basic file and directory creation.

These concepts provide the foundation for managing Linux servers and deploying applications in cloud environments.
