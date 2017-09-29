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
