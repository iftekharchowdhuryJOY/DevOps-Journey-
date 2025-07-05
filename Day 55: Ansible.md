## Ansible
Ansible is an automation tool used to configure systems, install software, and run commands on servers — without having to manually log into each one.

## 1. Control Node (Not "Controled Node")
This is the machine where Ansible is installed and from which you run commands/playbooks. It manages other nodes (called "managed nodes"). Requires Python (for most modules) and SSH access (by default) to communicate with managed nodes.

## 2. Managed Node (Also Called "Hosts")
These are the remote machines/servers being managed by Ansible. They do not require Ansible installed (Ansible executes tasks over SSH/WinRM). Must have Python (for Linux/Unix) or PowerShell (for Windows) to run modules.

## Two Ways to Use Ansible
1. Ansible Push (default and most common)
2. Ansible Pull (less common, used in some specific use cases)

## What Is Ansible Pull (In-Depth)?
Ansible Pull lets a device (like an IoT device or cloud server) self-configure by:
1. Connecting to a Git repository
2. Downloading the playbook(s)
3. Running the playbook locally, on itself

So instead of you managing the device, the device manages itself.
