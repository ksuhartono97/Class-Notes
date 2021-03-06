# Markov Decision Process

Are non-deterministic search problems.

In a Markov Decision Process, `A` indicates Action and `S` indicates state. And the assumption is that the future and the past is independent from the present state. As in what happened in the past doesn't affect what presently happens. With MDP, we can compute all the expected values of all the states.

With expectimax you're doing too much work, you have to expand so many trees, and if there are duplicated nodes, the tree can be infinite. Hence the idea behind MDP.

## Discounting

The concept can be used to make the agent prefer to get the reward as soon as possible as it maximizes the utility.

Delayed reward can increase the search depth of the problem, and also might replace the solution as the discount value will be very different.

## Solving MDPs

The fundamental operation is to compute the (expectimax) value of a state.

## Value Iteration

Start with zero values, then use an updating formulation where the value of s on an iteration (k+1) is based on the value of all state values at iteration (k).

Example, the racing search tree (the one where with expectimax we are doing too much work). Especially since it has repeated states that go on forever, causing each search tree to need to be expanded extremely deeply.

We should use a **time-limited** value.

##
