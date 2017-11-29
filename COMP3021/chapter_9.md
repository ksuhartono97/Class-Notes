# Multi-Threaded Programming

## Synchronization using Locks

You could have two methods that are running concurrently in threads, so you will need to acquire locks, if not there might be conflicts, causing the data result to be wrong.

> Race condition: Two methods are racing against each other, doing something with the functions, causing the end result to be wrong eventually.

You can choose a fairness option to the lock, when this is true, the lock will always be given to the thread that has been waiting the longest. (If it is false, there might be starvation).

A lock can create `Condition` objects that would prevent threads from executing unless the condition is fulfilled. But condition is only useful if you have **more than one thread**, that are **dependant on each other**.

When a thread sleeps, the lock is released temporarily so other threads can use the lock.
