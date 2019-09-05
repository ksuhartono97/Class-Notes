# Week 1

## Sets:

- Real numbers is a complete set
- Fraction numbers are incomplete

> This class mainly deals with real number Sets

Inner product: multiplication of two vectors, what does this mean?

```
Let there be a vector x and a vector y

xy is x multiplied by y (inner product)

This means that :
- y is projected onto x
- y's direction is the same as the x
- y retains it's magnitude

Given that x and y are both normalized, this means:
- The inner product is exactly cos theta
- Where theta is the angle between vector x and y
```

This means that:
- For non zero vectors, if the inner product is zero, these vectors are orthogonal (as the cosine of the vectors equate to 0) that is the angle is 90 degrees.

Thus, the absolute value of the inner product of two vectors is denoted by:
> |xy| = ||x|| . ||y|| . cos(theta) <=  ||x|| . ||y|| iff x = alpha * y
>
> Where alpha means that there is an angle between x and y

## Matrices

- A<sub>mxn</sub> : common notation
  - capitalized letters
  - mxn denotes the dimension of the matrix
- Available operation:
  - 2A: scalar multiplication
  - A+B: matrix addition
  - A<sub>mxk</sub> B<sub>kxn</sub>: legal only when k is **equal**.
- Known properties:
  - (A+B)<sup>T</sup> = A<sup>T</sup> + B<sup>T</sup>
  - (AB)<sup>T</sup> = B<sup>T</sup>A<sup>T</sup>
- Squared Matrices
  - If A<sup>T</sup> = A then the matrix is symmetric
  - If A, B are upper triangular matrices (all entries *below* main diagonal are zero not including the diagonal) the product of A B is a upper triangular matrix
  - If A<sup>-1</sup> A = A A<sup>-1</sup> = I that is A is nonsingular (invertible)
    - (A<sup>-1</sup>)<sup>-1</sup> = A
    - (AB)<sup>-1</sup> = B<sup>-1</sup>A<sup>-1</sup>
    - abs(A<sup>-1</sup>) = 1/abs(A)

## Spaces

- A space must go to infinity.
- Given a space if you multiply it with a scalar the result should still be in the space's set.

Linearly independent vectors: suppose you have a bunch of vectors (a<sub>1</sub>, ..., a<sub>m</sub>), they are linearly dependent if there exists scalars that is non zero (lambda<sub>1</sub>, ..., lambda<sub>m</sub>) such that `lambda<sub>1</sub> * a<sub>1</sub>, ..., lambda<sub>m</sub> * a<sub>m</sub> = 0`

This means to be linearly independent, there should be a value lambda that breaks that equation.

Thus if x, y (two vectors) != 0  are orthogonal, this implies that they are linearly independent.


sigma (from i to m) of lambda<sub>i</sub>a<sub>i</sub>, (lambda<sub>1</sub>, ..., lambda<sub>m</sub> are part of R<sup>n</sup>) this means that the set is spanned by (a<sub>1</sub>, ..., a<sub>m</sub>)

> TODO: lookup set spanned by vectors

## Functions

> send help
>
> TODO: lookup this thing

## Convex Sets

A set is convex if for any point x and y in the set, and any real number alpha (0 < alpha < 1), alpha * x + (1-alpha) * y is in the set.

This basically says for any two points, for different alphas (represents any points in between the two points), these points are in the set. Essentially, a convex set cannot have holes in it.

- if S is convex, b*S = {b*x: x in S} is a convex set
- if S1 and S2 are convex, S1 + S2 = {x1 + x2, x1 in S1 and x2 in S2}. The result must be a convex set
  - intersection between S1 and S2 must also be a convex set
- a hyperplane separates a set into two (strictly into two). example for 1 dimensional it is a point that separates values to less than and more than. for 2 dimensional it is a line that separates the set to above the line or under the line.
- Halfspaces: the resulting spaces that are separated by a hyperplane. By default they are convex.
- Any convex set S:
  - Separating hyperplane: for a point outside of S, a hyperplane can be created that passes through the point but doesn't touch the set at all.
  - Boundary points: we can find a hyperplane that touches the set. This hyperplane is called a supporting hyperplanes
- Convex Cone: a cone that is convex
- Convex hull: convex hull of a set S is the smallest convex set that includes all the points in S. In other words the intersection of all convex sets containing S. Basically to create it, fill in all the points in between all the points in set S. That is all the convex combinations of the points in set S.
  - Any point inside a convex set can be represented by a convex combination of any other points in the set.
  - But there exists points that are members of the set that cannot be represented by other points. These points are called extreme points.
    - So, let extreme points of a convex set be x
    - There are no two distinct points y, z in S such that x = alpha * y + (1 - alpha) * z for alpha between (0, 1)
  - Connecting these extreme points would create the convex set.
- A closed convex polytope: the intersection of some of the hyperplanes.

## Gaussian Elimination
A<sub>nxn</sub> . x<sub>nx1</sub> = b<sub>nx1</sub> is a series of equations. We can solve such equations using gaussian eliminations. That is we can create a set of equations such that we can create a triangular set of variables. This is done by doing operations(summations between equations or multiplications on both sides) to the existing set of equations. As such we are able to solve the set of equations.

## Eigenvalues and Eigenvectors
For any x in R<sup>n</sup> (x is != 0) and an A that is a square matrix.
- There exists a value x such that when you do A*x this simply changes the magnitude, not the direction.
- That is A * x = lambda * x where lambda is an eigenvalue and x is an eigenvector. As a result `(A - lambda * I) * x = 0` has a solution.
- Meaning that `A - lambda * I` must be a singular matrix.
- Thus that means that the determinant: `|A - lambda * I| = 0`. Such that when solving for the determinant this becomes a system of polynomial equations to the order of n.
- As such there are n solutions to the values of lambda (there exists lambda<sub>1</sub>, ..., lambda<sub>n</sub>). 
