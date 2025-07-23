* What is Cron, cronjob, and crontab?
1. Cron (The Daemon): Cron is a time-based job scheduler in Unix/Linux systems. It runs as a background service (cron or crond) and executes scheduled tasks (cron jobs) at specified times or intervals by checking configuration files called crontab.

Syntax for time based job scheduler:
* * * * *

│ │ │ │ │

│ │ │ │ └─── Day of the week (0 - 7) (Sunday = 0 or 7)

│ │ │ └───── Month (1 - 12)

│ │ └─────── Day of the month (1 - 31)

│ └───────── Hour (0 - 23)

└─────────── Minute (0 - 59)

2. Cronjob (Scheduled Task): An individual scheduled task/script/command defined in the crontab to run at set intervals. It can run scripts, clean up logs, take backups, or perform any repetitive task.

Example:
0 2 \* \* \* /home/user/backup.sh

→ This cron job runs the script backup.sh every day at 2:00 AM.
0 2 \* \* \* (cron)

/home/user/backup.sh (cronjob)
Crontab is a configuration file that contains a list of cron jobs (crontab)

3. Crontab (Cron Table): Crontab is a configuration file that contains a list of cron jobs. Each user can have their own crontab. System crontabs may also exist in /etc/crontab or /etc/cron.\* directories.

Cron - Background daemon that runs scheduled tasks.
Cronjob - A specific task scheduled via crontab
Crontab - File that lists cron jobs for a user/system

List of the cronjobs:
---------------------------
hello.sh
#!/bin/bash
echo "This is the hello shell script!"

welcome.sh
#!/bin/bash
echo "This is the welcome shell script!"

hello-data.sh
#!/bin/bash
echo "This is the hello-data shell script!"

hello1.sh
#!/bin/bash
echo "This is the hello1 shell script!"

hello2.sh
#!/bin/bash
echo "This is the hello2 shell script!"

How to add cronjobs in crontable?
crontab -l
crontab -r
crontab -e

*/1 * * * * /root/hello.sh
*/1 * * * * /root/welcome.sh
*/1 * * * * /root/hello-data.sh
*/1 * * * * /root/hello1.sh
*/1 * * * * /root/hello2.sh

tail -f /var/log/cron
cat /var/log/cron

* How to Fix the Permission Denied Issue
chmod +x /root/welcome.sh
chmod +x /root/hello.sh
chmod +x /root/hello-data.sh

How to start or stop or restart cron in our system?
* CentOS / RHEL / Fedora
sudo systemctl start crond       # Start the cron daemon
sudo systemctl stop crond        # Stop the cron daemon
sudo systemctl restart crond     # Restart the cron daemon
sudo systemctl status crond      # Check status

Crontab Commands (with Examples)
These commands manage user-specific scheduled tasks (cron jobs).

crontab -e
Description: Opens the current user's crontab file in an editor for editing (default: vi or nano).
Example:
crontab -e
This opens your crontab. You can add a job like:
0 6 * * * /home/ec2-user/backup.sh
(Runs the script every day at 6:00 AM.)

📋 crontab -l
Description: Lists all current user's cron jobs.
Example:
crontab -l

❌ crontab -r
Description: Deletes the current user's entire crontab file. ⚠️ Use with caution—this removes all scheduled jobs without confirmation.
Example:
crontab -r

👤 crontab -u <username> -e
Description: Edits the crontab of another user (requires sudo or root).
Example:
sudo crontab -u ec2-user -e

👀 crontab -u <username> -l
Description: Lists the cron jobs of another user.
Example:
sudo crontab -u ec2-user -l

🗑️ crontab -u <username> -r
Description: Removes all cron jobs for a specific user (requires sudo).
Example:
sudo crontab -u ec2-user -r
















