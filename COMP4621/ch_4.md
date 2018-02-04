# Network layer

Key functions of the network-layer:
- Forwarding : push out to an output port, within a router (from an incoming port)
- Routing : finding out the right path from one location to another

Local forwarding table, updated by routing algorithm

Between routing and forwarding:
- First translate the address
- Then check in the local forwarding table

Used to ensure whether a datagram can be transmitted from a router to the other.

## Connection Setup
In network layer, connection setup is done between two hosts and also all the intermediate routers.

## Virtual Circuit and Datagram Networks
Will be different based on whether the network is connectionless or a connection service. Datagram for connectionless and virtual-circuit for connection service.

### Virtual Circuit
Behaviour like telephone network, resources are allocated for you and only to be used by you. There is a performance guarantee. But the system will have to decline the request if the network is too busy.

In virtual circuit, before actually transmitting data (communicating), there needs to be a process of signalling. All the routers and end hosts communicate with each other to allocate resources. This is not possible for internet as it is too heavy.

### Datagram
When you have an address as a destination, check local datagram, then do longest prefix matching to find the port that you have to go to, so you can reach the destination.

In conclusion if you need speed, you should use datagram, if you need systems that need performance guarantee and doesn't mind loss like VoIP, video transmission, etc, you can use the virtual circuit format.

## Input Port functions
After passing the physical and link you enter the network layer, here you will see a datagram, and based on the table, you decide which output port to push to.

But if the arrival rate is faster than the pushing rate, there needs to be a place to hold the arriving datagrams, so here is the first place where we have a buffer. (This is the first place where congestion occurs).

Need two buffers to do rain-matching.

Even when output port for a certain packet is idle, but the input port is busy, and the scheduling if FCFS, then the packet will not get served.

First performance metric is how fast you process the datagram, and the second metric is the overall utilization of the system

## The Network layer
Need to have an IP protocol to ensure that all end hosts understand what is being communicated. Important point is:
- Addressing conventions: as we have to ensure consistency on how to name each endhost.

### IP datagram format
IPv4: 32 bits to represent source IP address and another 32 bits to represent the destination IP address.

However, internet became big, and 32 bits become not enough. So in the modern network, we use IPv6 to represent IP networks.

IPv6 : 128 bits, so we assume that anything in the world can be represented with a unique IP address. These two protocols, will then coexist up until now.

> Never make the assumption that everyone in the world will just switch to your protocol. It is simply too big of a system for it to be shared to everyone.

The IP protocol will understand that the upper layer has different types of traffic going on (video, media, etc). This traffic is like a background file transfer going on. When there is resource contention, we can base it on the nature of the traffic and attempt to do something differently.

The IP datagram has a field called **time to live**. For every datagram, when it passes through a router, this field is reduced by 1. When this field becomes 0, it means that this packet has reached its maximum number of hops and this packet will get dropped, then the router will have to report an ICMP message to source that the packet is dropped.

The TTL starts at 1, and then it will be sent to a router, if it hasn't reached the target router, it will get dropped as TTL is 0, so as mentioned above, a message is sent to source. Then the datagram will get resent with TTL 2, and the process is repeated.

The very basic overhead from IP datagram is 20 bytes, and then from the TCP header, another 20 bytes. So at the very least we have to support 40 bytes overhead. However there will be more overhead from the app layer.

Note that version is usually the same, type of service is usually the same, and also the source and destination should also be the same. So for very narrow networks, ITF thinks that we should do header compression.

#### IP fragmentation, reassembly
For different types of links, they have different MTUs (Maximum Transmission Unit). Since the maximum capacity of the size of a datagram that can be sent is varied, we will have to fragment the datagram to smaller pieces when sending through a link with a small MTU.

The fragmented flag will have a fragflag, which is set to 1 when it is fragmenting, the last segment will have this flag set to 0, to indicate that the fragmentation is over.

#### IP Addressing
IP address, a 32 bit identifier for host and routers. But an IP address is not associated with the device, it is associated with the network interface. So that each device may have multiple IP addresses due to the large number of network interfaces.

A network interface itself is the connection between host/router and a physical link.

Subnets, are areas where hosts can communicate with each other without using the router.

CIDR : Classless InterDomain Routing,

How to obtain an IP address?
- Hard coded by system admin in a file.
- DHCP : dynamic host configuration protocol, a plug and play protocol, just turn on and run protocol, no need for any setups or configurations.

## Routing Algorithms

### Distance Vector
Is a distributed design.

Link cost change implies the appearance of bad news, and this bad news actually travels very slowly.

### Hierarchical Routing
Consists of AS networks.

## Routing in the Internet

### Routing Information Protocol (RIP)
The distance metric is hops, where each link has a cost of 1. We do not want dynamic distance metric as it'll keep on changing.

### Internet inter-AS routing: BGP
BGP tries to let everyone know, that there is somebody in the world, if you want to reach them, there is a way to do so.

Everyone in the AS periodically broadcast a message(advertisement), so that if someone new comes into the network, they know that they exist, and they know how to contact them.

Gateway router, when it gets a path advertisement from a node, it doesn't necessarily receive the ad, it could just forward and broadcast it to the network.

### Why different routings
Policy:
- Inter-AS: there are multiple admins, and each admin would want to control over how traffic is routed, and who is routed through the net.

## Broadcast and Multicast routing
Source duplication is very inefficient and not doable, due to the fact that there is simply no way of knowing who to send your packet to.

### In network duplication
- Flooding : when a node receive a packet, broadcast it to all neighbours. Very traffic heavy. There's so many messages going on, also there is the cycle that can be caused. When A1 is a neighbour to A2 and A1 sends to A2, but then A2 sends back to A1, and A1 sends again to A2, and so on.
- Controlled flooding: node will only broadcast packets if it hasn't broadcasted it before, eliminates the cycle problem.
  - RPF : reverse path forwarding, forward a packet only if it has the shortest path between node and source. Meaning that it will only do flooding if the node that receives it received it from the source. As shortest distance is only possible if you are the first node.
- Spanning tree: allows no duplicated packet. The idea is to construct a spanning tree, where in the tree each node will send a unicast message to all nodes.

### Multicast Routing
You want to be able to do one to many broadcasting. There are a lot of applications that needs this kind of network support.

The solution for multicast should come from the application side, not the network side. This is due to the complexity it creates for the network layer. Causing the network layer to become not scalable, which is why it is impossible to do.

This is achieved through the use of the tree system again, and this tree will need to be constantly maintained.

Pruning: when a user quits the system, you need to send a pruning message, requesting to be removed from the tree. 
