# Process Scheduling
I/O bound processes do not need much CPU time, most of the time spent is on waiting for IO to complete.

After context switch, need to grab the CPU and runqueue as process might resume to different cpu.

A process belongs to a scheduling class.

Process goes to sleep:
- First time you enter, call schedule to schedule another process, then wait until condition is fulfilled.

## Completely Fair Scheduler
Provide fairness rather than running in timeslices.

Fairness and efficiency achieved by giving equal opportunity. That is when given the opportunity, they can use the resources. But if they do not, that opportunity is lost (not saved for next case).

> Red black tree: balanced trees that has constant insertion and deletion time.

Time slices:
- As small as possible for interactiveness, as large as possible for efficiency.

Linux (CFS) defines target scheduling latency of 20 ms. Target time that we are going to be unfair is 20 ms. This is also done to control the interactivity of the application. That is at worst case, you will need to wait 20 ms until you are scheduled again. Also minimum scheduling granularity of 4 ms, that is can't be scheduled for too small of a timeslice to ensure efficiency.

> At any given time (with <5 processes waiting to run), the system latency will be 20ms. But with more load, latency scales.

Virtual clocks:
- Integer variable that tracks historical runtimes in the CPU. In the ideal system, in one second of CPU time, a process will gain 1/5 (0.2s) of CPU time. (not achievable in reality).
- Speed of the clock changes based on the number of processes. Inversely proportional to the number of processes that are waiting to be scheduled. (larger total weight, slower clock).
- Virtual clock tick is 1 / sum of weights
- If virtual clock of a process is faster than the virtual clock of the system, it gets punished and gets kicked out of the system. The system is then given to another process that hasn't gotten access to the system (virtual clock slower than system).
- If the virtual clock is still slower than system after a tick, the process can remain in the CPU for another slice to save context switching costs.

> Basically only kick out when a process has grabbed more than it should (process virtual clock faster than system virtual clock)
