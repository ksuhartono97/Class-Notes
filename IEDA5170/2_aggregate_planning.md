# Aggregate Planning
Helps create a long term production plan that influences management decisions. The input to this system is the demand management (demand forecasting) and the output is the master production scheme (MPS). Is done only for the higher level planning. For detailed planning it can only be done on the short term. 

The assumptions exists as this is a very simple model. The model itself is doing planning on aggregate products which technically doesn't exist (demand is being forecasted on an aggregate product, something that doesn't make sense). This is because the planning is only done to help give some guidance to make some early decisions for resource allocation.

## Product Mix Planning Model
Considers multiple products.

- index of products: needed because there exists multiple products
- index of workstations: a product is manufactured in a workstation (machine) there can be many manufacturers
- index of time period: for planning further seasons.
- product demand range: to show what happens to the production with maximum demand and minimum demand.
- consumption time of workstation to produce one unit of product
- capacity of workstation: needs to optimize on this as this is the limit
- net profit: what we want to maximize
- holding cost: cost to hold a unit of period for one period, can be time dependent.

### Extensions to the basic model
Extra constraints:
- Workstation utilization: workstation cannot be performing at 100% capacity
- Backorders: assume that unsatisfied demand can be satisfied later, not lost (there is an associated penalty cost)
- Overtime: staff will work overtime, but becomes an overtime cost
- Yield loss: between different workstations, in a chain where output of one machine is fed to the next, there can be quality defects. Accounted for here.

Backorders: cannot have on hand inventory and back orders (by definition). Normally backorder cost is larger than backorder cost. Holding cost can be calculated. Backorder cost is usually intangible and hard to calculate. As such the penalty cost for backorder is usually much higher than inventory holding cost. 

## Workforce Planning
When regular workforce cannot meet the requirements:
- Overtime allocation: use currently available workers. If not enough then we go to second problem
- Workforce resizing problem: hire or fire. 

We use the cost information to do aggregation for workforce problems.

In aggregation, weighting is calculated based on the demand. 

## Finite Horizon Case
Cannot just use the infinite horizon case for the finite horizon situation. Because if the end of the horizon is before a time horizon T, the inventory will not drop to 0.

Possible solution #1: We make sure to order a smaller inventory for the last time horizon before the end of the horizon. As such we can guarantee that the last inventory will end at 0. However, this also isn't optimal because we can make the previous period to order more to minimize the ordering cost.

Thus, the underlying assumption is that we **do not know** whether we should order the **same amount** of inventory for every time horizon. 

Then solution is to change the length of a T cycle, that is change the duration of an interval. As such, the original assumption of the same amount to order every time cycle for the basic EOQ model works in this case.

> TODO: ADD IMAGE RESOURCE
