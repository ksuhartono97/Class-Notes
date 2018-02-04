# Supervised Learning

Big idea: function approximation, mapping from input to output.

Some terms:

- Hypothesis Space: Conceptual framework for thinking about supervised ML models.
- Restriction and Preference Bias : a restriction brought by the representation (representation bias), while preference bias prefers certain hypothesis to others.
- Validation test: the test set, to check if the supervised learning overfits to the training set

## Decision Trees

Answer to a decision tree by making iterative decisions as you progress through the tree.

Choose an attribute where you can slice the information the most. Need to figure out how to slice it before making the decision tree.

Idea of algorithm:

- Head node has all the data
- Figure out which attribute will give the most information gain when split on by using **entropy** which is a way of measuring agreement in the data.
- If it's good enough can be split into a leaf node
- Otherwise push it down as another decision node

### Biases of the decision tree

- Prefers "good" splits at the top: So there are big decisions at the top and more specific ones as it goes lower.
- Shorter trees
- Heavy bias to training set: brings overfitting. Given enough time, a decision tree can become infinite.

### Issues for decision tree

- Overfitting:
- Continuous output:

Solutions:

- Pruning: remove nodes that are too specific, so we remove nodes that can be removed without hurting test accuracy too much
- Decision Stumps: many trees with a single node, as largest predictions are usually made at the top, then use many trees that are trained on the data, and then these trees vote on the result. (A similar idea is random forest algorithm)

Decision trees want the input to be a 2d array. `np.reshape(x, (-1, 1))`

> Generally, we don't use decision trees anymore.

We can use it when:

- There are missing data
- Preference to discrete rather than continuous
- Relatively fast training time

## Artificial Neural Nets

Based on the concept of neurons

### Perceptrons

Weighted inputs that are fed to an activation function and you get an output.

The general idea of the training is you check how much error is there on the result, and then this error is backpropagated to update.

### Biases

- Restriction Bias: can't put in "raw" data
- Preference Bias: training set bias

Relationship to Deep Neural Networks: they just have more layers.
