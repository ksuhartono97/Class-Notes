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

Which queue the thread is on basically determines which state the thread is in.

## User and Kernel threads

User level thread basically says that if the program is separated into several pieces (basically has concurrency support) then you can schedule it such that it can run concurrently. Manages on the user-level/user program level

Separate from kernel threads that manages OS threads.

## Multithreading Models

### Many-to-one

Many user level threads are mapped to a single kernel thread. Basically there is no concurrency because you are mapping everything to one kernel thread only.

Threads with this model may not run in parallel because only one thread may be in kernel at a time. Whereas parallel threads require multiple threads to be able to run in the kernel

### One-to-one

**Each** user level thread maps to a kernel thread. Has more concurrency than many-to-one. But if there are a lot of processes are running, and there are many users, the number of kernel threads may be a huge number due to the user's requirements (depends to how many programs ran by all users, and the number of threads per program). Most commercial systems can't handle such a large number of kernel threads.

### Many-to-many model

Allows many user level threads to be mapped to many kernel threads.

The number of kernel threads will not increase a lot based on the number of user threads. Because the mapping is flexible and it is adjustable according to available resources. However, you will still have a form of concurrency.

### Two level model

Similar to many to many, however allows binding of user threads to a kernel thread. More restrictive than many-to-many model. Less flexible, as in if there is a free kernel thread but it is bounded to another user thread, then the current user thread can't use that kernel thread even though it is free.

## Threading Issues

### Semantics of `fork()` and `exec()`

If `exec()` is called right after `fork()` then there is no need to copy out all the threads of the parents. Because it is going to be replaced by the new process. In theory this is done automatically.

### Signal in UNIX

Used to notify a process that a particular event that has occurred.

Synchronous signal: generated by the process itself due to events happening inside the error.

Asynchronous signal: generated by events external to the running process.

#### Signal Handling

2 possible handlers:

- Default
- User-defined

Where a signal should be delivered depends on your needs.

The method for delivering the signal would also depends on the type of a signal (depends on your needs).

### Thread Cancellation

Termination of a thread before it has completed. Example: multithreaded search program, if one thread has found, all other threads should be cancelled.

Target thread: thread to be cancelled

Asynchronous cancellation: Terminates the target thread immediately. This can be dangerous as if you terminate say a kernel/os thread that is in the process of updating a shared data structure, it could cause synchronization issues because the content is not the same.

Deferred cancellation: check periodically if target thread should be cancelled.

### Thread Local Storage

Allows each thread to have its own copy of data. A place to keep data and data structures unique to this particular thread.
