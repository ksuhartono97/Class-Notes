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

### Version 1.0 of RDT

Suppose that there is no error or loss in the underlying channel (perfect underlying channel).
