# Bayesian Learning

Review:
- VC-Dimension: Representative power of H
- Circle Trick : a way to prove the VC dimension
- Proving VC Dimension:
  - Prove a lower bound : for some set of input x, represent all values
  - Prove an upper bound : some set of x, 1 set of values was impossible

The big idea of bayesian learning is given chances of some events happening, what is the probability of this event happening.

## Bayes Theorem

P (a | b) = P(b | a) * P (a) / P(b)

If we know the probability of cause given effect, we can figure out the probability of effect given cause.

Example in slides :
```
P(fire|alarm) : P(alarm|fire) * P (fire) / P(alarm)
= 0.98 * 0.008 / P (alarm) = 0.0078 / P (alarm)

P(-fire|alarm) : P(alarm|-fire) * P(-fire) / P(alarm)
= 0.03 * 0.992 / P (alarm) = 0.0298 / P(alarm)

To determine P(alarm), we need to use law of total probability, but we don't need to

As we can see above we can see the relation, and we can see that P(-fire | alarm)
is 3 times more likely than P(fire|alarm)
```

What we care about is the probability of a certain label

## Bayes Optimal Classifier
Basically gives us the maximum probability of a value.

Pros:
- It aggregates all the hypotheses and looks at the probability of the label given all of this, unlike others which finds the best hypotheses. Means that no other model can do better than this model.
- Can represent a hypothesis that is not in the space
Cons:
- May not be possible because the hypothesis space can be infinite.
