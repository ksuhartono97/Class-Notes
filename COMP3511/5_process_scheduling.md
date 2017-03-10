# Process Scheduling

4 Circumstances that might happen during CPU Scheduling :

- Switches from running or waiting state: Process that is occupying CPU gives up CPU resources **voluntarily**. This is non-preemptive.
- Terminates : Finishes execution, so it frees up CPU resources. This is non-preemptive.
- Switches from running to ready state: Interrupts. Somebody forced me to give CPU. Preemptive by nature.
- Switches from waiting to ready state: completion of I/O. Someone suddenly joins the ready queue. Due to the new process being high priority, then the scheduler might have to kick out the current process in the CPU (force give up CPU). This involuntary action is called preemptive by nature.

## Scheduling Types

### First-Come, First-Served (FCFS) Scheduling

Based on their order of arrival. Very commonly used.

Can result in **convoy effect** : where short process are stuck behind long process. Greatly increasing average wait time.

> Convoy effect is the major problem with FCFS scheduling because we can't control the order at which processes arrive in the ready queue.

### Shortest-Job-First(SJF) Scheduling

Depends on the amount of CPU burst time. The shortest CPU burst lengths will get scheduled first.

Is optimal as in produces the minimum average waiting time for a given set of processes.

To determine length of the next burst, check lecture slides slide 14-16 for formula.

#### Preemptive SJF

If the next CPU burst that arrives in the queue is faster than what is left of the currently executing process, then it means that the next CPU burst will be shorter than all processes is currently in ready queue. Due to the fact that the executing process must be the process that has the smallest CPU burst, and it has run for a while which means the time must be smaller than others. And since the new one is smaller than the smallest one in the queue, it can be assumed that the new one must have the smallest burst time.

> Preemptive SJF is called shortest-remaining-time first or **SRTF** scheduling.

### Priority scheduling

Priorities are associated with each process. (The smaller the number the higher its priority)

The longer you wait the higher your priority is. (Aging) This exists to solve the problem of starvation which is low priority processes may never execute.

#### Round Robin Scheduling

Each process gets a small unit of CPU time (time quantum q). After this time is elapsed, the process is preempted and added to the end of the ready queue as a circular queue.

> Rule of thumb 80% of CPU bursts should be shorter than the time quantum q. This is due to the distribution of the burst times of processes. (Most processes have short burst times)

### Multilevel Queue

Have multiple queues and each queue may have its own scheduling algorithm.

A process must join a certain queue, cannot move around and switch queues

Worry about two things:

- How many queues are there
- How much computational resources they get.
- What scheduling algorithm are they going to use.

#### Multilevel Feedback Queue

Unlike multilevel queues, here processes can move around between queues. This means that **aging** can be implemented in the case of priority based queues. (If a low priority queue can't execute because resources are being used for high priority queues)

In this queue, basically if a process is not finished running in the earlier queues, it will be passed on to the next queue. All jobs will first enter the first queue before being passed to the next queue. And if there are no processes running in the first queue, then the next queue will be executed if it isn't empty.

The later queues cannot be interrupted by any processes from earlier queues(the earlier queues must be empty). **With the exception of Q0**, the first queue can still interrupt.

> Each process gets to run at least once.

Basically this method of scheduling favors the shortest processes, however it wants to also give all processes a fair chance to run (Round Robin).

## Thread Scheduling

Kernel thread scheduling is basically job scheduling that was just talked about previously. It is basically scheduling jobs.

> Do not confuse that kernel thread is only running kernel code. The kernel thread can run both kernel code and user level code.

We need to worry about user level thread. Because these threads aren't run by the OS. It needs to be mapped to a kernel thread. To make it seem like it is running on the OS (to do the mapping) we create a special data structure called the **lightweight** process.

If it is one-to-one mapping there is nothing to worry about, because all user level threads are given one kernel thread. What we need to worry about are many-to-one and many-to-many mappings.

## Multiple-Processor Scheduling

- Asymmetric Multiprocessing : master-slave style
- Symmetric Multiprocessing : Each processor is self-scheduling, the ready queue is shared by all processors or each has its own private queue of ready processes.

Processor affinity : process has affinity for a processor in which it is currently running. Due to cache validation and population. If a process has run on one processor, then the cache would be filled with the stuff from that process. Thus if the process would move around it would be costly to get the needed data again to the cache. Thus the processor might prefer that the process be run in the same process. Two types of this:

- Soft affinity : no guarantees, the OS attempt to keep a process in the same processor
- Hard affinity : forced, the process specifies which processors on which it may run

### Load Balancing

Attempts to keep workload evenly distributed.

- Push migration: a task periodically checks the load on each processor. If imbalanced push task from overloaded CPU to idle or less-busy CPUs.
- Pull migration: idle processors pulls waiting task from a busy processor.

Need not be mutually exclusive. Both methods can exist at the same time.

Load balancing often counteracts the benefits of processor affinity. Because it forces the process to move out of its cached processor.

### Multicore processors

Allows interleaving processes during memory stall time. Because a process often spends a lot of time waiting for memory access. Therefore, the scheduling can take advantage of this memory stall event to run computation on another process.

This kind of switching causes multithreaded cores, which basically means multiple logical processors. Ex: dual-threaded, dual-core system represents four logical processors.

## Little's formula

> **n = lambda * W**

Where:

- n = average queue length
- W = average waiting time in queue
- lambda = average arrival rate into queue

## Simulations

Needs input that signify the future input that you design the system to accept (that is typical of the inputs that you will give).
