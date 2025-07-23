### Sending Gmail from CentOS 8

* switch to root 
```
sudo su -
```

* Install Postfix, the SASL authentication framework, and mailx.
 ```
yum -y install postfix cyrus-sasl-plain mailx
 ```

* Restart Postfix to detect the SASL framework.
```
systemctl restart postfix 
```

* Start Postfix on boot
```
systemctl enable postfix 
```
* Open the /etc/postfix/main.cf file.
```
vim /etc/postfix/main.cf 
```
append the following into the file at the end

```
relayhost = [smtp.gmail.com]:587
smtp_use_tls = yes
smtp_sasl_auth_enable = yes
smtp_sasl_password_maps = hash:/etc/postfix/sasl_passwd
smtp_sasl_security_options = noanonymous
smtp_sasl_tls_security_options = noanonymous
```
 
*  Configure Postfix SASL Credentials

Add the Gmail credentials for authentication. Create a "/etc/postfix/sasl_passwd" file
```
touch /etc/postfix/sasl_passwd  
```

```
chmod 600 /etc/postfix/sasl_passwd
```

Add the following line to the file:
```
vim /etc/postfix/sasl_passwd
```
```
[smtp.gmail.com]:587 xyz:AppPassword
 ```
 **Note: xyz is from xyz@gmail.com, password_app is from google management app password**

* If not working above commands, then below will work
  Gmail  manage your google account security turn on two-step verification  search apps passwords  create app password enter name devops create app password.
```
[smtp.gmail.com]:587  lingarao9885@gmail.com:amuorfiyfebhjcgh
```

* Create a Postfix lookup table from the sasl_passwd text file by running the following command:
```
postmap /etc/postfix/sasl_passwd 
```
```
systemctl restart postfix
```

* Sending mail
Run the following command to send mail:
```
echo "This is a test mail & Date $(date)" | mail -s "message" info@joindevops.com
```
```
echo "This is a test mail from $(hostname) sent on $(date)" | mail -s "Test Email from CentOS Server" rao.lingaiah@gmail.com
```







✅ Confirmed Working Commands on RHEL 9
Switch to root
sudo su -

✅ Yes, works as expected.
Install required packages
yum -y install postfix cyrus-sasl-plain mailx

✅ Works, but note:
RHEL 9 uses dnf by default, but yum is still an alias to dnf, so this command works.
Make sure your system is registered with Red Hat subscription or using a repo (like EPEL) if packages are missing.
mailx in RHEL 9 is part of the heirloom-mailx or bsd-mailx depending on available repos.

Restart and enable Postfix
systemctl restart postfix
systemctl enable postfix

✅ Works as is.
Edit configuration file
vim /etc/postfix/main.cf
✅ Standard config file edit. No issues.
Configure SASL password
touch /etc/postfix/sasl_passwd
chmod 600 /etc/postfix/sasl_passwd
vim /etc/postfix/sasl_passwd

✅ Works as expected.
Generate Postfix hash map
postmap /etc/postfix/sasl_passwd
systemctl restart postfix

✅ Works. Ensure the .db file is created.
Sending test email
echo "This is a test mail & Date $(date)" | mail -s "message" info@joindevops.com
echo "This is a test mail from $(hostname) sent on $(date)" | mail -s "Test Email from CentOS Server" rao.lingaiah@gmail.com

✅ Will work if Gmail SMTP authentication is configured correctly.
⚠️ Important Notes for RHEL 9 & Gmail
App Passwords: Gmail no longer supports less secure apps, so:

You must use App Passwords, generated after enabling 2-Step Verification.

Example:
[smtp.gmail.com]:587 your_email@gmail.com:your_app_password
Package availability:

If mailx or cyrus-sasl-plain are not found, enable the required repositories:
sudo dnf install epel-release
sudo dnf install cyrus-sasl-plain mailx

Firewall/SELinux:
Ensure port 587 is allowed through the firewall:
firewall-cmd --permanent --add-port=587/tcp
firewall-cmd --reload

SELinux might block postfix from sending email. You may need:
setsebool -P httpd_can_sendmail 1
Logging & Debugging

If mail fails to send, check logs:
journalctl -u postfix
tail -f /var/log/maillog

✅ Summary
Yes, your steps will work on RHEL 9, with minor adjustments:
Use dnf if needed.
Ensure proper repositories and App Passwords.
Watch for SELinux/firewall blocking issues.
Gmail App Password is required.





