# Learning MDPs

Fixing the infinite loop problem:
- Introduce a discount
- Introduce a horizon

So redefining the policy to maximizing expected **discounted** reward from every state.

Problems with value and policy iteration:
- Have to iterate through every single state (large/infinite states)
- No transition model

RL value iteration exercise:

How to do value iteration?:
- Discretise the space using the gps coordinates (round them down or up to get an approximate position), and create a sort of gridworld to represent the states with the goal state being point B.
- Assign a reward to point B, just a positive reward will do
- Assign a mild living penalty, so that there will be an attempt to navigate to the target state as fast as possible
- Allow 8 direction movements between states.
- Transition function where probability of moving from a location to another location (states) is always 1
- Have a second space for the height, do a separate value iteration for it, attempt to maintain a certain height.
