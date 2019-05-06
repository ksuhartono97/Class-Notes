# Kernel Synchronization Mechanisms

User space concurrency can be solved with semaphores because all these issues are due to the scheduler. But in the kernel space, there are more issues that can cause race condition as compared to for user space processes. There is no specific rule on deciding what to protect and when to protect. In general there is a rule of thumb to ask questions whether I need to lock the data or not.

## Atomic Operations
Atomic operations: CPU gives means to implement this. Not actually implementing it.
- On integers: set and test integers. Operate on type called `atomic_t`.
- On bits: set and test bits

Atomic bit level operations defined in `include/asm-generic/bitops`. Each architecture (ARM, x86, etc) has their own definition of these operations.

In kernel version 5, the return values of atomic bitwise operations is `bool`, before that it is `void` but it isn't an issue as it can be casted to any type.

## Spinlocks
Spinlocks are unsafe in interrupt handlers, but fast. It is unsafe as it can call a function that causes it to go to sleep and cause it to be unable to wakeup from there. So better to disable the local interrupts beforehand. If you are sure code is not going to sleep then can simply use spinlock lock and unlock.

Spinlocks aren't recursive, can only grab lock once.

Has IRQ interfaces to make operations safer by masking interrupts (disabling them so cannot enter interrupt context).

## Reader Writer
Some parts of the code only need to read, other parts need to read and modify (write). When a code is being locked by a writer lock, only one single piece of code should be accessing that  critical section. No other readers can access. But if we aren't modifying, then can have as many readers as possible.

Unfair to writers(prefers readers) when there are too many readers.

## Semaphore
Sleeping lock, better for codes that execute for a long time. In interrupt context not suitable simply because it is going to sleep by design. Not suitable for critical sections with spinlocks, spinlocks aren't supposed to sleep (semaphore will take it to sleep), causes spinlock to be unretrieveable. 
