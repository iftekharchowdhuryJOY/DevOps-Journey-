# DHCP
Dynamic Host Configuration Protocol (DHCP) is a protocol that automatically assigns IP addresses and other network configuration parameters (like subnet masks, gateways, and DNS servers) to devices on a network. 

# How DHCP Works
DHCP Components:

- DHCP Server: A device (often your router) responsible for managing and assigning IP addresses to devices.
- DHCP Client: A device (laptop, smartphone, etc.) that requests an IP address from the server.

Process of Assigning IPs: The DHCP process uses a four-step handshake called DORA:

1. Discovery (Client → Broadcast): When a device (client) joins the network, it sends out a DHCP Discover broadcast message to find available DHCP servers. This message is sent to the address 255.255.255.255 to ensure all devices in the network can receive it.
Example: "I need an IP address. Any DHCP server available?"
2. Offer (Server → Broadcast/Client): The DHCP server receives the discover message and responds with a DHCP Offer message. The offer includes:An available IP address for the client.
Subnet mask, gateway, DNS servers, and lease duration.
Example: "I can offer you IP 192.168.1.100 with a subnet mask 255.255.255.0 and gateway 192.168.1.1 for 24 hours."

3. Request (Client → Broadcast/Server): The client selects an offer and sends a DHCP Request message to the server. This message tells the server it accepts the offered IP address.
Example: "I accept the IP 192.168.1.100."

4. Acknowledgment (Server → Broadcast/Client): The DHCP server confirms the lease by sending a DHCP Acknowledgment message. This message informs the client that the IP address is now allocated.
Example: "IP 192.168.1.100 is now yours for 24 hours. Happy networking!" After this handshake, the client configures its network settings and begins communication.

## Key Concepts in DHCP
IP Lease: The assigned IP address comes with a lease time. The lease specifies how long the client can use the IP. Once it expires, the client must renew the lease.
IP Address Pool: The DHCP server maintains a pool of available IP addresses (e.g., 192.168.1.100 to 192.168.1.200) and assigns them dynamically.
Static vs Dynamic IPs: Dynamic IP: The DHCP server assigns IPs automatically from its pool. Static IP: An IP address is manually set and permanently assigned to a specific device (e.g., a printer or server).
Reservation: You can configure the DHCP server to reserve an IP address for a specific device using its MAC address. This ensures the device always receives the same IP.

Real-Life Example
When you connect your smartphone to your home Wi-Fi:
- The phone sends a DHCP Discover message.
- Your router responds with a DHCP Offer, proposing an IP address from its available pool (e.g., 192.168.0.105).
- Your phone accepts the offer by sending a DHCP Request.
- The router confirms with a DHCP Acknowledgment.
- Your phone is assigned the IP 192.168.0.105, valid for 24 hours.
