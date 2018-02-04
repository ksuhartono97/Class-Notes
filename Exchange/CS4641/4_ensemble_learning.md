# Ensemble Learning: Boosting and SVMs

## Binary Classification

Classification over 2 classes.

The base idea is that we want to divide the space such that there is all the data of one class on one side, and the data of the other class on the other side (split the data cleanly)

### Boosting

> Originally Adaboost (adaptive boosting)

Using importance to boost accuracy, implemented by doing weighing. But static weighing won't help. The idea is to do some dynamic weight adjustment, to adjust the weight to tend more to the parts that the classifier is doing bad on currently.

So we bias the classifier to do better on the things we did bad on last time.

Generally:

- Right: weight goes down (less important)
- Wrong: weight goes up (more important)

The algo uses multiple weak classifiers. And on each step, only evaluate the latest classifier.

Boosting tends to not overfit, as in a way by the nature of boosting, it is not possible to focus too much on irrelevant details as we keep on shifting the focus.

When to use boosting:

- Restriction and preference bias doesn't exist initially, it depends on the chosen weak classifier.

### Bagging vs Boosting

- Large coverage doesn't necessarily mean good coverage as there are many other factors that can affect it.
- Small coverage is too focused on certain things.

Boosting is combining many simple models, we can get good coverage by combining the many

Bagging is using many complex models, all trained on subsets of the training data.

Baggging Example approach:

- Random forest: a forest of decision trees trained on a random subset of the training data.

### SVMs

Lines separating the groups should be as close to the groups as possible as that is going to lead to the smallest possibility of getting something wrong. The distance between the two lines that separate the groups is called the **margin**, and SVMs want to maximize the margins.

> The margin is the biggest possible line between the points

The support vectors are always parallel. In training an SVM, we are trying to find the margin.

The notion is a representation made up of support vectors and a margin.

The margin is a line that is perpendicular and intersects with the points.

Cannot perfectly split the classes, then use the hinge loss function.

What about curving lines? We need to convert them to a different dimension so that the points are linearly separable. This is done by using a distance function to convert the datapoints. This is called the **"kernel trick"**, the kernel must act like a distance function, but can in practice be anything, it's on the author to come up with a domain value.

Generally distance functions are given to you as a default by the library.

The kernel that is chosen will have a huge impact on the data.

SVMs cannot learn any features, and the kinds of functions that it can approximate are functions that are linearly separable.

## Quick review section
Representation: sort of the blueprint

Algorithm: the process to construct a house from blueprint given material

Model: The house

Cross validation: tool to ensure that the training approach is not limited to a single dataset.

The bigger the dataset, the more folds you should have, a smaller dataset should have a smaller fold number.
