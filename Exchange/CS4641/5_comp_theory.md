# Baselines
Something to compare with to check whether the performance is good or not.

# Computational Learning Theory

Example 1: need a minimum of 4
- 1100 : true
- 1111 : true
- 1011 : false
- 0111 : false

Example 2:
- 1111
- 0111
- 1011
- 1101
- 1110
- 1100

You need to make justifiable small changes.

Mistake bound: how many training examples will the learner misclassify before converging to a successful hypothesis

A learner with mistake bounds learns more the more times it gets something wrong.

## Haussler's Theorem

### Agnostic Learning Setting
When the concept is not in the hypothesis space. Can still be approximated.

# Thursday Review
- PAC Learning: Delta is certainty, how certain we are that we've hit the error rate. Epsilon is the error rate
- Agnostic Learning Setting: the target concept isn't in the hypothesis space. But we can still search for the target concept as close as possible in the hypothesis space.

# Infinite Hypothesis Space

If the hypothesis space is infinite, but the VC dimension is finite, we can use the VC dimension as an approximation of the VC dimension.

## Proving VC Dimension
General rule, VC dimension

VC dimension: each point gives us 2 vc dimensions.

VC dimension of any convex triangle: 7, the intuition is there are always 3 points, so there are 2 * 3 points at least, but the last one comes from the fact that one of the points need to be some distance away from the other 2 points.

VC dimension of any convex polygon: Infinite. Because there are infinite inputs. The general VC dimension of a convex polygon with p points, the VC dimension is 2p + 1

The circle trick, check these 5 points. The circle is nice because these 5 points are always as far away from each other as possible.
