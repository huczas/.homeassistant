# Setup RaspberryPi to send email notifications

ssmtp is a nice and simple solution for sending emails from the command line etc.

## Installing

`sudo apt-get install ssmtp`
`sudo apt-get install mailutils`

Now edit the SSMTP configuration file

`sudo nano /etc/ssmtp/ssmtp.conf`

It needs to include this:

```BASH
root=postmaster
mailhub=smtp.gmail.com:587
hostname=raspberrypi
AuthUser=AGmailUserName@gmail.com
AuthPass=TheGmailPassword
FromLineOverride=YES
UseSTARTTLS=YES
```

Save and exit

## Sending an email

`echo "Hello world email body" | mail -s "Test Subject" recipientname@domain.com`

## Sending A File

Install mpack

`sudo apt-get install mpack`

To send a file

`mpack -s "Test" /home/pi/some_folder/somefile.ext recipientname@domain.com`

TIP, send email every reboot with new IP address:

```BASH
echo -e "Restart o `date '+%H:%M %d/%m/%Y'`. \n\nAktualne IP: `hostname -I`"| mail -s "Restart Raspberry Pi 3B" myemail@gmail.com
```