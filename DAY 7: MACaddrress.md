# MAC Address (Media Access Control Address)
suppose, you have a device or i have a device that can talk to internet and that's why this device need a unique identifier so device can connect to internet. That's where MAC address come. It's a address and 
unique identifier that assigned to a device or NIC. It's used by devices to communicate on a local network. 

**MAC address work in layer 2 which is data link layer.**

Format: It’s typically a 48-bit address (6 bytes) written in hexadecimal format, like 00:14:22:01:23:45

### where mac address used? 
In your local network if you want to identify a device, that's where mac addresses used. 

## How it Works:
1. Data Link Layer Communication: Devices use MAC addresses for data exchange on the local network (Ethernet, Wi-Fi). When data is sent over the network, 
it includes the MAC address of the source and the destination device.
2. Unchangeable: MAC addresses are usually burned into the hardware by the manufacturer and generally can't be changed (though software tools can spoof MAC addresses).

## Comparison Between IP Address and MAC Address
| Aspect      | MAC address | IP address |
| ----------- | ----------- | ---------- |
| Definition  | A unique hardware address assigned to each network device. | A logical address is used for identifying network devices (Layer 3). |
| Layer       | Data Link Layer (Layer 2) | Network Layer (Layer 3)  |
| Uniqueness  | 	Globally unique (manufacturers assign these addresses). | Unique within a network but not globally unique. (Can change based on network) |
| Format    | 48-bit hexadecimal, e.g., 00:14:22:01:23:45 | IPv4 (32-bit), e.g., 192.168.0.1 or IPv6 (128-bit), e.g., 2001:0db8::1           |
| Function | Identifies devices on a local network (Ethernet/Wi-Fi). | Identifies devices on a larger network or the internet. |
| Scope   | Local network (LAN).      |          Local network and the internet.  |
| Used for     | Local device communication.       |     Routing data across networks (Internet or LAN).       |
