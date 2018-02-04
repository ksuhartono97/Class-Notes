# Pathfinding NavMeshes
Short review:

> Pay attention to the width of the agent

Flood fill: to expand a path network. Plant a seed and expand around. This is important as in a local space, you may not be able to find the global path network, so essentially the use is to grow a local network that can lead the agent to the global path network.

## NavMesh
Convexity test: doing the straight line test, draw a straight line through the object, and ensure that it only goes through.

A convex polygon is something that cannot break the straight line test. Convexity is important because it is necessary to ensure navigation is possible.

Flood filled path network would result in the most dense network.

> isConvex function in utils.py

Major wins of a NavMesh:
- Local movement is easy (can move anywhere inside a convex object)
- A really compact representation, meaning sparse and faster search

Autocreate, works nicely with PCG and dynamic worlds. 
