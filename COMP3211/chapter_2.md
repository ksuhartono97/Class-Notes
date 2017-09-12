# Informed Search

## Search Heuristics
A heuristic is a function that estimates how close a state is to goal.

### Greedy Search (Best-first search)
Expanding the node that seems closest to the goal, based solely on the heuristics function. However this search can take you to the wrong goal (due to the heuristics function being wrong).

The greedy search doesn't always take you through the lowest cost path.

### A* search
Idea is to combine UCS and Greedy Search. By adding together the heuristics and cost value together and expanding according to this. However, this causes it to be dependent on the heuristics function design.

So problems of A* are when should you stop and how should you design the heuristics function.

We should stop when we **dequeue** a goal node, not when we enqueue a goal.

In the whether A* is optimal or not, the heuristics is wrong. Therefore, it causes the distance to be incorrect. Causing a wrong representation and making the algorithm expand a node that has a larger cost. Due to overestimating the value for heuristics of one node.

So, the idea is that we have to make estimates smaller than the real cost.

g(n) is the cost, h(n) is the heuristics value to n and h*(n) is the actual value of n.
