# Process Address Space

Page tables: available through the pgd pointer in the `mm_struct`. Gives the means to translate virtual address space to physical address space.

Kernel threads: processes that belong in the kernel. Will compete for resources with user processes. But cannot access any data in the virtual memory in the user space.

> `mm_struct` represents memory (virtual address space) of the user. Since the kernel thread doesn't have this, they cannot access this part. As such, kernel thread doesn't have `mm_struct`

Thus how does a kernel thread access the page table? Borrow the `mm_struct` of the last running process (that is the process that is running before this kernel process is started).

`vm_start - vm_end` gives the exact size of the memory area in bytes.
