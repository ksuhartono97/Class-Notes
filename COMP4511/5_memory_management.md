# Memory Management

Physical addresses: 32 bit can use 64 bit. This is done by sending double signals (communicate twice) on the memory bus.

SLAB allocator:
- Fractional allocation: allocates objects that are smaller than the size of a page. Preallocates these objects from pages.

`alloc_pages` allocates contiguous physical pages.

Zeroed pages: pages where the data is cleared off. Blank empty pages, useful for giving pages to user space processes (to clear off sensitive data).

## Buddy System
Take what is needed, if blocks of a certain size is not available, take from the next order. Take as needed and assign the rest to the lower order. 
