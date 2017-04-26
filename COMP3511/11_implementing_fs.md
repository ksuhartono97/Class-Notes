# Implementing File Systems

Metadata is everything about the file-system structure except the actual content of the file.

File control blocks, has a pointer that can help locate the contents of a file in the disk.

## In memory File System Structures

File hasn't been opened, then the system wide and per process file tables do not have this file. The file is still in the disk.

On file open, create a pointer in the system wide open-file table that points to the data blocks of the file that is opened, then in the per-process open-file table, create a pointer to the system-wide open-file table. Putting it in the system-wide open file table, basically gives it the functionality of a cache, allowing other files that want to find the file to be able to find it quicker.

After use, delete the entry from both open-file tables. But if there is someone else using the file, the don't delete it in the system-wide open-file table.

### Contiguous Allocation

Each file occupies a set of contiguous blocks in the file system.

Benefits:

- Allows sequential and direct access easily
- Simple, only need to remember the starting block, and size of files. A small amount of things to remembers. This can be a great advantage because the number of blocks that belongs to a file can be huge. Meaning that if you have to keep track of all the blocks, then there is a tremendous overhead.

Problems:

- Hard for file to grow or finding space for new file.
- Typically needs to know file size on creation, also overestimation would lead to internal fragmentation (assigned but unused).
- Also there are external fragmentation.

> Internal fragmentation means that there are space assigned but unused. External fragmentation is the space between files that cannot fit any other files, rendering the space unusable.

#### Extent-based File Systems

A file consists of multiple **extents** and these extents are contiguous blocks of disks.

There is still internal and external fragmentation but it is less severe. This is similar to moving from contiguous allocation to segmentation.

### Linked allocation

Need the first block and the least block of the file. Each block has the data and a pointer to the next block, except the last block that has a `null` pointer that signifies the end-of-file. These blocks can be scattered **anywhere** in the disk.

Problems:

- Terrible performance when doing random access or direct access of a file
- There is overhead for the pointers.

#### FAT (File Allocation Table)

Instead of having to open a block to check the pointer (because the block has the pointer that points to the next one), make a table that contains all the block numbers. (The block pointers)

The FAT can be cached, meaning that we can access any block without having to go through each of the blocks in the disk.

The FAT method allows speeding up random(direct) access speeds greatly as we no longer have to enter and follow the pointer path in the blocks in the disk. Finding the block can be done in memory instead of disk.

### Indexed allocation

The file will tell you the location of the index block, and the index block is the one that stores all the locations of the blocks of data of the files.

Problems:

- There is overhead, because we always waste a block to index the contents of the file. Especially if the filesize is too small, it means we are wasting the extra block at a great percentage. The wastage percentage is even greater than normal linked allocation.
- The file is too large such that the index block cannot support it, too many blocks to store here.

> Disk size : size of block _size of pointer, example: block size : 4 KB and size of pointer 4 bytes, thus it means that size of disk is 2^12_ 2^32 = 2^44 = 16 TB

> File size : # of pointers that the file has * block size

However naturally, in the OS we always have varying file sizes, and we can't just use one scheme to support all of them. For example if we use three-level scheme to support the files, that would mean an extreme amount of wasted space for smaller files.

Thus we can go for a combination, giving different schemes for different file sizes.

What is the maximum file sizes that can be supported? Just calculate the largest file size that can be supported by the highest level, because the difference is huge.

### Free Space Management

Using **bit map** that enumerates all the blocks that exist and associate it with a state to show whether this block is occupied or free.

Problem with bitmap approach is that there is a huge overhead because of the great number of blocks that exists.

Solutions:

- Grouping
- Counting
