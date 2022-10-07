# Single Warehouse and Multi-Retailer Model
The problem is how can the warehouse decide it's inventory replenish policy. To solve this problem, it isn't easy to directly solve it by formulating a single optimization problem.

Two standard policies to solve this problem:
- Nested policy: when warehouse places an order, each retailer also orders. Certain retailers could have run out of inventory before the warehouse orders. Due to the differences in time period and demand rate, there is likely to be a retailer that either have not finished the inventory or have run out of inventory for a while.
- Stationary policy: Reorder intervals are constant for each facility, and the intervals are powers of two multiple of a base planning period. We must determine a base planning period, then we can multiply that base by powers of 2.

System Inventory: to decompose the system. basically to know which inventory belongs to which retailer. Because when we delegate the inventory in warehouse to certain retailers, we can break down the problem. The system inventory for each inventory is called the **echelon** inventory. Which is basically `inventory at retailer i + retailer i's inventory at warehouse`

> TODO: INSERT RETAILER DIAGRAM

We need to determine the average cost of echelon holding inventory. 

Legend:
```
T<sub>0</sub>: time interval for retailer to order
T<sub>i</sub>: time interval for retailer i to order
```

Cases: 
1. T<sub>i</sub> >= T<sub>0</sub>: Every time the retailer orders, then the warehouse have already ordered before. Thus the warehouse will not be holding inventory for the retailer i.

> TODO: INSERT PHOTO

2. T<sub>i</sub> < T<sub>0</sub>: In this case, the warehouse will actually be holding inventory for the retailer. 


