# Linux Process Management

## 1. Introduction

Process management is an important part of Linux system administration.

A process is an instance of a running program. Whenever an application or command executes, Linux creates a process to manage its execution and allocate system resources.

Examples of Linux processes include:

- Nginx web server
- PostgreSQL database
- Django applications
- Redis
- Docker services
- Background scripts
- SSH services

Process management allows administrators to monitor, control and troubleshoot running applications.

It is particularly important in DevOps and cloud infrastructure because production servers often run multiple applications and services simultaneously.

## 2. Understanding Process IDs (PID)

Every running process has a unique Process ID (PID).

The PID identifies a particular process within the operating system.

To view processes associated with the current terminal:

```bash
ps
```

To display all running processes:

```bash
ps aux
```

To display the first ten processes:

```bash
ps aux | head -10
```

### Understanding `ps aux` output

| Column | Meaning |
|---|---|
| USER | User running the process |
| PID | Process ID |
| %CPU | CPU usage |
| %MEM | Memory usage |
| VSZ | Virtual memory size |
| RSS | Resident memory size |
| TTY | Controlling terminal |
| STAT | Process state |
| START | Process start information |
| COMMAND | Command that started the process |

### Display processes sorted by CPU usage

```bash
ps -eo pid,ppid,user,stat,%cpu,%mem,comm --sort=-%cpu | head -10
```

This displays processes with the highest CPU consumption first.

## 3. Finding Specific Processes

Sometimes administrators need to determine whether a particular application is running.

For example, checking Nginx:

```bash
ps aux | grep nginx
```

Another option is:

```bash
pgrep nginx
```

To display matching process IDs and their commands:

```bash
pgrep -a nginx
```

These commands are useful when investigating applications running on Linux servers.

## 4. Monitoring Processes in Real Time

Linux provides tools for monitoring running processes.

### top

```bash
top
```

The `top` command provides a continuously updated view of:

- Running processes
- CPU usage
- Memory usage
- System load
- Process IDs
- User accounts

Press `q` to exit.

### htop

```bash
htop
```

`htop` provides an interactive process monitoring interface.

On Ubuntu or Debian, install it using:

```bash
sudo apt install htop
```

### Difference between top and htop

| top | htop |
|---|---|
| Usually installed by default | May require installation |
| Basic terminal interface | Interactive interface |
| Displays process information | Provides easier navigation and filtering |

## 5. Understanding CPU and Memory Usage

Running applications consume system resources.

For example:

- Django consumes memory while handling requests.
- PostgreSQL uses CPU and memory for database operations.
- Nginx handles incoming web requests.
- Background workers execute scheduled tasks.

### Check memory usage

```bash
free -h
```

The `-h` option displays memory values in human-readable units.

### Check system uptime and load

```bash
uptime
```

This displays:

- Current system time
- How long the server has been running
- Number of logged-in users
- System load averages

### Monitor resource consumption

```bash
top
```

High CPU usage and high memory usage are different problems.

CPU usage measures processing activity, while memory usage indicates how much RAM processes occupy.

## 6. Linux Process States

Processes can exist in different states.

| State | Meaning |
|---|---|
| R | Running or runnable |
| S | Interruptible sleep |
| D | Uninterruptible sleep |
| T | Stopped |
| Z | Zombie process |

### Understanding zombie processes

A zombie process is a process that has finished executing but still has an entry in the process table because its parent has not collected its exit status.

Inspect process states using:

```bash
ps aux
```

Look at the `STAT` column.

## 7. Parent and Child Processes

Linux processes can create other processes.

A process that creates another process is called the parent process.

The newly created process is called the child process.

Each process normally has a Parent Process ID (PPID).

### Display the process hierarchy

```bash
ps -ef
```

Important columns:

| Column | Meaning |
|---|---|
| UID | User running the process |
| PID | Process ID |
| PPID | Parent Process ID |
| C | CPU utilisation |
| STIME | Process start time |
| CMD | Command |

### Display a process tree

```bash
pstree
```

If the command is unavailable on Ubuntu or Debian:

```bash
sudo apt install psmisc
```

The process tree helps administrators understand relationships between applications and the processes they create.

## 8. Managing Processes

Linux provides several commands for controlling processes.

### Starting a process

For example:

```bash
sleep 300
```

This starts a process that waits for 300 seconds.

### Interrupting a foreground process

Press:

```
CTRL + C
```

This sends an interrupt signal to the foreground process.

### Finding a process

```bash
pgrep -a sleep
```

This displays matching processes.

### Terminating a process

```bash
kill PID
```

Replace `PID` with the actual process ID.

By default, `kill` sends SIGTERM, requesting graceful termination.

Always verify the process ID before terminating anything.

## 9. Linux Process Signals

Signals allow the operating system and users to communicate with processes.

Important signals include:

| Signal | Number | Purpose |
|---|---|---|
| SIGHUP | 1 | Hangup; sometimes used to request configuration reloads |
| SIGKILL | 9 | Forcefully terminates a process |
| SIGTERM | 15 | Requests graceful termination |
| SIGCONT | 18 | Resumes a stopped process |
| SIGSTOP | 19 | Stops a process |

### SIGTERM

```bash
kill -15 PID
```

Requests that the process terminate gracefully.

This gives the application an opportunity to perform cleanup operations.

### SIGKILL

```bash
kill -9 PID
```

Forcefully terminates a process.

It does not allow the application to perform normal cleanup.

SIGKILL should not be the first option when terminating an application.

### SIGSTOP and SIGCONT

SIGSTOP pauses a process.

SIGCONT resumes a stopped process.

These signals should only be used when you understand the effect on the application.

## 10. Background Processes

A background process allows a command to continue running without occupying the foreground terminal.

### Start a process in the background

```bash
sleep 300 &
```

The `&` symbol starts the command in the background.

### Display background jobs

```bash
jobs
```

This displays jobs associated with the current shell.

### Bring a job to the foreground

```bash
fg
```

### Suspend a foreground job

Press:

```
CTRL + Z
```

This suspends the foreground process.

### Resume a suspended job in the background

```bash
bg
```

These commands are useful when running scripts and other tasks from a terminal.

## 11. Process Priority

Linux allows processes to have different CPU scheduling priorities.

Two important commands are:

- `nice`: Starts a process with a specified nice value.
- `renice`: Changes the nice value of an existing process.

Nice values generally range from -20 to 19.

| Nice value | Meaning |
|---|---|
| -20 | Highest scheduling priority |
| 0 | Default priority |
| 19 | Lowest scheduling priority |

### Start a process with a lower scheduling priority

```bash
nice -n 10 sleep 300
```

### Inspect process priority

```bash
ps -eo pid,ni,comm | grep sleep
```

The `NI` column displays the nice value.

### Change an existing process priority

```bash
renice 10 -p PID
```

Replace `PID` with the process ID.

Changing to a higher nice value generally makes the process less favoured by the CPU scheduler.

Administrative privileges may be required for certain priority changes.

## 12. Practical Lab: Inspect Running Processes

The following commands provide a basic process inspection exercise.

### Step 1: Identify the current user

```bash
whoami
```

### Step 2: Display running processes

```bash
ps aux | head -10
```

### Step 3: Display processes sorted by CPU usage

```bash
ps -eo pid,ppid,user,stat,%cpu,%mem,comm --sort=-%cpu | head -10
```

### Step 4: Inspect memory

```bash
free -h
```

### Step 5: Inspect uptime and system load

```bash
uptime
```

These commands help administrators understand which processes are running and how the server's resources are being used.

## 13. Practical Lab: Starting and Terminating a Test Process

Use a harmless test process rather than a production application.

### Step 1: Start a background process

```bash
sleep 600 &
```

### Step 2: Find its PID

```bash
pgrep -a sleep
```

### Step 3: Inspect the process

Replace `PID` with the actual process ID:

```bash
ps -o pid,ppid,user,stat,ni,cmd -p PID
```

### Step 4: Terminate the test process

```bash
kill PID
```

### Step 5: Verify termination

```bash
pgrep -a sleep
```

If no matching process remains, the test process has stopped.

**Important:** Only terminate the test process created for this exercise. Do not experiment with termination commands on production services.

## 14. Real-World DevOps Applications

Process management is used regularly when maintaining production infrastructure.

### Application troubleshooting

Imagine a Django application becomes unresponsive.

An administrator may:

1. Identify the Django process.
2. Inspect CPU consumption.
3. Inspect memory consumption.
4. Check the process state.
5. Examine application logs.
6. Investigate related database processes.
7. Determine the appropriate corrective action.

### Resource monitoring

Administrators monitor processes to identify applications consuming excessive resources.

This helps prevent resource exhaustion and unexpected service interruptions.

### Background processing

Applications frequently use background workers to process tasks without blocking normal application requests.

### Server maintenance

Process management helps administrators understand which applications are running before carrying out maintenance operations.

## 15. Security and Production Best Practices

1. Avoid terminating processes without identifying them first.
2. Prefer graceful termination using SIGTERM.
3. Avoid using SIGKILL unless necessary.
4. Monitor CPU and memory consumption.
5. Investigate unexpected processes.
6. Avoid experimenting with production services.
7. Understand parent-child process relationships.
8. Use appropriate privileges when managing processes.

## 16. Useful Commands Reference

| Command | Purpose |
|---|---|
| `ps` | Display processes associated with the terminal |
| `ps aux` | Display running processes |
| `ps -ef` | Display processes in full format |
| `pgrep process` | Find process IDs |
| `pgrep -a process` | Find processes and display commands |
| `top` | Monitor processes in real time |
| `htop` | Interactive process monitoring |
| `free -h` | Display memory usage |
| `uptime` | Display uptime and load averages |
| `pstree` | Display process hierarchy |
| `kill PID` | Request process termination |
| `kill -9 PID` | Force process termination |
| `jobs` | Display shell background jobs |
| `bg` | Resume a suspended job in the background |
| `fg` | Bring a background job to the foreground |
| `nice` | Start a process with a specified nice value |
| `renice` | Change an existing process's nice value |

## Conclusion

Linux process management is essential for understanding how applications execute and consume system resources.

Knowing how to inspect processes, monitor CPU and memory, understand process states, manage signals and control background tasks helps administrators maintain reliable Linux servers.

These skills provide an important foundation for the next stages of Linux administration, cloud infrastructure and DevOps engineering.
