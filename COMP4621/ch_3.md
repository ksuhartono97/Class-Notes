# Transport Layer

Will be found in end system, not in the server(network). Will handle who is talking to who, unlike network layer that takes care of the door to door communication.

## Transport Layer Services

Transport protocols:

- TCP : efficient, reliable, in order communication protocol
- UDP : unreliable, unordered transmission, most famous instance

## Multiplexing and Demultiplexing

Multiplexing at sender side: data that will be transferred to different destinations through different sockets.

Demultiplexing at receiver side : And also you can receive information from different clients. You should know that as different segments are talking to different recipients, we must know how to deliver the right segment to the right socket.

Hosts uses IP addresses and port numbers to direct segment to the appropriate sockets.

2 Types of socket, reliable and unreliable.

When we setup a socket, we put our **local** port number. So essentially when we want to send a packet, we simply need to input the target ip and port number.

UDP is identified by the local port number only. When receiving, check the UDP segment, if the target port number is the same, I should direct all the segments to the target socket that is setup on that port number, even though the sources are different.

TCP sockets, are identified by the 4 tuple:

- Source IP
- Source port number
- Destination IP addresses
- Destination port number

Use these 4 items to decide which socket to direct the segment to. The difference with UDP is that even if the target IP and port number is the same, if the source is different, it is still demultiplexed to different sockets.

## UDP : User Datagram protocol

Popularly used to provide for media transmission. Connectionless, meaning that there is no handshaking.

UDP Checksum included in the UDP header. Used to check for errors in transmission. No error correction, only used for error detection.

## Reliable Data Transfer

Upper level evoke `rdt_send()` and then the transport layer will invoke `udp_send()`. This is because the lower level is just an unreliable channel. So you send something with UDP. Then on the receiving side it will call `rdt_rcv()` called when the packet arrives on the receiving end and `deliver_data()` to deliver data to the upper level.

## Protocol Design

### The RDT versions

- Version 1.0 : assume perfect channel, no bit error or packet loss, only care about send and receive.
- Version 2.0 : in the channel we will find some bit error with every packet. There is a guarantee that packets can be sent and received but there is no guarantee that the content is correct. Hence the availability of checksum for checking the validity of the content. If there is something wrong that is found out during checksum calculation, then the receiver must inform the sender. Thus there is a feedback system, ACK (acknowledgement) and NAK (negative acknowledgement). This version has a flaw. It assumes that the sender side will be able to receive the feedback packet perfectly, as in it will only receive ACK/NAK. But if there's is a bit error during that transmission, then the sender will not know what the receiver sent. This will cause receiver to send a duplicate packet as it doesn't know what is wrong.
- Version 2.1 : there is a packet differentiation. The sequence of FSM will be:

  - Wait for packet 0 from upper level.
  - Send packet request with sequence number 0, and other control variables such as the checksum, to ensure the validity of the data. Note that all these control variables are all overhead.
  - Then the packet with sequence number 0 is created, and sent with `udt_send()` and then wait for feedback. (assume waiting feedback for packet 0)
  - When you receive feedback, you have 2 cases:

    - Receive a correctly received feedback packet that is an ACK, which means packet is successfully received by destination. Then you can handle the next packet.
    - Received a NAK or a corrupted packet, you do the same thing, retransmit the packet. And every time there is a retransmit, the sequence number is reattached to it.

  - The receiver will now have 3 cases that it has to handle:

    - Received a packet, packet is not corrupted, and the packet is what we wanted. So then receiver will create an acknowledgement and send it back to sender. Then it will send the packet to the upper level, and then it will await for the next packet.
    - If the receiver cannot understand the packet content, it sends back the NAK.
    - If the receiver receives a packet, it is not corrupted, and is the right packet, however, the sequence number is wrong. For example, expected packet 0 but you get packet 1\. This means that there is a duplication. The issue here is that the sender cannot understand the feedback, resulting in the sender to resend the packet. And in this case, this packet just gets dropped. And then, you'll have to send the acknowledgement so that it triggers the sender to send the next packet.

- In version 2.1 a `0` and `1` state would be enough to differentiate the states of the packets for both receiver and sender. Remember that for all the packet transmissions you'll have to send a checksum with it, also beware of duplications that need to be handled correctly. This version is a complete protocol, unlike the previous versions.
- Version 2.2: removed NAK completely, if you obtain the packet you send ACK. However, if you fail to get the packet, you send an ACK of the previous received packet. Thus triggering a retransmission. In that sense, any duplicated ACK means that something is wrong in the receiver side, so you can retransmit the current packet. In the very beginning of the system, you'll have to send a special ACK that you can use so that there is the first packet that is sent.
- Version 3.0 : The previous version is able to efficiently handle transmission errors. Now we consider the assumption that some packets can get lost due to buffer size issues of the router. To handle loss, we wait for a "reasonable" amount of time for an ACK response (Should take approximately an RTT). If there is no feedback, there should be something wrong with the sent packet, so the sender will guess that the packet is lost (it is just a guess, as the sender will not be able to know what happens). If the packet is lost then the sender will retransmit. However, it is very possible that the guess is wrong and that the packet is just delayed. So it could mean that the transmitted packet could be duplicated. However this is not a big issue, as there is already duplicate handling.

> Version 3.0 basically introduces a timeout function.

### Pipelined Protocols
Two forms of pipeline protocol
- Go-Back-N
- Selective Repeat

#### Go-Back-N
Characteristic is cumulative ACK, meaning that basically if there is a gap between the packets, it won't send any ACK packets. As it suspects that something is lost.

The ACK will return a certain sequence number, meaning that if you get duplicated ACK's multiple times, it means that something went wrong during transmission.

When timer expires, will have to retransmit all packets with sequence number larger than N. (All the packets in the window).

The window and buffer size is determined by the router.

Receiver side, only receive and check whether it is what is expected. And then give feedback to sender side. The ACK side will always send the highest inorder sequence number. If the packets are received out of order, the newly received packets are dropped. And send the last received ACK, see slides for example.

#### Selective Repeat
Gives individual ACK. Extremely specific, if a packet is sent, when received I will send an ACK for the packet with its details. Sets a timer for every single packet being set, so that when the timeout happens, just retransmit that specific packet.

Sender : received data from above, check if window can receive extra packets from application level. If receive acknowledgement from receive side, mark packet as sent. Then, check if all the packets with sequence number below that packet is received already, if it is move the sliding window, else do not move it.

Receiver side : Also has a window. Simply receive the packets and send ACKs for the packets. Even if it is out of order, still mark it as sent. When all the packets are in order, move the window and send the packets to the upper level.

Efficiency wise, this is much better than go-back-n. However, you need to set a timer for every single of inflight packets. This is too much for the transport layer.

## TCP
A typical reliable data transfer protocol (the most widely and well deployed transfer protocol).

- Is a point to point protocol : has one sender and receiver
- Is full duplex : no need to setup a new connection when the receiver want to talk to sender (bi-directional, communication works two ways)
- Flow control : regulate the number of packets sent so it doesn't overwhelm the receiver. (As the buffer exists in the receiver)
- Handshaking : to ensure that both sender and receiver are ready to communicate with each other.

Has a header, similar to UDP, but has more content than UDP as this is a reliable protocol (need to have pipeline, flow and congestion control)

Uses cumulative ACKs, but we do not want to do unnecessary transmission.

### Timeouts
In TCP is related to the RTT, as in the past i've received something for the packet transmission at that amount of time. Intuitively, there should be a sort of relation that can be expected here. However using same RTT as before as a timer setting is very aggressive, as the network condition could be either better or worse than previously. If the rule is to rigid, there will be a lot of retransmits (vice versa, when too relaxed will be too conservative, wait too long).

### TCP RDT
Maintain a single retransmission timer for the oldest not yet acknowledged segment.

TCP sender and receiver

An updated acknowledgement basically tells the sender that it can proceed to send a newer version of the packet.

### Flow control
Done to make the receiver inform the sender about it's buffer capacity.

### Connection Management
Before doing data exchange, we do a handshake to establish agreement to connect and the parameters of the connection.

Will turn down the communication if after some time there is no connection happening (release resources for future connection).

#### 2 way handshake
Failure scenario : The accepted connection comes too slow, resulting a retransmit connection, however this retransmission is taking a longer time. During the time, the original accepted connection arrives and then the connection is done by the client. After the connection is finished, the retransmitted connection finally arrives at the server side. However, there is no client for that connection.

#### 3 way handshake
The server side will listen for a SYN from the client. When the server receives the SYN, it sends a SYNACK, when the client sees this, it will send a SYNACK for the SYNACK of the server and establish a connection. When the server receives the SYNACK for its SYNACK, it also establishes the connection.

#### Closing a connection
When the client has sent a closing connection request, it can't send data but can still receive data. It will wait for a server close which will be indicated by an ACK bit sent by the server. Then the server will also send a close request, and wait for ACK from the client, at this point the server cannot send any data either.

## Congestion Control
Congestion is when too many sources sending too much data for network to handle. The way to prevent this is to control the sending such that it doesn't overwhelm the network. The result of congestion is that there are long packet delays and packet loss.

### Cause and Costs of Congestion
Scenario 2 : there is a finite buffer, meaning that the router can reject when buffer is full, causing there to be a retransmission in the client. The assumption here is that there is perfect knowledge of the router, as in it will only send when the router buffers are available (unlikely to be known in reality) and to resend if the packet is *known* to be lost (very hard to know in reality)

> Goodput : the effective amount of data that you transfer through the network

Costs of congestion in this scenario is that it lowers the goodput of the network. (throughput increases due to unneeded transmissions and this decreases the goodput).

Scenario 3 : Four senders, multihop paths, and timeout or retransmit. Another cost of congestion, when a packet is dropped, any upstream transmission capacity used for the packet was wasted.

All the congestion costs imply that there needs to be cooperation to prevent network congestion. As too much congestion will decrease performance of network and even personal network.

### ATM ABR Congestion control
Interleave a RM(resource management) cell between a number of data cells. There is an ER(explicit rate) field that tells the senders about the max send rate. However, these cells cause too much overhead.

### TCP congestion control : additive increase multiplicative decrease
The sender increases the transmission rate until loss occurs (to test the rate capability of the network), the moment it detects the loss, half the sending rate. The point is we are probing for network bandwith. Sometimes called as the network probing technique. As the sender uses the protocol to estimate the network's capacity. 
