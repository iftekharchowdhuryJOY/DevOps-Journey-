Client and server wants to establish a reliable connection. And here TCPHandshake helps client and server to establish the reliable connection.
Three things to remember:
1. SYN
2. SYN-ACK
3. ACK
4. 
Here is an example:
Let’s assume:
1. Client IP: 192.168.1.2
2. Server IP: 192.168.1.1
3. Port: 80 (HTTP)

1. SYN (Client → Server):
Source IP: 192.168.1.2, Source Port: Random (e.g., 54321)
Destination IP: 192.168.1.1, Destination Port: 80
Flags: SYN
Sequence Number: 100

2. SYN-ACK (Server → Client): The server responds:
Source IP: 192.168.1.1, Source Port: 80
Destination IP: 192.168.1.2, Destination Port: 54321
Flags: SYN, ACK
Sequence Number: 200
Acknowledgment Number: 101
3. ACK (Client → Server):
The client sends:
Source IP: 192.168.1.2, Source Port: 54321
Destination IP: 192.168.1.1, Destination Port: 80
Flags: ACK
Sequence Number: 101
Acknowledgment Number: 201
