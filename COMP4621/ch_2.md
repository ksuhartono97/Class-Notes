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

### Iterative Query

Typical topology: An endhost trying to visit another location. The requesting host tries to find out something, so then there will be a dns request to the umass address. So first, you will talk to the local server. If the local server doesn't know anything about the address that you asked, then it will send a request to the root DNS server. The local server will then get a result from root DNS that sends it to TLD DNS, the TLD will then tell you that the authoritative server that knows who umass address. So lastly, the local server contacts that server and get the address.

> Iterated query, the server you connect replies with the name of the server to contact. As in the current server doesn't know about your query, the server will send a different server to contact.

### Recursive Query

Instead of passing which server to contact, each contacted server will contact the server that is needed to contact. Until it finally finds the address that needed to be found, then it will pass the result back.

Once any name server learns mapping, it caches mapping.

DNS mapping only exists for a period of time.

> Conclusion about DNS is basically an endhost tries to visit location. Contacts a local server. Local server know or doesn't know the address of location. If know return address, if don't know contact root server, and then figure out the address by multiple contacts. When you have the address, create a mapping for the address and save it in the cache for future reference to ease burden from next connections.

### Attacking DNS

- Man in middle attack : 2 nodes trying to communicate. Node A sends something, node B sends a reply. In the internet we want to confirm whether Node A is really sending and node B is really replying (preventing IP spoofing). However, there is a person between the two nodes that are intercepting all the communications and forwarding to the two nodes, making them believe they are communicating with each other. Meanwhile the middle node gets all the information.
- DNS Poisoning : send bogus replies to DNS server, which caches the fake replies, making a request link to somewhere else.

## P2P Applications

Bottleneck of file transfers are clients with the lowest downloading speed. Or the server can be the bottleneck (unlikely, most of the time the client is the bottleneck) due to low uploading speed. And the last possible bottleneck is the server and users working together to upload NF files (N items of F filesizes).

### Napster

Users need to install application, after installation, report status to central directory server (if you are on or not, what kind of files in disk space, these are uploaded to server). Directory server will check who is online and what sort of content is available in the disk space. Then get the client with highest bandwith and smallest delay with the user that wants to download, and then make the user download from that client. The central server only maintains a list of who has a certain file.

User wants to find out who has something, send request to server. Then server will inform you with the best user that can serve you. Then user will contact the server user and download the item. Scalability of the system is nice since all traffic happens between users.

Issue with Napster is legal issue. As it means that if at least one user is paying for a certain mp3 file, any other user can access the file for free.

This is a server peer to peer.

### Gnutella

Searching in a peer to peer situation is extremely tough. Due to the propagating query. Even though a peer has already returned the answer, other peers may not be able to find out this information. So the issue with P2P search is it is not comprehensive (might not get result) and inefficiency.

This is pure peer to peer.

### KaZaA

Hierarchical structure. Basically a super-peer system. There are super peers that act as servers (like in Napster system) if this super node knows of the information, then it will inform the requesting node. If not the super node will communicate with other super nodes in a pure peer to peer way (like in Gnutella).

> In cluster, like napster, among super nodes, like Gnutella.

### BitTorrent

Strategy is if you contribute more, you have a higher chance to get served better.
