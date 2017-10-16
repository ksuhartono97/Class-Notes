# Reinforcement Learning

## Model Based Learning
Learn an approximate model based on experience.

## Model Free Learning

### Passive Reinforcement Learning
Basically, apply a given policy.

#### Direct Evaluation
Given a policy, we want to compute all the utilities and values associated with the states. We assume that the policy is fixed (passive reinforcement, no change).

The goal is to learn the state values **directly**.

The idea is simple, to average all the values. So, every time you visit a state, write the discounted values. So with all these values from the episodes, we can sum up all the values and average them. And eventually it will tend to seeing the MDPs.

However, the estimation can be not very accurate if the number of episodes are too little. Due to the characteristic of examining each state separately.

#### Temporal Difference Learning
Update the values everytime there is a transition (learning from a new experience).

### Active Reinforcement Learning

#### Q-Value Iteration
Remember in value iteration, we implicitly update the policy by updating the values.

In Q value iteration we do not follow any policy, we simply play the game a lot and figure out the best way. 
