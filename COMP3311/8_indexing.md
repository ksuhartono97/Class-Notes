# Database Indexing

## Indexing Concepts

Arrange records and minimize the effort of finding records. (Minimize the number of pages you need to open before finding the record as in attempt to find the record on first try).

Methods of arranging:

- Random Order: worst case, have to search 10^6 records before finding the record
- Sorted : Sort database with binary search. Much less pages that needs to be seen before finding.
- DBMS: have disk pages and pull it into main memory

Making it even faster:

Build an additional **index** on the sorted data. Each record can have a unique index entry associated with it. Since these entries are smaller, we can fit in more data in a page.

But we don't need all the records to have an index. As the data is sorted in order, you only have to index the first data in the page. Only need to use the first element to know whether the record is in the page or not, if not then can move to the next page.

> Only need to index **one record per page**

Doing this can save a lot of index space.

### How do we use index to speedup searches?

Because we know that the index is also sorted, we can use binary search to find the target record that is most similar to the target record. The cost is lower than just searching sorted pages. After finding the index **note that you still need to follow the pointer to the record**.

### How to speedup even more?

Indexing the index. Will increase speed even more because we have to check a smaller number of pages.

If you are still not satisfied, you can create another index level to make it even faster.

> This category of indexing is called **ordered indexing** is better than hashed indexing because this supports ranged value searches better. Whereas hashed indexing supports specific value searches better.

## Ordered Indices

Index is ordered / also called **tree**-indexed. Good for equality and range search.

Cost of searching here is height of the tree + 1 (for a single record only)

Terminologies:

- Index node: index page
- Fanout: number of children pointers of a node

### Primary Index

The data file is sorted on search key of the index

### Secondary Index

The data file is not sorted on search key of the index. Sorted on something else.

### Sparse Index

Contains index records for some search-key value only. Example of the one in the HKID example.

Sparser indexes implies less maintenance overhead for insertions and deletions.

### Dense Index

Each search key value has an index that has an entry.

## Hash Indices

Organizes search keys with their associated record pointers.

# Index Structures

## B+ tree

> Review: each index has a pointer and a data value. The pointer points to the data page.

Satisfies these requirements:

- A balanced tree
- Each node has between n/2 and n pointers
- Each leaf node has between (n-1)/2 and n-1 data values (1 less then number of pointers)
- Number of pointers : Fanout
- (n-1)/2 is the order

In the leaf node, the reason why there is always 1 more pointer than data value is because that 1 pointer points to the next leaf node in search key order (right sibling node)

We should have dense index in the leaf node.

In the non-leaf nodes, we do not need to have dense index.

### Queries on B+ trees

Search through the nodes, 3 cases:

- Key found, then follow pointer +1 from the found key
- k < Km-1, follow the pointer where the key is the smallest search-key value that is > k
- If k >= Km-1 go to the child node of Pm

Repeat until leaf node, if till leaf node key still not found then k doesn't exist.

#### Insertion into B+ trees

Check lecture note for algorithm.

Special case:

- If we keep inserting entries such that root node is full, then we still insert another node, we have to split the root and recreate a new root node.
