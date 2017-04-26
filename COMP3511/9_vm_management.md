# Virtual-Memory Management

## Virtual Memory

Separation of user logical memory from physical memory.

- Less I/O to load or swap, because it is partially loaded already.

Space wise, logical address can be really big, however no program actually uses the full amount. Note that, virtual memory cannot be larger than the disk size.

Methods of implementation:

- Demand Paging (will be discussed)
- Demand Segmentation

### Demand Paging

Bring pages into memory only when you are using the data. If it is currently not needed, then leave it inside the memory. Eliminates the need to bring the entire process into memory at load time.

> Pages are stored information or data

#### Valid Invalid Bits

Actually signify the existence of the page table entry in the memory. Doesn't relate to the validity of the page!!

#### Page Fault

During access to an address that is inside the page (not the whole page, just that single address). And get a trap. This is a page fault.

Handle it by bringing the missing page back into the memory, and then reset the page table and instruction.

### Thrashing

A process is busy with swapping pages in and out.

The long term scheduler might bring in more processes. But if system is in thrashing status, it will bring down CPU utilization very quickly to a low number.

#### Why does demand paging work

Locality model: only working on a small number of documents.

Thrashing can still occur if the size of the locality is larger than the total memory size.

Therefore, we need to estimate the size of the locality.

##### Working-set model

You have a working-set window that moves along the program, this window encompasses a certain number of instructions that form a principle of locality in the program.

Size of the window is a fixed number.

Working-set itself is a variable that changes over time.

However, this has too much overhead, because every memory access/instruction access, we need to update the moving window. Thus we have to approximate, instead of all the instructions in the working-set, only interrupt in a smaller frequency.

##### Page-fault frequency

Establish an acceptable page fault frequency.

##### Prepaging

Prepage all or some of the pages a process will need.

However, there is a risk associated with this, if we don't use the pages then the prepaged pages are useless, wasting I/O and memory.
