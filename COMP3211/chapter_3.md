# Adversarial Search
> Point of the course is to develop an agent that can act rationally (max utility)

The higher utility the better.

## Adversarial Game Trees
Using a reward system, giving a positive value reinforcement if you are able to complete the objective. The closer you are to the objective the larger the value reinforcement. The further you are from the goal, the more negative the reward.

States:
- Ghost : want to minimize PacMan's utility
- PacMan : want to eat all the dots.

Separate the states to two different types,
- under agent's control : enlarges agent's utility
- under opponent's control : enlarges opponent's utility (lower agent utility)

In this case, there is one action taken for every step (as in you assume that only one character can do one action at a time)

This is a case of zero sum games, where one player minimizes the other players utility.

### Minimax Search
2 functions one for the agent, one for the adversary. Take turns in using a utility function based on which agent's turn is it. We compute in a recursive way.

So there are values from the game of certain actions. Every time it is the minimizing agent's turn, it will choose the minimum value from the set of values. And if it is the maximizing agent, it will choose the maximum value from the set of values. Basically meaning that the maximizing agent will get to choose an action that maximizes utility from among worst case scenarios.

Assumption is that the opponent is optimal.

Cooperation can happen even if the agent's are programmed differently only due to the consequence of minimax due to the fact that they are trying to achieve the same goal.

However, the efficiency is really bad, the same as exhaustive DFS. Meaning for most big cases, minimax is completely infeasible.

Depth limited search, to limit the number of nodes it searches. Only search a certain depth every move. The deeper you search usually the better the algorithm is.

#### Evaluation Functions
Typically a weighted linear sum of features.

#### Minimax Pruning
Prune the children if the value of the node is worse than the max node.

##### Alpha Beta Pruning
Order of children matters.
