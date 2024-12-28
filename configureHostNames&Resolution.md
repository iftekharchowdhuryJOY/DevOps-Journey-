### Changing the system host name
1. hostname command
A static host name may be specified in the /etc/hostname file.
hostnamectl - command modify /etc/hostname file
set host name: hostnamectl set-hostname host@example.com

CONFIGURING NAME RESOLUTION: stub resolver is used to convert host names to IP addresses or the reverse.
Display the current host name: hostname
Display the host name status: hostnamectl status
Change the host name and host name configuration file: sudo hostnamectl set-hostname servera.lab.example.com
View the configuration file providing the host name at network start: cat /etc/hostname
Display the host name status: hostnamectl status 

Temporarily change the host name: sudo hostname testname
Display the current hostname: hostname 
View the configuration file providing the host name at network start: cat /etc/hostname
Reboot the system: sudo reboot
