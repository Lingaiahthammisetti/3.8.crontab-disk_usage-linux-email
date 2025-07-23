## Memory Types in Linux
* There are two main types of memory we monitor:
1. RAM Memory (System Memory)
2. Disk Memory (Hard Drive Storage)

* Monitor RAM Memory
➤ Basic Commands:
free           # Shows memory usage in KB
free -m        # Shows in MB
free -h        # Human-readable (auto-selects KB/MB/GB)

➤ Monitor in Real-Time:
top            # Shows processes consuming CPU and memory (interactive)
htop           # Improved version of `top` (may need to install)

* need to install htop on rhel
sudo yum install htop -y

* Check Disk Memory
➤ View Disk Usage:
df -h          # Disk usage in human-readable format
df -hT         # Shows filesystem types as well

➤ Check Only xfs Filesystem Usage:
df -hT | grep xfs

🧰 Extract Specific Fields Using awk
➤ Get only usage percentage (without % symbol):
df -hT | grep xfs | awk '{print $6}' | cut -d "%" -f1

$6 is typically the "Use%" column
cut -d "%" -f1 removes the % symbol

➤ Get the mount point (usually $7 column):
df -hT | grep xfs | awk '{print $7}'

⚠️ Correction Notes
You had a few typos in your original commands:
aws → should be awk
'print $6F' → should be 'print $6'
'print $1F' → should be 'print $1'

✅ Summary Table
Task	Command
Check RAM usage (human)	free -h
Real-time memory monitor	top or htop
Disk usage (human-readable)	df -h
Disk usage with filesystem type	df -hT
Filter only xfs disks	df -hT | grep xfs
Get usage % (without %)	df -hT | grep xfs | awk '{print $6}' | cut -d "%" -f1
Get mount point	df -hT | grep xfs | awk '{print $7}'

🧠 Understanding Disk Usage in Linux
You can check disk space and usage at various levels:
Whole filesystem
Specific partitions
Individual directories/files
File types
Interactive analysis

📌 Common Commands to Check Disk Usage
🔹 1. df – Disk Free
Shows total, used, and available disk space for mounted filesystems.

Basic usage:
df

Human-readable format:
df -h

Show filesystem types:
df -hT

Show only specific filesystem (e.g., ext4):
df -ht ext4

Example output:
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        20G   5G   15G   25% /
tmpfs           1.0G  4.0K  1.0G    1% /dev/shm

Only show xfs usage:
df -hT | grep xfs

🔹 2. du – Disk Usage
Estimates space used by files and directories.

Check usage of a directory:
du /var/log/audit



Human-readable format:
du -h /var/log/audit

Summary only (total size):
du -sh /path/to/dir
Example:
2.3G    /home/user/Pictures
1.2M    /home/user/Documents

🔹 3. ls – List File Sizes
Shows file sizes in a directory.

Long list with human-readable file sizes:
ls -lh

🔹 4. ncdu – NCurses Disk Usage Analyzer (interactive)
Better for analyzing large directories visually.

Install:
* Debian/Ubuntu
sudo apt install ncdu

* RHEL/CentOS
sudo yum install ncdu

Use:
ncdu /path/to/directory

🔹 5. lsblk – List Block Devices
Shows block devices (disks, partitions), not file-level usage.
lsblk

To check usage (combine with df):
df -h

🔹 6. find with du – Check Specific File Types
Find and display usage of .log files larger than 1GB:

find /path/to/logs -name "*.log" -size +1G -exec du -h {} \;
🔹 7. pydf – Colored Output for Disk Usage
Optional tool with pretty CLI output (not installed by default).
sudo apt install pydf
pydf

🔹 8. fdisk – Disk Partition Info
Shows partition table but not usage:
sudo fdisk -l

✅ Quick Summary of Commands
Purpose	Command
Show disk usage (all filesystems)	df -h
Show disk usage with filesystem type	df -hT
Disk usage of a specific folder	du -sh /path/to/directory
List file sizes in a directory	ls -lh
Interactive disk analysis	ncdu /path/to/directory
Show disk devices and partitions	lsblk
Find large files by type	find /path -name "*.log" -size +1G
