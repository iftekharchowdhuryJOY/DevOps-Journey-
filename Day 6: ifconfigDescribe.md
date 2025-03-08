ens160: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.112.128  netmask 255.255.255.0  broadcast 192.168.112.255
        inet6 fe80::20c:29ff:fe9c:c475  prefixlen 64  scopeid 0x20<link>
        ether 00:0c:29:9c:c4:75  txqueuelen 1000  (Ethernet)
        RX packets 663794  bytes 971924710 (926.8 MiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 112373  bytes 7957898 (7.5 MiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0


1. ens160: This is the name of the network interface. In modern systems, interfaces often have predictable names like ens160 instead of the older eth0 or wlan0.
2. Flags: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>:
UP: The interface is enabled and operational.
BROADCAST: The interface supports broadcasting, which means it can send data packets to all devices on the local network.
RUNNING: The interface is currently active and running.
MULTICAST: The interface supports multicast communication, which allows it to send data packets to a group of devices.
3. MTU (Maximum Transmission Unit): mtu 1500: The maximum packet size that can be transmitted over this network interface is 1500 bytes.
4. IPv4 Address: inet 192.168.112.128: This is the IPv4 address assigned to the network interface ens160. The private IP address 192.168.112.128 is part of the 192.168.x.x range, which is reserved for private local networks.
5. Netmask: netmask 255.255.255.0: This defines the subnet mask for the network. A subnet mask of 255.255.255.0 means the first 24 bits are used for the network part, and the remaining 8 bits are used for the host part. This allows up to 256 addresses (0-255) in this subnet.
6. Broadcast Address: broadcast 192.168.112.255: This is the broadcast address for the network. A broadcast address is used to send a message to all devices within the network. Here, 192.168.112.255 is the address used for broadcasting to all devices within the 192.168.112.0/24 network.
7. IPv6 Address: inet6 fe80::20c:29ff:fe9c:c475: This is the IPv6 address assigned to the interface. The fe80:: prefix indicates that this is a link-local address, meaning it's only valid within the local network and is not routable on the internet.
prefixlen 64: This shows the length of the network prefix (subnet). In this case, the first 64 bits are used for the network portion of the address.
8. MAC Address: ether 00:0c:29:9c:c4:75: This is the MAC address (Media Access Control address), a unique identifier assigned to the network interface card (NIC). This address is used for communication on the local network.
00:0c:29:9c:c4:75 is the MAC address for this interface.
9. Transmission Queue Length: txqueuelen 1000: This is the length of the transmit queue. It indicates the number of packets the system can hold for transmission before they are actually sent out.
10. RX/TX Packets and Bytes: RX packets 663794 bytes 971924710 (926.8 MiB): RX packets: This shows the number of packets received by the interface (663,794 packets).
- RX bytes: This shows the total number of bytes received (971,924,710 bytes, which is approximately 926.8 MiB).
- TX packets 112373 bytes 7957898 (7.5 MiB):
- TX packets: This shows the number of packets sent by the interface (112,373 packets).
- TX bytes: This shows the total number of bytes sent (7,957,898 bytes, which is approximately 7.5 MiB).
11. Errors and Dropped Packets: RX errors 0 dropped 0 overruns 0 frame 0: This means no errors occurred when receiving packets. RX errors: The number of receive errors (none).
RX dropped: The number of packets dropped during reception (none).
RX overruns: The number of buffer overruns (none).
RX frame: Frame errors (none).
TX errors 0 dropped 0 overruns 0 carrier 0 collisions 0: This means no errors occurred when sending packets.

TX errors: The number of transmit errors (none).
TX dropped: The number of packets dropped during transmission (none).
TX overruns: The number of buffer overruns (none).
TX carrier: Carrier errors (none).
TX collisions: The number of packet collisions (none).
