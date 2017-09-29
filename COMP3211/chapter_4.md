# Expectimax Search

Basic idea is, it is similar to minimax search, however the min nodes in minimax are replaced with _chance_ nodes.

Example case, opponent use depth 2 minimax, and uses the result 80% of the time, the rest of the time it moves randomly. What search should you use?

- Expectimax Search : because there is randomness, you should use expectimax. And for finding out the probabilities in each chance node, you have to run a simulation of the opponent. However, it will increase complexity very quickly.

## Other Game Types

Expecti-minimax : An extra random agent in the form of the environment. While there are 2 adversarial agents.

### Go

Should be "easy" in category of AI problems.

Monte Carlo Tree Search:

> Argmax : find the argument of a function that can maximize the function.
