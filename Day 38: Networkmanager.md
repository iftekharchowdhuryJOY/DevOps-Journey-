# Describing NetworkManager Concepts
It is a process or daemon that work network management. It manages network interfaces like Ethernet, Wi-Fi, and VPN connections, enabling automatic switching and configuration.
## Viewing Networking Information
Commands:
1. nmcli device show - Displays detailed information about network interfaces.
2. ip addr - Shows IP addresses and interface states.
3. nmcli connection show - Lists all configured network connections.
4. ifconfig (deprecated, use ip instead) - Displays network interface details.
5. cat /etc/resolv.conf - Shows DNS server configurations.

# Adding a Network Connection
- nmcli connection add type ethernet ifname eth0 con-name my-connection ip4 192.168.1.100/24 gw4 192.168.1.1
- type - Type of connection (e.g., ethernet, wifi).
- ifname - Interface name (e.g., eth0).
- ip4 - IPv4 address.
- gw4 - Gateway.

## What is the nmcli Command?
nmcli is a command-line tool for managing NetworkManager. It allows you to configure and control network interfaces, connections, and settings without a graphical interface.

Basic Usage:
- nmcli device - Shows device statuses.
- nmcli connection - Lists and manages network connections.
- nmcli general - Provides general NetworkManager information.

## How to configure Networking from the Command Line
ip link set dev eth0 up
ip addr add 192.168.1.100/24 dev eth0
ip route add default via 192.168.1.1

### Editing Network Configuration Files
Network configuration files in Red Hat Linux are typically located in /etc/sysconfig/network-scripts/: 
vi /etc/sysconfig/network-scripts/ifcfg-<interface-name>

TYPE=Ethernet
BOOTPROTO=static
IPADDR=192.168.1.100
NETMASK=255.255.255.0
GATEWAY=192.168.1.1
DNS1=8.8.8.8
ONBOOT=yes
systemctl restart NetworkManager
