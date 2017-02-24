# Process Concept

Process is a program in execution

Differentiate program and process. Program is **passive** it is a file containing a list of instructions. Whereas process is **active**.

Program becomes a process when it is loaded into the memory. One program can be used by multiple processes.

## Process States

- New : memory allocated for the process. Process is being created. Also means that it is waiting for system resources before being ready.
- Running : Only one process can be in this state at a time.
- Waiting : This state means you are not ready or you are not running. Basically means you are waiting for something to complete before you can run.
- Ready : Process is waiting to be assigned to a processor.
- Terminated : process has finished execution. Memory deallocation occurs here.

Processes has a maximum runtime during one single cycle. To allow optimization of CPU usage.

**Process Control Block (PCB)** contains all information about a process.

## Threads

Multithreaded execution allows running multiple processes simultaneously. Which allows users to have some processes running concurrently.

The thread is the execution unit of a process.

When you have multiple threads that belongs to a process, you can execute different functionalities of the process simultaneously.

Program exists independent of a process. However, a process exists due to the existence of a program.

## Process Scheduling

Process scheduler selects among multiple available processes for next execution on CPU.

There are multiple queues:

- Job queue : set of all processes in the system
- Ready queue : set of all processes in the main memory that is ready and waiting to execute
- Device queue : set of processes waiting for an I/O device.

There is a correspondence between the queue a process is on and the process's state.

### Schedulers

Two types:

- Long term scheduler (or job scheduler) : selects the processes that should be in the ready queue. Controls the **degree of multiprogramming** : the number of processes that can be concurrently running in the system. If the degree is high, then there are a lot of processes causing the resources to be distributed thinly.
- Short term scheduler (or CPU scheduler) : Among the processes that are in the ready queue, decides which process is gonna run next and how long will it run (the time slice).
- Medium term scheduler (not all systems have it) : when degree of multiprogramming is too high. This scheduler will be added if the workload is too high. At this situation, this scheduler will swap out the process into the disk and leave it there and then return the process when system workload is lighter.

Main difference between the two (other than their functionalities) is the frequency of execution. Short term scheduler will be executed more frequently compared to long term scheduler.

A process that has been selected to run **will** occupy a certain amount of system resources, regardless of their state.

> Fact: Schedulers are processes too! They have a priority over other process in terms of system resources.

### Context Switch

When CPU switches processes, the system must save the old process's state and load the saved state for the new process using a **context switch**. The context is represented in the PCB (specifically in the stack).

## Process Creation

A **parent process** creates a **child process** which in turn creates more child processes. Creating a tree of processes.

A process is identified usually by the **process identifier** (pid).

Address space:

- Child duplicate of parent(same program and data)
- Child has a new program loaded into it

Forking will cause the creation of a new process that is running the same program (same code). That program is run by independent processes.

Requirement to create a process:

- Must construct a new PCB
- Must set up new page tables for the process : more expensive, basically memory allocation.
- Copy data from parent process? : done by `fork()`
- Copy I/O state

Return values of fork:

- To the parent : children's pid if successful (positive number) or -1 if failed
- To the child : 0 if successful, if failed then the child won't even exist.

### Forking

The reason why forking is done is because we want to speed up the process of process creation. So rather than remaking everything from scratch, the process just needs to copy the structure from the parent.

Usually in the program, after fork is done you should specify what the parent should do and what the child should do. Basically you should find out what process is this on and what should each process do.

Notes:

- We have no idea which process is going to run first, parent or child. Because it depends on the scheduler. The result should be the same in the end though. So in program design, you should never rely on the order of process execution.

> Concurrently is not the same as simultaneously, concurrence means the processes are all in the system and will eventually be all executed. Simultaneously means its done now.

## Process Termination

Cascading termination, termination of parent terminates all child processes.

Zombie process : parent is not waiting for the termination of a process. At this state, the process is almost done being deleted. However, the parent still has a pointer to the child process. Before wait is called then the child process still exists in the OS data structure even though it is practically dead.

Orphan process: the process does not have a parent referencing this child process. It is just dangling freely and doesn't exist in the process data structure. Linux and UNIX will always assign an **init** process to orphaned processes that calls wait periodically to reclaim system resources when the orphan is terminated.

> TLDR: orphan is your parent process is terminated. Zombie is that the process is almost dead, but not completely cleaned.

## Interprocess Communication

Cooperating process usually needs an interprocess communication (IPC) mechanism that allows them to exchange data and information. Two common models of IPC:

- Shared memory
- Message passing

### Message passing

Process communicate with each other without resorting to shared variables. Communicating through sending and receiving messages.

#### Direct communication

Creates a direct link to the target process. And if you want to receive, then must create a receiving link from the target process.

#### Indirect communication

Uses mailboxes with unique ids, and process can only communicate with each other if they share mailboxes.

After finished sending and receiving messages, the processes should destroy the mailbox to reclaim the resources given to the mailbox.

#### Synchronization

Blocking or non-blocking:

- Blocking is synchronous : blocking send / receive
- Non-blocking is asynchronous : non-blocking send/receive

Both sender and receiver are blocking : rendezvous

#### Buffering

- 0 capacity : both side blocking
- Bounded capacity : finite length, if full then sender must wait
- Infinite capacity : Sender never waits.

### Sockets

Defined as endpoint for communication.

Essentially if you want to establish communication to a web server, then you need the IP address of the machine and you need to identify the process id that is running the content that you want to connect to.

Port number identifies which process/application you want to connect/communicate with.

Only client can initiate communication to the server.

Server has to be running all the time and has to be always be ready to accept communication all the time.

> Server doesn't contact the client.

4-tuple that uniquely identifies a communication request : [source ip, destination ip, source port, destination port]

### Pipes

Acts as a conduit allowing two processes to communicate.

In the case of bidirectional communication:

- Fully duplex : both directions can send at the same time
- Half duplex : when one direction is sending the other must wait until that direction is finished before it can send.

Still different from unidirectional communication because it is only supposed to go one way.

#### Ordinary Pipes

Communication in producer-consumer fashion or unidirectional. The producer always puts in at one side of the pipe and the consumer receives on the other side.

> Called anonymous pipes in Windows

This pipe is only created unidirectional. So if you want to communicate both ways between the parent and children, then you need to create two pipes.

If the parent children relationship no longer exists, the pipe no longer exists either.

Basically this type of pipe is associated with the process, it cannot be independent of the process.

#### Named Pipes

Allows any process to share the pipe. Can associate multiple processes with it.

Bidirectional.

Even though the process terminates, the pipe still exists due to it being created by the OS.
