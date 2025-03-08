## REGISTERING SYSTEMS FOR RED HAT SUPPORT

There are four basic tasks performed with Red Hat Subscription Management tools:
1. Register
2. Subscribe
3. Enable repositories
4. Review and track

### Registering a System
subscription-manager register --username=yourusername -- password=yourpassword
View available subscriptions:subscription-manager list --available | less
Auto-attach a subscription:subscription-manager attach --auto

attach a subscription from a specific pool from the list of available subscriptions: subscription-manager attach --pool=poolID
View consumed subscriptions: subscription-manager list --consumed
Unregister a system: subscription-manager unregister

## EXPLAINING AND INVESTIGATING RPM SOFTWARE PACKAGES
RPM package files names consist of four elements:
1. name
2. version
3. release
4. architecture

coreutils-8.30-4.e18.x86_64.rpm
coreutils-name
8.30 - version
e18-release
x86_64 - arch

some rpm command
- rpm -qa - List all RPM packages currently installed
- rpm -q NAME - Display the version of NAME installed on the system
- rpm -qi NAME - Display detailed information about a package
- rpm -ql NAME - List all files included in a package
- rpm -qc NAME - List configuration files included in a package
- rpm -qd NAME - List documentation files included in a package
- rpm -q --changelog NAME - Show a short summary of the reason for a new package release
- rpm -q --scripts NAME - Display the shell scripts run on package installation, upgrade, or removal

## INSTALLING AND UPDATING SOFTWARE PACKAGES WITH YUM
The yum command allows you to install, update, remove, and get information about software packages and their dependencies.
- sudo yum install httpd
- sudo yum remove httpd
- sudo yum update

Installing and removing groups of software with yum
- `yum group list`
- `yum group info` - displays information about a group
- `yum group install` - installs a group that installs its mandatory and default packages and thepackages they depend on.
- `yum history` - displays a summary of install and remove transactions.
- `sudo yum history undo 5` - history undo option reverses a transaction.

### ENABLING YUM SOFTWARE REPOSITORIES
- `yum-config-manager --enable rhel-8-server-debug-rpms`

creating yum repo: yum-config-manager command
`yum-config-manager --add-repo="http://dl.fedoraproject.org/pub/epel/8/x86_64/"`

### MANAGING PACKAGE MODULE STREAMS
To display a list of available modules, use yum module list
`yum module list perl` 
`yum module info perl`
`sudo yum module install -y perl`
`sudo yum module remove -y perl`



