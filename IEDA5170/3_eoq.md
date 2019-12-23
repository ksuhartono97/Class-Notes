# EOQ 

Critical assumptions: if these are violated, then the model can no longer be applied.

## EOQ Basic Model
1. Single product: most inventory models are on single products
2. Production is instantaneous: implies that production rate is infinite. 
3. No delivery leadtime: product is obtained right after product is ordered
4. Demand is deterministic
5. Demand rate is constant over time
6. A production run incurs a fixed setup cost, regardless of production quantity
7. No backorders are allowed.

Critical assumptions on this model: **4, 5, 6**. Other assumptions can be relaxed.

> Inventory graph on slide 4:
> - Vertical lines on inventory shoots up because production is instant
> - Inventory goes down linearly because the demand is constant

Model average inventory: Q/2

### Power-of-2 Policy
Deciding order intervals should be based on powers of 2. 

The error of the policy can be bounded due to the choice of interval. The largest possible gap that can be introduced is sqrt(2).

### Economic production IoT
New assumption, production now takes time. As such, production rate must always be greater than consumption rate. Inventory can only build up if the production rate is equal or greater than consumption rate.

Maximum inventory level: Q (1 - D/P)

Total cycle length T = Q / D

### Backorder
Add in a new parameter, backorder cost (per unit/time). Because demand is deterministic, backorders can be completely avoided if we really want to. But if backorder's aren't too big we can introduce the backorder. The benefit is that we can reduce the setup cost. 

