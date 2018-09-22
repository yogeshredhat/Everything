# Everything
All Configuration


ssh root login email alert

apt-get install libio-socket-ssl-perl libnet-ssleay-perl sendemail
   vim /root/.bashrc
echo "ALERT : Root Shell Access on: $(date) $(who)" | sendemail -f yogeshredhat14@gmail.com -t prashant@fcoos.net -u subject -m "Alert: Root Access from $(who) -f1" -s smtp.gmail.com:587 -o tls=yes -xu yogeshredhat14@gmail.com -xp yourpassword 

-------------------------------------------------------------------------------------------------
free ssl for domain
---------------------
https://linuxhostsupport.com/blog/install-lets-encrypt-ssl-certificates-using-certbot/
-----------------------------------------------------------------------------------------------
postfix
---------
https://devanswers.co/configure-postfix-to-use-gmail-smtp-on-ubuntu-16-04-digitalocean-droplet/
-----------------------------------------------------------------------------------------------------------
Nagios 4.2 on 16.04
------------------------
Create 2 new vm called server, client. Install ubuntu 16.04 Server.
Do this command for both machines. apt-get update  apt-get upgrade.
Once it is done, Reboot both machines and refer below url steps.
https://www.howtoforge.com/tutorial/ubuntu-nagios/
------------------------------------------------------------------------------------------------------------------
mailq alert
-------------
#!/bin/bash 
mailq_count="/bin/cat /etc/postfix/mailq_count" 
if [ `$mailq_count` -gt 25 ]; then echo "Mail count on Server is" `$mailq_count`| mail -s 'OVH Mail Server' yogesh@fcoos.net karthik@fcoos.net ; 
else 
exit 0; 
fi 
FTP Group Access
----------------------
Configure FTP in ubuntu server 16.04
------------------------------------

Access Directory /share/ftp with set of user access
----------------------------------------------------

sudo apt-get update

sudo apt-get install vsftpd

Backup original file
--------------------

sudo cp /etc/vsftpd.conf /etc/vsftpd.conf.orig

Add require ip in Firewall
--------------------------

sudo ufw allow 20/tcp
sudo ufw allow 21/tcp
sudo ufw allow 990/tcp
sudo ufw allow 40000:50000/tcp
sudo ufw status

sudo ufw status

Add user and assign Password
-----------------------------
sudo adduser u1
sudo adduser u2

sudo mkdir /share/global

sudo chown ftp:ftp /share -R

sudo chmod 775 /share -R

sudo setfacl -R -m u:u1:rwx /share
sudo setfacl -R -m u:u2:rwx /share

Edit configuration and add required content
-------------------------------------------
sudo vim /etc/vsftpd.conf

local_enable=YES

write_enable=YES

chroot_local_user=YES

local_root=/share/global

pasv_min_port=40000
pasv_max_port=50000

listen_port=45000

userlist_enable=YES
userlist_file=/etc/vsftpd.userlist
userlist_deny=NO

allow_writeable_chroot=YES

Add user in /etc/vsftpd.userlist file
-------------------------------------

sudo vim /etc/vsftpd.userlist

u1
u2

sudo systemctl restart vsftpd


Access it from browser
-----------------------

ftp://10.191.5.194:45000

Access it from terminal
-----------------------

ftp -p 10.191.5.194:45000

username : u1
Password : ********

imapsync
-----------
imapsync --host1 imap.gmail.com --user1 vm@pnrao.com --passfile1 passfile1 --host2 mail.fcoos.in --user2 vm@pnrao.com --passfile2 passfile2 --exclude "All Mail|Spam|Trash|Important|Starred" --allowsizemismatch 



