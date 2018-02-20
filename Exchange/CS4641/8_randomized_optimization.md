# Randomized Optimization

Review:
- Variable length encoding
- Entropy: tells us consistency, not right or wrong. It tells us **nothing** about performance.
- Confidence interval: how sure are we, within what range is our training error within the true error.
- Sample vs true error: sample error, error according to stuff we know. True error, error representing the underlying distributions error.
- Bias and variance.

# Unsupervised Learning
Given any x and a heuristic, approximate the y.

## Randomized Optimization Approaches
- Hill Climbing / Greedy Search
- Simulated Annealing
- Genetic Algorithms
- MIMIC

### Hill Climbing
Is basically greedy search. The process would require finding and comparison of a node with its neighbours. We will need a separate algorithm to find the neighbours.

Hill Climbing Exercise:
1. A
2. A
3. C
4. D
5. D/E, either one, unless there's a special neighbour determination function.

Issues:
-  Choice of neighbour function: where you go is very dependent on the neighbour function.

Neighbour Function Exercise:
- Neighbour function 1:
  - 010101: **100101** or 011001 or 010110, 101010
  - 000100: 001000 or 000100
  - 110000: 101000 , can't flip anything else after.
- Neighbour Function 2:
  - 010101: same way as above any way is fine it works, gets to global maxima
  - 000100: can reach global maxima
  - 110000: Multiple different local maximas, cannot reach global

#### Finding the global maximum
Doing random restarts. It doesn't work really well in some spaces.

Bad solutions:
- Exhaustive search: infinite problem
- Random walk: random moves until we stop seeing anything but better, but at worst case it reaches Exhaustive search level of runtime.

### Simulated Annealing
Hybrid between random walk and hill-climbing. The key is on the schedule to decrease the temperature.

Simulated annealing will always do better, but it's not used in industry mostly.

### Genetic Algorithms
Is often called the second best approach, usually works well.

### MIMIC
Intuitively we reduce the space size.

Mimic slower in most cases, except when heuristic 

## Dependency Tree
Dependency Tree:
- a2a1, a1a3, a3a4: gives us maximum!
Root: a1, why is it root, doesn't matter, any node can work for the root.
