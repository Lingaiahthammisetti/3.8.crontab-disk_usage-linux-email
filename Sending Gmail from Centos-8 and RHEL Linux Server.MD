# Sending Gmail from CentOS 8

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
* append the following into the file at the end
```
  relayhost = \[smtp.gmail.com]:587
  smtp\_use\_tls = yes
  smtp\_sasl\_auth\_enable = yes
  smtp\_sasl\_password\_maps = hash:/etc/postfix/sasl\_passwd
  smtp\_sasl\_security\_options = noanonymous
  smtp\_sasl\_tls\_security\_options = noanonymous
  ```
* Configure Postfix SASL Credentials
* Add the Gmail credentials for authentication. Create a "/etc/postfix/sasl\_passwd" file
```
  touch /etc/postfix/sasl\_passwd
  ```
* Add the following line to the file:
```
  vim /etc/postfix/sasl_passwd
  ```
  \[smtp.gmail.com]:587 xyz:AppPassword
  \[smtp.gmail.com]:587  lingarao9885@gmail.com:Welcome#100
* If not working above commands, then below will work
  Gmail  manage your google account security turn on two-step verification  search apps passwords  create app password enter name devops create app password.
```
[smtp.gmail.com]:587  lingarao9885@gmail.com:amuorfiyfebhjcgh
```
* Note: xyz is from xyz@gmail.com, password\_app is from google management app password
  Create a Postfix lookup table from the sasl\_passwd text file by running the following command:
  ```
  postmap /etc/postfix/sasl_passwd
  ```
```
systemctl restart postfix
```
* Sending mail Run the following command to send mail:
```
  echo "This is a test mail \& Date $(date)" | mail -s "message" rao.lingaiah@gmail.com
  ```
```
echo "This is a test mail from $(hostname) sent on $(date)" | mail -s "Test Email from CentOS Server" rao.lingaiah@gmail.com
```






# Sending Gmail from RHEL 9

* switch to root
  sudo su -
* Install Postfix, the SASL authentication framework, and mailx.
  dnf -y install postfix cyrus-sasl-plain mailx
* Restart Postfix to detect the SASL framework.
  systemctl restart postfix
* Start Postfix on boot
  systemctl enable postfix
* Open the /etc/postfix/main.cf file.
  vim /etc/postfix/main.cf
* append the following into the file at the end
  relayhost = \[smtp.gmail.com]:587
  smtp\_use\_tls = yes
  smtp\_sasl\_auth\_enable = yes
  smtp\_sasl\_password\_maps = hash:/etc/postfix/sasl\_passwd
  smtp\_sasl\_security\_options = noanonymous
  smtp\_sasl\_tls\_security\_options = noanonymous
* Configure Postfix SASL Credentials
* Add the Gmail credentials for authentication. Create a "/etc/postfix/sasl\_passwd" file
  touch /etc/postfix/sasl\_passwd
* Add the following line to the file:
  vim /etc/postfix/sasl\_passwd
  \[smtp.gmail.com]:587 xyz:AppPassword
  \[smtp.gmail.com]:587  lingarao9885@gmail.com:Welcome#100
* If not working above commands, then below will work
  Gmail  manage your google account security turn on two-step verification  search apps passwords  create app password enter name devops create app password.

\[smtp.gmail.com]:587  lingarao9885@gmail.com:amuorfiyfebhjcgh

* Note: xyz is from xyz@gmail.com, password\_app is from google management app password
  Create a Postfix lookup table from the sasl\_passwd text file by running the following command:
  postmap /etc/postfix/sasl\_passwd

systemctl restart postfix

* Sending mail Run the following command to send mail:
  echo "This is a test mail \& Date $(date)" | mail -s "message" rao.lingaiah@gmail.com

echo "This is a test mail from $(hostname) sent on $(date)" | mail -s "Test Email from RHEL Server" rao.lingaiah@gmail.com



