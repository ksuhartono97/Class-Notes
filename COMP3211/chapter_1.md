# Uninformed Search

Agents that plan are able to plan and do something automatically.

Reflex agents, an agent acts based on the current state, doesn't consider future consequences. May or may not be optimal, from its behaviour. Likely to be unable to deal with complex situations.

Planning agents ask 'what-if', makes decisions from hypotheses, acts according to possible consequences from a certain action.

## Search Problem

Consists of:

- State space : every state corresponds to a state of where the agent is in the world
- A successor function (with actions, costs)
- A start state and a goal test (to check whether goal state has been reached or not)

## State Space Graphs and Search Trees

Both are usually unable to be reconstructed in memory due to the size of the tree.

## General Tree Search

Maintain a fringe of partial plans under consideration and expand as few as possible.

### Depth First Search

Strategy : expand a deepest node first. Make it LIFO stack. Basically explore as deep as you can before going back and exploring another node.

May not be able to find the best solution.It will only find the leftmost solution.

### Breadth First Search

Expanding the shallowest node, and instead of a stack uses a FIFO queue. Put in the nodes at every level to the queue, expand the nodes and push their children on top of the nodes. Repeat until finish.

Not necessarily expanding the whole tree at the beginning. Only expand as necessary.

### Iterative Deepening

Combination of DFS and BFS, by implementing a depth limit per search.

### Uniform Cost Search

Make a priority queue, and expand the nodes with the lowest cost first.
