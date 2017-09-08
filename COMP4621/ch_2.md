# Application Layer

## Principles of Network Applications

### Application Architecture

#### Client-server Architecture
Server is always on, but the client is not always connected. The clients may have dynamic IP addresses. There is a scalability issue in this design, as there are limited numbers of users that a server can support concurrently. Also security issue as there is only one server, which will obviously be targeted by attackers. Performance issue exists as everything will have to pass through the server, causing the server to be a bottleneck.

#### P2P Architecture
Realized that laptops and computers nowadays are significantly improved compared to olden days. Let the devices talk directly, no need to go through a server. Any new device means a new server, meaning the system is self-scaling. Scalability wise, theoretically, this is the best choice. However, the problem is the device is not always on.

### Process Communication
Inter device process communication. There is a client process and server process. In a peer to peer architecture, each device has the chance to be a client and server process.

### Sockets
Can be imagined as a door. Sockets at both client and server, serves as entrance and exit points.

### Addressing Processes
IP address is not sufficient, the host has many networking services running in the system. That is why you need a port number. The combination of an IP address and port number can represent a certain process running in a device.

A certain number of port numbers are reserved for ports that are often used. Approved by the internet committee. So that these ports cannot be reused by other processes.

### App-layer Protocols
Needed to ensure that both sides are able to ensure each other. Basically a definition for how to understand the different fields of the message (semantics of the message).
