# Instance Based Learning

Review from last Thursday:

- Smaller/Larger hypothesis space: smaller is better as it's easier to train and manage
- Restriction bias: representation of dataset, preference bias: algorithm preference

## Learning Methods

- KNN (k-nearest-neighbours) :

  - Solution to the travel example in the lecture notes

    - Walk
    - Drive
    - Metro/Drive can be either one, depending on weighting.

  - Use when there is a lot of training data with few attributes, if there are many attributes, the test time(prediction time) becomes really long.

    - Pros:

      - Cheap training
      - Learn complex target functions, each training data becomes a function, such that each input maps to an output
      - No information loss, may be able to predict 100% correct

    - Cons:

      - Slow query time : definitely slower than neural net and decision trees. Need to test the distance to **every single** point every time we try to make a prediction.

        - Voronoi diagram: split to partitions, check adjacent neighbours.

      - Curse of dimensionality: the more features, the worse the algorithm perform

        - Decision Trees: focus on few features that matter, so not as affected

- Case-based Reasoning:

  - The idea is to learn while testing
  - Adaption methods:

    - Null adaption: basically KNN
    - Transformational adaption: map features on cases based on similarity, transform to a domain specific equivalent
    - Generative adaptation: have a secondary knowledge base

  - Exercise 2:

    - Representation:

      - Number of legs
      - Mouth type
      - Tail type

    - Retrieve training cases:

      - Big beak: duck
      - Big tail: beaver
      - 4 limbs: dog, beaver, cat

    - Adapt:

      - Duck like beak
      - Beaver tail
      - 4 limbs: beaver

    - A way to approach the representation, the way to do it is by finding the smaller number of variables that allows representing all the data as distinct

  - Not used too much because of the high amount of hand-authoring required that is very domain specific.

- Locally weighted regression: doesn't perform that much better compared to KNNs or Neural nets
- Radial basis functions: neural network version of locally weighted regression.
- Lazy learning

Comparison:

|           |Neural Nets|Decision Trees|KNN|CBR|
|-----------|-----------|-----------|-----------|-----------|
|Neural Nets| \\\\\\\ |Regression |Generalize |Too many features |
|Decision Trees|Low Training Time| \\\\\\\ |Lots of attributes | Fewer resources/lower computation time (testing) |
|KNN|No information loss|Complex function | \\\\\\\ | Smaller hypothesis space |
|CBR|Symbolic representations| Active Learning| Adaption | \\\\\\\ |
