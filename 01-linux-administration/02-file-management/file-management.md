Linux File Management

Overview

This section covers Linux file and directory management, including creating, copying, moving, renaming, deleting, searching and inspecting files.

These skills are fundamental to Linux system administration and DevOps engineering.

Learning Objectives

- Understand Linux file management.
- Create and organise directories.
- Copy and move files.
- Rename and delete files.
- Search for files using "find".
- Search file contents using "grep".
- Read and inspect application logs.
- Create file backups.
- Understand command pipelines.

Topics Covered

Topic| Commands
Creating files| "touch"
Creating directories| "mkdir", "mkdir -p"
Copying files| "cp", "cp -r"
Moving and renaming| "mv"
Removing files| "rm", "rmdir"
Searching for files| "find"
Searching file contents| "grep"
Reading files| "cat", "less", "head", "tail"
Monitoring logs| "tail -f"
Counting lines| "wc -l"
Editing files| "nano"

Practical Lab: Application Log Investigation

Scenario

A Django application generates log files containing application events, warnings and errors.

The objective is to locate the logs, investigate errors and create a backup.

1. Create the directory structure

mkdir -p ~/linux-lab/file-management/{logs,backups,documents}

2. Generate a sample application log

cat > ~/linux-lab/file-management/logs/django.log <<EOF
2026-11-03 09:00:00 INFO Application started
2026-11-03 09:01:00 INFO Database connection successful
2026-11-03 09:02:00 WARNING High memory usage
2026-11-03 09:03:00 ERROR Database connection failed
2026-11-03 09:04:00 INFO Application restarted
2026-11-03 09:05:00 ERROR Payment processing failed
EOF

3. Find log files

find ~/linux-lab -type f -name "*.log"

4. Search for errors

grep -n "ERROR" ~/linux-lab/file-management/logs/django.log

5. Count errors

grep -c "ERROR" ~/linux-lab/file-management/logs/django.log

6. Display the last three lines

tail -n 3 ~/linux-lab/file-management/logs/django.log

7. Create a backup

cp ~/linux-lab/file-management/logs/django.log ~/linux-lab/file-management/backups/django-backup.log

8. Verify the backup

ls -lah ~/linux-lab/file-management/backups/

Important Command Differences

Command| Function
"cp"| Copies files without removing the original
"mv"| Moves or renames files
"find"| Searches for files and directories
"grep"| Searches for text inside files
"tail -n 20"| Displays the last 20 lines
"tail -f"| Continuously monitors new log entries
"rm -r"| Removes directories and their contents

Command Pipelines

Linux allows commands to work together using pipes.

Example:

grep "ERROR" django.log | wc -l

This searches for lines containing "ERROR" and counts the matching lines.

Understanding command operators

- "&&" executes the next command only if the previous command succeeds.
- "|" passes the output of one command into another.

Real-World DevOps Applications

These skills are useful when:

- Investigating application failures.
- Searching server logs.
- Creating configuration backups.
- Organising deployment files.
- Monitoring application activity.
- Troubleshooting production environments.
