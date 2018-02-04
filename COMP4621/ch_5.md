# Link Layer

For different links (ethernet, 4g network, etc) each have a different link protocol.

Frame: basic unit of the link layer

Wireless link generally has high bit error rate, and it has a unique nature as wireless transmission can experience bursty errors, when it experiences an error, it tends to stay there for a bit.

In bit error prone link, it is very likely something was changed during transmission. Therefore you add a portion of redundant data bits (EDC bits).These serve as error checking, later we check these EDC bits to see whether the damage is repairable or not (error checking).

CRC (Cyclic redundancy check), a more reliable error checking.

## Multiple Access Protocols

Collision happens in the receiver side, when there are multiple nodes that want to communicate to that receiver.

Ideal protocol takes note of:

- Fairness
- Distributed
- Simplicity

3 broad classes:

- Channel partitioning, ensures exclusiveness, ensure that collisions never happens.
- Random access, allow collisions to happen (random access, collisions can happen anytime) but emphasis more on recovering from the collisions.
- Taking turns: nodes will take turns to use the channel, can allow varied time in using the channel.

### Channel Partitioning

Divide it based on:

- TDMA (time division multiple access) : each user accesses the channel in a period of time (has a timeslot). Can cause low utilization as unused slots become idle.
- FDMA (frequency division multiple access) : has the same issues as TDMA, as when the channel is assigned and it isn't used it is a waste.

### Random Access Protocols

We know that there is a lot of bursty transmissions in the channel, and we want to utilise the full speed to transmit when I need to transmit, and do not want coordination (division of slots between channels).

#### Slotted ALOHA

Is a simple version, transmission time will be divided into slots (hence slotted ALOHA), and the length of the slot is the same size (to make it simple).

If there is a collision, you need to recover from collision by doing retransmission. There is a random probability for the nodes that want to transmit, so it should reduce the probability of the node having collision again in the next slot (although it is still possible). The probability is the same, but the chance that you visit a certain channel for a particular slot is different.

If no collision, simply continue transmission.

But this protocol have a significant probability for collisions, so there is a lot of wasted slots.

Protocol's efficiency, is looking at the long run, if there are nodes that have saturated traffic and they all have slots, what will be the long run fraction of successful transmissions.

And for this protocol, the max efficiency is 37%.

#### Carrier Sense Multiple Access (CSMA)

Revisits human behaviour, when you want to talk to somebody, but you find out someone is talking at the same time, then you will check for neighbours who are talking, wait for them to stop, and initiate conversation when they are finished. This is what is applied in this.

Basic idea is we should listen before transmission, we have to ensure that there is no one else talking.

Collisions can still happen due to propagation delay, causing the nodes to not hear each other's transmission.

#### CSMA/CD (Collision Detection)

Check for collisions, if you detect a collision, then just stop the transmission, reducing the channel waste.

Would work only if we can detect the collision, and is much easier in wired LANs, but difficult in wireless LANs.

When collision is detected, you wait for a little time before trying retransmission (backoff period). With more collisions, the backoff will be a longer time (exponential backoff).

### Taking Turns Protocols

Polling: master invites slave nodes to transmit, if you are invited, then you can use full speed to transmit (master has a lot of burden).

Token passing: a control token being passed, whoever has token can transmit with full speed. But the token is a single point of failure. 
