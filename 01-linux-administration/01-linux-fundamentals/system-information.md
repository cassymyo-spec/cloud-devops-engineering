# Linux Fundamentals – System Information

## 1. Objective

The objective of this exercise is to understand the basic Linux environment and learn how to retrieve important system information using terminal commands.

## 2. Understanding Linux

Linux is an open-source operating system kernel used in servers, desktops, cloud infrastructure and embedded systems.

Linux distributions package the Linux kernel with system utilities and software to provide a complete operating system.

Examples:

- Ubuntu
- Debian
- Fedora
- Red Hat Enterprise Linux
- Rocky Linux

## 3. Basic System Investigation

### 3.1 Current User

Command:

```bash
whoami
```

Purpose:

Displays the username of the currently logged-in user.

My result:

```text
root
```

### 3.2 Current Directory

Command:

```bash
pwd
```

Purpose:

Displays the absolute path of the current working directory.

My result:

```text
/root/cloud-devops-engineering/01-linux-administration/01-linux-fundamentals
```

### 3.3 Linux Distribution

Command:

```bash
cat /etc/os-release
```

Purpose:

Displays information about the installed Linux distribution, including its name and version.

My result:

```text
PRETTY_NAME="Ubuntu 26.04 LTS"
NAME="Ubuntu"
VERSION_ID="26.04"
VERSION="26.04 LTS (Resolute Raccoon)"
VERSION_CODENAME=resolute
ID=ubuntu
ID_LIKE=debian
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
UBUNTU_CODENAME=resolute
LOGO=ubuntu-logo
```

### 3.4 Kernel Information

Command:

```bash
uname -a
```

Purpose:

Displays kernel information, including the kernel version and machine architecture.

My result:

```text
Linux vps3652394.trouble-free.net 7.0.0-38-generic #38-Ubuntu SMP PREEMPT_DYNAMIC Fri Sep  4 09:10:14 UTC 2026 x86_64 GNU/Linux
```

### 3.5 Hostname

Command:

```bash
hostname
```

Purpose:

Displays the system's hostname.

My result:

```text
vps3652394.trouble-free.net
```

### 3.6 System Uptime

Command:

```bash
uptime
```

Purpose:

Shows how long the system has been running, the number of logged-in users and system load averages.

My result:

```text
10:50:21 up 4 days,  3:07,  1 user,  load average: 0.24, 0.30, 0.29
```

### 3.7 Memory Usage

Command:

```bash
free -h
```

Purpose:

Displays total, used and available memory and swap space.

The `-h` option displays values in human-readable units.

My result:

```text
               total        used        free      shared  buff/cache   available
Mem:           3.3Gi       1.4Gi       517Mi        38Mi       1.7Gi       1.9Gi
Swap:          1.0Gi       461Mi       562Mi
```

### 3.8 Disk Usage

Command:

```bash
df -h
```

Purpose:

Displays filesystem disk space usage, including total, used and available space.

My result:

```text
Filesystem      Size  Used Avail Use% Mounted on
tmpfs           680M  1.4M  679M   1% /run
/dev/sda4        77G   27G   47G  37% /
tmpfs           1.7G     0  1.7G   0% /dev/shm
none            1.0M     0  1.0M   0% /run/credentials/systemd-journald.service
none            1.0M     0  1.0M   0% /run/credentials/systemd-resolved.service
tmpfs           1.7G  190M  1.5G  12% /tmp
/dev/sda2       974M  179M  729M  20% /boot
none            1.0M     0  1.0M   0% /run/credentials/systemd-networkd.service
none            1.0M     0  1.0M   0% /run/credentials/getty@tty1.service
overlay          77G   27G   47G  37% /var/lib/docker/rootfs/overlayfs/200290389d8f32960a0d06f989d354fefbf82b52d0dc130a71c2abb363f5094d
overlay          77G   27G   47G  37% /var/lib/docker/rootfs/overlayfs/97ae1e1eb17d8675bae95718cb046a99b2afdcca00b19d76975905a08021e8ba
overlay          77G   27G   47G  37% /var/lib/docker/rootfs/overlayfs/2f7752d5d3249d3c10d2a2690e2f72d425ad66dbadf55bb3c9fb16a20d4c0c5b
overlay          77G   27G   47G  37% /var/lib/docker/rootfs/overlayfs/24eca0db9b88191425b12af550c551e55ae5d334b0d4f561bc2e87ea71a4fb4c
overlay          77G   27G   47G  37% /var/lib/docker/rootfs/overlayfs/8bc9c7ad432c66c2bf8138734554c2bbaa2c80d3c6c44bdb66d57b7e1f31ef9b
overlay          77G   27G   47G  37% /var/lib/docker/rootfs/overlayfs/54543622d1eba365c6e119188d61ed6ca74d258afab5942857bfb3f5e048aa21
overlay          77G   27G   47G  37% /var/lib/docker/rootfs/overlayfs/1cf83ad8bca81d4e7150ae67d8326f6e6c68206823ac3228c1183fa2b68a936a
tmpfs           340M  8.0K  340M   1% /run/user/0
```

## 4. What I Learned

- I learned how to identify the Linux distribution.
- I learned how to inspect kernel information.
- I learned how to identify the current user and working directory.
- I learned how to check memory and disk usage.
- I learned how to inspect system uptime.

## 5. Practical Importance in Cloud Engineering

System information commands are important when:

- Investigating server performance.
- Troubleshooting memory shortages.
- Diagnosing disk space problems.
- Identifying operating system versions.
- Monitoring server health.

## 6. Conclusion

This exercise introduced basic Linux system investigation commands. These commands form the foundation for Linux server administration and cloud infrastructure management.
