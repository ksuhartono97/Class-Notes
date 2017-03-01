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
