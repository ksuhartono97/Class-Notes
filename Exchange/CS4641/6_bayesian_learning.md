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

## Brute Force MAP Learning
Search through every single hypothesis in the hypothesis space, and figure out which is the best hypothesis. But is not good because of the possibility of hypotheses spaces being infinite.

## Bayes Optimal Classifier
Basically gives us the maximum probability of a value.

Pros:
- It aggregates all the hypotheses and looks at the probability of the label given all of this, unlike others which finds the best hypotheses. Means that no other model can do better than this model.
- Can represent a hypothesis that is not in the space
Cons:
- May not be possible because the hypothesis space can be infinite.

## Gibbs Algorithm
Minor alteration of the Bayes Optimal Classifier.
- Select one random hypothesis according to the probability
- Use that hypothesis

Problem is this is still an infinite problem.

## Naive Bayes Classifier
The intuition is given a big block D, we need to look at the attributes covered in the D.

Exercise 1:
```
P (C,T,L) = 3/4
P(!C,!T,!L) = 1/4

P(rain) = 1/2
P(!rain) = 1/2


P(rain | C, T, L): 2/3, pred True


P (rain | !C, !T, !L): pred False
1/4 * 1/2 /

P(rain | C, !T ,!L)

=== Answer
P(rain | C, T, L): 0.66 * 0.5 / P(C,T,L)
P(!rain | C, T, L): 0.33 * 0.5 / P(C,T,L)

66% rain, predict rain.
```

Naive bayes, we need to see every single possible attribute value to be able to make prediction.

Problem 1b
```
C, !T, !L : P (C | T) * P(!T | T) * P (!L | T)

P(C | True) = 1
P(C | False) = 1/2
P(!C | True) = 0
P(!T | True ) = 0
P(!L | True) = 0

Thus, Vnb = (1*1/2)0*0 = 1/2 ?

=== Answer
P(T) = 0.5 * P (C | True) * P(!T | True) * P (!L | True)
     = 0.5 * 1.0 * 0.0 * 0.0 = 0

P(F) = 0.5 * P(C | False) * P (!T | False) * P (!L | False)
     = 0.5 * 0.5 * 0.5 * 0.5 = 0.0625

Thus the max = P(F) thus the likely one is P(F)
```

Note that we still need to see each variable at least once! So we need to be able to make a prediction based on what the probability of a variable is.

### Bayesian m-estimate
Assume ahead of time equal probability over all possible values. Example if 2 possible values then probability of each value is 1/2. This ensures the removal of the probability of something becoming zero if we have never seen it before.

## Bayes Nets
Represent dependency through arrows.

Bayes nets are representations!! Not an algorithm. Most of the good bayes nets construction algorithms need clustering!
