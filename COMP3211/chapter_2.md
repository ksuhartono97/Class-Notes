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

## 8 Puzzle
The states: 9!/2 as there are 9 possible slots but divide by 2 as the possible positions are only half of all possible locations.

### Heuristics for 8 Puzzle
The numbers of tiles misplaced from its goal position.

### Manhattan Distance Heuristics
Is admissible because assumes that the tiles can move without the blank space restriction. Meaning that definitely it is much less than the actual cost.

> Most of the time, if the problem is relaxed, the heuristics is admissible, however NOT ALL THE TIME.

But usually it's too hard to estimate cost based heuristics as you would have to expand a lot of nodes.

> Generally, the closer the heuristics get to the cost, the more work needs to be done to expand a node.

## Graph Search
Never expand a state twice. The example on slide 35, we shouldn't expand those nodes as it is the same as some other node in the tree. As we wouldn't want to expand it twice so we must not expand those.

The graph search example is blocked by the A node, simply because the heuristics we gave to the node is too large. Causing the graph search to be inaccurate.

With a consistent heuristic function the above issue can be alleviated. The characteristic is that the f value (heuristic + cost value) is never decreasing
