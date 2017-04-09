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
