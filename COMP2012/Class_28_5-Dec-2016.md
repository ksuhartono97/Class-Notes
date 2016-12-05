#AVL

Binary Search Trees can become unbalanced due to insertion and deletion
of nodes. Therefore there is a need for an algorithm that can rebalance the
trees.

AVL Trees are self-balancing binary search trees, where at most the 
heights of the two child subtrees differ at most by one. Each node stores
a height value, which refers to the height of the node.

If at any moment the height difference differ by more than one, rebalancing
is done to fix this problem.

Efficiency of any operation on an AVL tree always has **order of logn**.


Rebalancing done by **left** or **right** rotation. Or a combination of the two (left-right or right-left)

Problematic node is the node that has a height difference of > 1 for its subtrees

Problem causing node is the source of the problem (usually the inserted or deleted node) and
is useful to judge what type of rotation should we use.

For single rotation, always perform the rotation on the problematic node

If there are more than one problematic node, always fix the bottom problematic node first.

You should perform first rotation on the node **directly under** the problematic node!
And the second rotation **on the** problematic node directly!

###Deletion
- If the node is a leaf, remove immediately
- If the node has 1 child, adjust a parent pointer to bypass the deleted node.
As in make the grandparent point to the child
- If the node has 2 children, replace the deleted node with maximum node in its left sub tree, or the minimum
node in the right sub tree. Then remove the chosen node.

Deletion can choose max/min either way result is same.

