# Multithreaded Programming

Parallelism can only happen in a multicore system, running multiple processes in different processors simultaneously.

Concurrency implies that you have a lot of processes running over a period of time on one processor.

Types of parallelism:

- Data : distribute the data to the multicore
- Task : distribute threads of the task to the multicore

## Amdahl's Law

Illustrates how much of a speedup that can be achieved if the system is switched to a multicore system.

## Thread State

A multithreaded process would still have a PCB that would have a pointer that points to the number of threads that it has.

Each thread has a thread control block (TCB) which is a unique data structure that is associated with every single tutorial.

In a multithreaded process system, the active part of the process are the threads, as in the part that switches states are the threads. Which signifies a difference between a thread and process. There is **no state** defined for a process if it is multithreaded.

In comparison, in a single threaded process, the process has only one thread which means in this case process and thread is the same thing. And it also means that the process itself is the active part that switches states in the lifecycle.
