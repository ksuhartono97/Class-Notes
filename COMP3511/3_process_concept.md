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

###Schedulers
Two types:
- Long term scheduler (or job scheduler) : selects the processes that should be in the ready queue. Controls the **degree of multiprogramming** : the number of processes that can be concurrently running in the system. If the degree is high, then there are a lot of processes causing the resources to be distributed thinly.
- Short term scheduler (or CPU scheduler) : Among the processes that are in the ready queue, decides which process is gonna run next and how long will it run (the time slice).
- Medium term scheduler (not all systems have it) : when degree of multiprogramming is too high. This scheduler will be added if the workload is too high. At this situation, this scheduler will swap out the process into the disk and leave it there and then return the process when system workload is lighter.

Main difference between the two (other than their functionalities) is the frequency of execution. Short term scheduler will be executed more frequently compared to long term scheduler.

A process that has been selected to run **will** occupy a certain amount of system resources, regardless of their state.

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
