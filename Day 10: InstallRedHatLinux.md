## Installing Red Hat Enterprise Linux
User can download the OS, other resources from RED Hat customer portal website. A user need active subscription.
## AUTOMATING INSTALLATION WITH KICKSTART

## CREATING A KICKSTART PROFILE
Kickstart automates the installation process for Red Hat Linux. 
### commands
- url: url --url="http://classroom.example.com/content/rhel8.0/x86_64/dvd/"
- repo: repo --name="appstream" --baseurl=http://classroom.example.com/content/rhel8.0/x86_64/dvd/AppStream/
- clearpart: clearpart --all --drives=sda,sdb --initlabel
- part: part /home --fstype=ext4 --label=homes --size=4096 --maxsize=8192 --grow
- ignoredisk: ignoredisk --drives=sdc
- bootloader: bootloader --location=mbr --boot-drive=sda
- volgroup, logvol: Creates LVM volume groups and logical volumes.
part pv.01 --size=8192
volgroup myvg pv.01
logvol / --vgname=myvg --fstype=xfs --size=2048 --name=rootvol --grow
logvol /var --vgname=myvg --fstype=xfs --size=4096 --name=varvol

## Network commands
- network: network --device=eth0 --bootproto=dhcp
- firewall: firewall --enabled --service=ssh,http


## INSTALLING AND CONFIGURING VIRTUAL MACHINES
In Red Hat Enterprise Linux, manage KVM with the virsh command or with Cockpit's Virtual Machines tool.
## MANAGING LAYERED STORAGE WITH STRATIS

## DESCRIBING THE STRATIS ARCHITECTURE

