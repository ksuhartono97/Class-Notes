# Mass Storage Systems

## Moving Head Disk Mechanism

There are multiple disk platters that are covered with magnetic materials to store information. These platters are separated into tracks that are subdivided into hundreds of sectors even.

There is a head that just "flies" above the surface of each platter, and memory access is done by spinning the

## Solid State Disks

Non-volatile memory (you can store things permanently) and is very fast.

Key advantage is :

- how fast it is
- power efficiency
- reliability.

Issues:

- Dollar to byte cost is large
- Maximum capacity is not comparable to standard HDD (magnetic disks)

That is why usual usage of this SSD is as a cache on magnetic disks, or as main disks on computers.

## Magnetic Tapes

Early secondary-storage medium. Used to be used in the past, but not anymore.

## Disk Attachment

Usually they use buses to connect the disk to the computer.

There are also Fibre channels.

## Network-Attached Storage

SCSI protocol used to be called the high speed protocol for connecting to storage systems that are remotely accessed.

## Disk Scheduling

### FCFS: First Come First Serve

Is fair but doesn't provide fast service, needs to go through a lot of head movement.

Not good because we have to keep moving and retouch the same place multiple times

### SSTF: Shortest Seek Time First

A form of SJF scheduling, may cause starvation but much lesser amount of head movement compared to FCFS.

It doesn't always mean that SSTF is always better compared to FCFS, it depends on the sequence.
