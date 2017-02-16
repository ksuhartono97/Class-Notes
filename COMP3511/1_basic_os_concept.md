# Basic OS Concept

## Computer Startup

Bootstrap program is loaded at power-up or reboot time (the init software):

- Stored in ROM or EPROM (erased programmable ROM)
- Initializes all aspects of the system
- Loads OS kernel and starts execution (kernal is the essential function of the os that we are currently running in the system).

## Interrupts

Interrupt transfers control to an interrupt service routine

Types:

- Polling
- Vectored interrupt system

A trap or an exception is a software-generated interrupt caused either by an error (e.g., division by zero) or a user request for operation system service

All modern OS are interrupt driven

## Operating System

Is a program that acts as an intermediary between a user of computer and computer hardware.

OS goals:

- Control and coordinate the use of system resources
- Use computer hardware in an efficient and protected manner (have security such that the hardware configuration cannot be arbitrarily changed by a program)
- Make the computer system easy to use.

There is no universally accepted definition of an OS.

### Timesharing

Basically creates an illusion that the user has a dedicated environment that it is interacting with. So that even though the computer is actually doing multiple jobs, the user will feel like the computer is solely serving the user.

Time shared OSes allows sharing of the computer.

### Operating System Operations

#### Dual Mode

Two modes, user mode and kernel mode. Kernel mode has specific instructions that are executable only in that mode. The user mode cannot access these.

The reason for this is so that the user cannot alter important settings on the computer.

However, if a user in user mode needs to do something that needs the kernel mode, there is a system call that can be used to execute that command in kernel mode, and when the job is finished, it will return to user mode.

Allows protection of the OS from users.

#### Single Processor Systems

#### Multiprocessor Systems

Two types:

- Asymmetric Multiprocessing - one master CPU distributes tasks among multiple slave CPUs, or boss-worker relationship
- Symmetric Multiprocessing - all cpus share tasks (most common)

Symmetric multiprocessing:

- Has its own set of registers and local cache
- Shares physical memory
- Usually the number of processors are powers of two (dual core, quad core)

#### Cluster Systems

Composed of multiple individual systems (at least two)

### Computing Environments

#### Client-Server

There is a main computer that is the server and all computers will connect to the server

#### Peer-to-Peer

Doesn't differentiate client and server, all are called peers.

#### Virtualization

OS(guest) running within another OS(host).

Allows running applications that is not targeted for the native OS.

#### Cloud Computing

Delivers services as a network, is based on virtualization.

Is composed of traditional OSes plus a Virtual Machine Manager.

#### Real Time Embedded Systems
