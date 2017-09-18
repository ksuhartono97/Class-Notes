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

### Internet transport protocol services

- TCP Service

  - Reliable transports: Means that what is transmitted must be receivable. To ensure this, will make the network complicated. TCP is the most reliable protocol for this. Ensure only have one transport protocol.
  - Flow control
  - Congestion control
  - No timing guarantees, anything can happen.
  - Usually called as connection oriented protocol.

> For TCP, it guarantees reliability, but no other guarantees (timing or min. throughput)

- UDP service (unreliable), we need this to introduce overhead to the reliable service (voice chatting and video streaming uses UDP)

## Web and HTTP

HTTP doesn't keep history, so there is no need to do lookup. Each request is independent to each other.

### HTTP Connections

Two types, persistent and non-persistent http.

- Non-persistent http means per TCP connection, you send one object.
- Persistent http means you can send multiple objects per connections. (even only one is fine)

> Non persistent design existed only in the old days. Now usually only persistent http is used.

RTT (Round trip time) : time taken for a packet to travel from client to server and back.

### Caching
> Recall : if arrival is larger than going rate, will cause delay to get longer and longer eventually becoming infinity.

Higher access link rate means lower access link utilization which also means higher internet speed. However, expensive cost

Solution is to use a cache, to handle repeated accesses of certain data. Basically allowing a reduction in the amount of data flow and the access link utilization. For example a 40% cache hit rate will reduce traffic rate through the access link to 60%.

> The higher the cache hit rate, the better your performance.

Using a proxy server architecture to improve performance. Conditional get is different from normal get request.

The cache will be put with the proxy server. The proxy server itself is both client and server. When talking to the client the proxy acts as a server, and the server itself is acting as a client when asking for content from the server. The proxy can get either 304 or 200 response.

## FTP
Control related parts will get sent through port 21, authentication, filesystem navigation, and others goes here. After obtaining authorization and location of the file, we setup another port at port 20 for real data transmission.

From the application point of view, we are using 2 network protocols to achieve the applications requirement. This is called as the out-of-band design. (One band for control, one band for data, causing the control communication to not interact the data transmission)

## Electronic Mail
Components:
- **User agent** is the interface with which the user interacts.
- **Mail servers** where messages are stored, there are numerous servers in the world.
- **SMTP (Simple Mail Transfer Protocol)** this is the protocol that allows the servers to talk to which other in order to deliver the mail.

The mail server has two components, the user mailbox (yellow colour in the slides) and the outgoing message queue (green in the slides).

Mailbox, for every user, it contains the incoming message for the user. Message queue will have the messages that needs to be sent to another server. So the interaction is between the message queue of one server with the mailbox of another server. Again the server can serve as a client and server, depending on what the server needs to do. When sending a message, serves a client, and the receiver serves as a server.

### SMTP
Standardized by ITF, using port 25.

Say Alice wants to send a message to Bob, Alice's mailserver has to open a protocol (acting as a client) to Bob server's mailbox. Bob's mailserver will receive and put the message in Bob's mailbox. At this point the SMTP protocol is finished.

Is a push based connection (setup a connection and send data, as compared to HTTP who is a pull based connection where you setup a connection and get data).

### Mail Access Protocol
User Agents access the messages from the server using MAPs.

Types:
- POP
- IMAP
- HTTP

## DNS
The protocol itself is the infrastructure of internet that is implemented on application level.

IP address is too hard to remember, just a set of numbers that are always changing, that is why there are user friendly names for humans.

There are 13 root name servers worldwide, there is 1 root server in Asia, which is in Japan.

Most details are put in the authoritative DNS servers, which is maintained by organization or SP.

Typical topology: An endhost trying to visit another location. The requesting host tries to find out something, so then there will be a dns request to the umass address. So first, you will talk to the local server. If the local server doesn't know anything about the address that you asked, then it will send a request to the root DNS server.
