# Query Processing

## Query Optimization
Amongst all equivalent evaluation plans choose the one with the (**expected**) lowest cost.

Cost measure: number of page transfers from disk.

### Selection
Available algorithms that are used:
- Linear search: Scan each file page and test all records **one by one**
- Binary search: Applicable if the selection is an equality comparison on the attribute on which file is **ordered**.
- Index Scans: Uses an index
  - Primary tree index on candidate key : When we have the primary key, we need to do 1 more page access to retrieve the found object.
  - Primary tree index on non key: Not enough to just search the primary tree index. After finding the index that contains the records, have to find all pages that contain the retrieved records. Because this is a non-key.
  - Equality on search key of a secondary index:
    - On single record if the search key is a candidate key: same as primary tree
    - On multiple records if search key is not a candidate key: Can be very expensive if the records are on different pages, the amount of page transfers may be larger than linear search.

### Join Processing
