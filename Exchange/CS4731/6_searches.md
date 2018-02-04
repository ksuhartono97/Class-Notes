# Searches

Detecting negative cycles: a node getting to itself should always be zero, but if there is a negative value, it gets infinitely cheap, meaning that there might be something wrong, so you'll have to recompute such that there is no negative edge.

When to use A*/Djikstra/APSP:
- If environment is small and static: djikstra
- If environment is dynamic: A*
- If environment is large and static: it depends
  - If runtime memory is an issue: Lookup Table with Djikstra or
  - If runtime memory isn't an issue:

In sticky situations such as when there are objects that dynamically change over time.

You wanna put things that can change the behaviour, so you don't want the AI to make the character do the same thing over and over again. 
