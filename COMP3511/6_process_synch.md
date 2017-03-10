# Process Synchronization

Race Condition, due to interleaving process that are accessing the shared memory, can cause errors in the final value of the shared memory.

## Critical Section Problem

Critical section is the segment of code during which:

- A process may be changing shared variables

Things that need to be guaranteed in the solution:

- Mutual Exclusion: If a process in executing in its critical section, no other processes can be executing in the critical section. Checking is done in the entry section, if someone entered, can close the entry point to allow others to enter. Until released, no new function can enter. (Even though that function is interrupted)
- Progress: No process is executing in its critical section, and there are processes that want to enter the critical sections, the selection of a process that wants to enter next cannot be postponed indefinitely.
- Bounded Waiting: A bound for the number of times that other processes are allowed to enter their critical sessions after a process has made a request to enter its critical section and before that request is granted.

In the kernel, kernel code is subject to several possible race conditions. Due to file system management (simultaneous updates) and kernel data structures.

### Peterson's Solution

Assume that load and store are **atomic** as in cannot be interrupted.

Processes share some variables:

- `turn` to tell whose turn is it to enter the critical section. Is mutually exclusive.
- `flag` for each process, to tell whether it is ready to enter the critical section or not. `True` implies ready to enter.

### Synchronization hardware

Special instructions from the hardware that can be used to lock critical regions

- `test_and_set()`
- `compare_and_swap()`

Doesn't guarantee progress. Only guarantees mutual exclusion.

#### Bounded-waiting Mutual Exclusion with test_and_set

Keep doing test and set while lock is true, the moment lock is false, set waiting to false and enter critical section. (Guarantees **mutual exclusion**)

After that loop through the list of processes that is in the waiting. If there isn't anyone that is ready to execute (has a true value) then release the lock. Else let that process execute its critical section next.

> Bounded waiting implies progress, but progress doesn't imply bounded waiting.

### Mutex Locks

Previous solutions are too complicated and generally inaccessible.

`acquire()` to get a lock and `release()` to release the lock.

#### Semaphore

Used for synchronization.

Looks like an integer, however we cannot do integer operations on a semaphore. We are only able to do two operations to the semaphore, which is `wait(S)` and `signal(S)`.

### Priority Inversion

Scheduling problem can arise when a lower priority process holds a lock that is needed by a higher-priority process.

A low priority process is holding a high priority process's locks. While holding, a new process with higher priority than L, enters which preempts L. Thus interrupting the whole cycle. Causing H to wait for M and L.

Solution is to let the L inherit H's priority. Such that no new processes that is lower than H but higher than L in priority can preempt L and interrupt it from execution.

## Classical Problems of Synchronization

### Bounded Buffer Problems

Finite amount of buffers, consumer has to wait if the buffer is empty. Producer has to wait if buffer is full.

Buffer is shared, need to guarantee mutual exclusion.

> Note in slides, full means **empty** and empty means **full**

Full is initialized to 0 and empty is initialized to n. This means that there are n empty spaces and full counts the number of items in the buffer.

Wait for empty and signal for full. Why? Because wait will reduce the value of the semaphore by 1\. Since empty counts the number of empty spaces, then certainly we have to reduce by 1 every time there is a loss of space. Also signal for full because it counts the number of items in the buffer, and signal increases value by 1.

### Reader-Writers Problems

Can have multiple readers at a time. However, can only have one writer at a time. If writer is inside, reader cannot enter. Whereas if reader is inside, writer have to wait until reader is all finished.

The problem is when there is a reader inside and there are writers waiting. Since readers have a higher priority, the writers could be denied access continuously if readers keep on coming (starvation).

Logic is, when you a reader enters, increment the read_count by 1\. If the read_count is 1 (the first reader) lock the rw_mutex so that there is no writer that comes in. If the reader leaves, then do -1 on the read_count. If the read_count is 0 (the last reader) it means that it is the last one, so signal the rw_mutex so that it is released.
