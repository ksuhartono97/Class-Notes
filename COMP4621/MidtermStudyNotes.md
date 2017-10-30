# Midterm Study Notes
## Chapter 1
A protocol defines the format and order of messages sent and received among network entities, and describes the actions taken on message transmission and/or receipt of a message.

5 layers in the internet protocol stack:
- Application : supporting network applications
- Transport : process-process data transfer
- Network : routing of datagrams from source to destination
- Link : data transfer between neighbouring elements
- Physical : bits "on the wire"

5 services that use internet services:
- Web
- Email
- VoIP
- Multimedia
- Online Games

### Packet Switching vs Circuit Switching
Packet switching is when data is separated into packets, these packets are then transferred to the target router, and reassembled there. Whereas circuit switching is when hosts who are going to communicate with each other gets assigned specific circuits, granting them access to the resources to communicate and send data at any time.

The benefits of packet switching is that it has better scalability and is able to support infinite number of concurrent users (however the delay would be extremely huge, not to mention packet loss). It also has great resource utilization in the case of transmitting packets all the time. The problem with it is availability as the network is servicing everyone at the same time, it may not be able to do what you want instantly. (delay)

The benefits of circuit switching is the ensured all time access for both hosts, they can communicate anytime they want as the resources are always available. The problem with it is that it has limited number of resources (not as scalable) and it has resource utilization problems as the resources are reserved for the use of only the two hosts (other people who need it can't use it)

Use binomial distribution to figure out probability.

### Two key network core functions
- Routing: figures out a source to destination route that the packet will need to take.
- Forwarding: moves the packets from router's input to appropriate router's output (to be moved again to target)

### FDM and TDM
FDM is frequency division multiplexing, the channel is divided into different bandwidths that is not overlapping with each other. Users are then assigned to frequencies that they can use.

TDM is time division multiplexing. Where users get the channel for a certain period of time where they can use the channel.

FDM is better in the sense that there is a smaller amount of latency as the user has access to the frequency at all time, meaning it can transmit whenever it would like. But TDM is better because it is more flexible, as the resources are allocated based on time, users with higher demand can be dynamically allocated the resource for a longer time.

The problems with each of them is exactly the pros of the other.

### Delays
Calculated with `L * a / R` where
- L is packet length
- a is average packet arrival rate
- R is the link bandwidth

### Layering
Layers as needed as networking is complex, therefore we'll need to split up the problem into layers, where each layer has to only interact with adjacent layers and deal with its own business, simplifying the problem.

Layering is not necessarily the best solution but it is good due to the its scalability.


## Chapter 2

### Application Architecture
Client-server:
- Always on with a permanent IP address
- Client do not directly communicate with each other

P2P :
- No always on server
- Arbitrary end system directly communicate with each other
- Better scalability

### Addressing processes
Need to use both IP address and port number to directly specify which process running on which port had requested.

### TCP and UDP
TCP:
- Is connection oriented
- Provides reliable data transfer, flow control, and congestion control

UDP:
- Does not need a connection (connection less).
- Unreliable data transfer

TCP is slower than UDP, no timing guarantees as it has a higher overhead.

SSL provides security to TCP by encrypting the connection

### Web and HTTP
HTTP, hyper text transfer protocol:
- Uses client-server model
- Uses TCP for connection
- Is "stateless" : maintains no information about past client requests

Non-persistent HTTP:
- One object sent per HTTP connection
- Downloading multiple objects needs multiple connections

Persistent HTTP:
- One HTTP connection required, connection will not be closed

> Notes, for non-persistent, 2 RTT to send HTML object and 2 RTTs per object in html file(if not parallel, if parallel then only 2RTT for all objects). For persistent, 2 RTT required to send HTML but only 1 RTT for all objects inside it (each for non-pipelined and only one RTT if pipelined).

> Time to transfer the HTML object always exist. For the rest of the objects, depends on the type. If it can send all the same time, consider only the longest. If not, the sum of all the transmission times.

HTTP Request Messages:
- Standard format :
  - request line :  method, URL, version. Ex: `GET /index.html HTTP/1.1\`
  - header line : header field name, value. Ex : `Host: www-net.cs.umass.edu`
  - body
- Post method : input is uploaded to server in entity body
- URL method : uses GET method, the input is uploaded in the URL of the field of the request line.
- Method types:
  - Ver 1.0 : GET, POST, HEAD
  - Ver 1.1 : GET, POST, HEAD, PUT, DELETE

HTTP Response Messages:
- Format:
  - Status line: protocol, status code, status phrase. Ex: `HTTP/1.1 200 OK\`
  - Header line: HTML headers
  - Data
- Sample status codes:
  - 200, OK : request succeeded
  - 301, moved permanently : request object moved
  - 400, bad request : request message not understood by server
  - 404, not found : requested document not found in server
  - 500, internal server error : server cannot process request for some reason

### Cookies
Used for messages that carry state.

Consists of 4 components:
- Cookie header line of HTTP response message
- Cookie header line in next HTTP request message
- Cookie file kept on user's host managed by user's browser
- Back end database at website

### Caching
Needed to increase internet speed, as a cheaper and more viable solution compared to increasing bandwidth speed. Works in the sense that hits in the cache would reduce traffic to actual request to the server, as in satisfy the client's request without actually involving the server.

Formulas:
- Access link utilization : Average request rate / Access link rate. Remember to scale it with amount that actually goes to server (not in cache).
- Total delay : normally, Internet delay + access delay + LAN delay. If with cache then: (percentage not in cache) * (delay from origin server) + (percentage in cache) * (delay when satisfied in cache).

#### Conditional GET
Basically, do not send object if cache has an up-to-date cached version. Used between client and the server(cache). Only sends an html code 304 for not modified.

### FTP
Uses port 21, used to transfer files to/from remote host. Uses out of band protocol.

> In band protocol is when control messages and data messages may be interleaved in the same TCP connection. Whereas out of band protocol means that control messages and data messages are carried in separate TCP connections. HTTP, DNS, SMTP are in band. FTP is out of band.

Process:
- Client contacts FTP server at port 21 using TCP
- A connection is established over control connection.
- User browses files, selects file for FT
- FTP opens 2nd TCP connection and closes the connection after transferring the file
- Repeats that for each file

### SMTP
Uses port 25, used for transferring mail.

Three phases of transfer:
- Handshaking
- Message transfer
- Closure

Uses persistent connections, requires message to be in 7 bit ASCII, uses CRLF as end of file.

Mail Access Protocols:
- POP : authorisation and download
- IMAP : more features regarding manipulating mail in the server
- HTTP : modern stuff

### DNS
Domain name server, used to identify name-servers. Services provided:
- Hostname to ip address translation
- Aliasing hosts
- Aliasing mail servers

Hierarchy:
- Root : highest level, has a directory of all the TLDs
- TLD : has a directory of all the authoritative servers (high level domain)
- Authoritative : the local networks

2 Types of query:
- Iterative : server asks other servers, if it doesn't know, will be directed to a server that knows where the site the server is looking for is.
- Recursive : burden on server that was asked to find, creates high demand on upper levels.

Resource record types:
- A : value is IP address
- NS : value is hostname of authoritative name-server for this domain
- CNAME : value is alias name for some canonical name
- MX : value is name of mailserver

#### Attacking DNS
- DDoS : bombard root servers with traffic, not usually succesful due to traffic control in root. Local DNS also caches routes, making the requests go to local instead of root. Instead now people bomb the TLD caches instead of root, which is more dangerous.
- Man-in-middle : query interception, there's a third party listening to all the packets
- DNS poisoning : sends bogus replies to DNS, which caches the reply, making subsequent queries lead to the wrong address.

#### P2P applications
File Distribution Time Equation:
- Client server : MAX{NF/Us, F/dmin}
- P2P: MAX{F/Us, F/dmin, NF/(us + Sigma(ui))}

P2P apps:
- Napster: uses a centralized directory server for P2P. Efficient, because it was centralized. But, performance bottleneck. Even though this is server peer to peer
- Gnutella : no server, can handle complex queries, and robust. But it is not comprehensive and inefficient. BUT this is pure P2P
- KaZaA : hybrid architecture. There are super peers that acts as servers (supernode). Clients communicate to the super peers to gain the information.
- BitTorrent : P2P, but if you contribute more, you get more bandwidth.


## Chapter 3
TCP : provides reliable data transfer, flow control, congestion control. UDP : provides unreliable data transfer, but with less overhead, meaning faster.

### Multiplexing
Basically multiplexes at sender, which allows users to communicate with different destinations at different sockets. And demultiplexing at receiver allows users to communicate with different sources at the same time.

UDP identification : port number only
TCP identification : 4 tuple, Source IP, Source port number, destination IP, destination port number

### UDP
Characteristics:
- Unreliable, meaning data can be lost or unordered (best effort service)
- Connectionless

UDP header : Source port #, Dest port #, length, checksum (8 bytes/64 bits)

Benefits:
- No connection established, meaning less delay
- Simple
- Small header size
- No congestion control (can use as much of bandwidth as possible)

Checksum, created by treating the contents as 16-bit integers and adding them together to create a 16 bit checksum. On receiving end, sum the data packets again. If result of sum is different from checksum then something went wrong.

### RDT
Order:
- rdt_send()
- udt_send() : send data through unreliable channel
- rdt_rcv() : when data received
- deliver_data() : called by rdt to deliver data to upper level

- Version 1.0 : assume underlying channel is perfectly reliable (the channel with which udt_send() is called). Thus just follow order above. As there are no problems.
- Version 2.0 : bits may get flipped during transmission. Solution is checksum to check if there are flipped bits. But how to fix the transmission error? Using acknowledgments to tell if the file has been corrupted or not. ACK for OK, NAK for error. So the FSM is upgraded. After receiving call from above, send the packet and transition to wait for ACK/NAK state. Then when ACK/NAK is received we check it. If it is NAK, resend packet and wait for NAK. If ACK then go back to wait for call. For the other side its the same as before, however now there's an ACK/NAK sending after data received.
- Version 2.1 : The problem with this is what if the ACK/NAK gets corrupted, can't just retransmit as there might be duplicates. So sequence number is added to differentiate the packets from one another for duplicate prevention. If receiver receives duplicate, it can just discard it. But this creates a STOP and WAIT status for sender, sends one packet and wait for response (very slow rate). Only uses 0 and 1 for sequence number, and is used alternatingly. Basically sender has to handle 2 states(ACK or NAK), receiver 3 states (send ACK when correct, NAK when wrong, NAK when duplicate)
- Version 2.2 : same as 2.2 but removed NAK. Replaced the functionality of ACK with sending the previous correct ACK. (So if last packet received is 0, and is expecting 1 but not getting 1, send back ACK 0, prompting sender to resend).
- Version 3.0 : new assumption, packet can be lost. To solve this, we basically introduce a timeout concept. Where the sender waits a "reasonable" amount of time for an ACK. If after this time there is no ACK, retransmit packet. So basically, adds an extra criterion to sender FSM, if timeout, resend. If receive ACK, stop the timer.

RDT 3.0 is correct but performance is bad.

### Pipelined Protocols
Sender allows multiple in flight packets. Two generic forms:
- Go-Back-N
- Selective Repeat

#### Go Back N
Basically, retransmit all packages if any of the packages get lost. All in a sense that after the latest ACK. So if there are 5 packets and signal lost on packet 2, retransmit packet 2-5 only. When all 5 finish, move window.

#### Selective Repeat
Each packet has a timer, if any of them timeout, retransmit.

### TCP
Characteristics:
- Point-to-point
- Reliable
- Pipelined
- Full duplex
- Connection oriented
- Flow Controlled and Congestion controlled

Estimated RTT = (1−𝛼)∙𝐸𝑠𝑡𝑖𝑚𝑎𝑡𝑒𝑑𝑅𝑇𝑇+𝛼∙𝑆𝑎𝑚𝑝𝑙𝑒𝑅𝑇𝑇

If unreadable : (1 - alpha) * Estimated RTT + alpha * Sample RTT
>First time estimated RTT is sample RTT. I.E. first iteration will basically give the RTT time as a result.

#### TCP RDT
Behaviour of receiver side:
- Inorder segment, all segments acked : delayed ACK, wait 500 ms, if no segment then ACK
- Inorder segment, segments unacked : immediately send cumulative ACK, acking all segments
- Out of order segment, seq # larger than expected (gap) : immediately send duplicated ACK with expected seq #
- Out of order segment, fills gap : immediately send ACK, provided segment fills gap from left end side.

#### Fast TCP
Do not wait until timeout, if 3 duplicated ACKs received, we know something went wrong. Retransmit the unacked segment with smallest sequence number. Remember, out of order segment with gap sends duplicated ACK, but that segment gets buffered.

#### TCP Flow Control
Receiver controls the sender so that the sender won't overwhelm the receiver by sending too much data too fast.

Is done by splitting the buffer into two parts, the RCV-buffer and the rwnd part. The rwnd buffer's size can be controlled so that the receiver doesn't get overwhelmed.

#### TCP Connection Management
- 2 way handshake : before establishing connection, do handshaking between sender and receiver to confirm that both agree to communicate.
- 3 way handshake : starts with sender sending SYN, server receives sends SYNACK. Sender receives SYNACK, sends a SYNACK for that SYNACK and establish connection. Server receives reply, establishes connection.
- Closing a connection : Client sends FIN bit, can no longer send data now, server replies with ACK FIN. Then after some time, server sends a FINbit indicating server is done, client sends an ACK for that FIN, and then when server receives that ACK, it gets closed. While client closes itself after a timed wait period.

#### TCP Congestion Control
Congestion : too many sources sending too much data for Network to handle. Causes packet delay and packet loss.

2 methods:
- End-end congestion Control : no explicit feedback from network, congestion inferred from system loss, delay
- Network assisted congestion control : explicit feedback from network, network sends an amount that specifies the transmission rate that it can handle.

ATM ABR Congestion control : utilizes the available bit rate, which is elastic, can tell sender to either use bandwidth, or throttle. Done by interleaving an RM cell, between transmitted data, with 2 bits, NI and CI (NI means no increase in rate and CI means congestion indication). This cell is modified by receiver and sent back to sender.

TCP methods:
- AIMD (additive increase multiplicative decrease) : basically probing the network. Increase transmission rate until delay/loss starts to happen, when that happens, half the transmission rate. If no delay/loss keep on increasing rate by 1 MSS. (cwnd or congestion window increased by 1 MSS and halved when congestion)
- TCP Slow Start : basically, what is done is the cwnd always starts from 1 MSS, then keep on doubling cwnd size until first loss event. Loss event is indicated by a timeout or 3 duplicated acks (fast retransmit). Then there are 2 methods:
  - TCP Tahoe : reset the cwnd size to 1
  - TCP Reno : half the cwnd and then increase linearly (AIMD)

Concept is use Tahoe when timeout and Reno when duplicated ACK.

When the slow start MSS is bigger than the threshold, we switch to AIMD.

Average throughput is 3/4 * window size / RTT
