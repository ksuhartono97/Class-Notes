# Functional Dependencies

Convention of FD: X->Y

This means that X is the **determinant set** or LHS of the FD. And Y is the **dependent set** or RHS of the FD.

We say that X determines Y or Y depends on X.

## Trivial FDs

An FD is trivial if in X->Y and Y is a subset of X.

Is always true for all relation instances

It is called trivial due to it having an overlap, as in there is no new information introduced in this case.

## Non-Trivial FDs

Are just the opposite of trivial FDs, are non-trivial if there are no overlaps.

## Closure of a set of Functional Dependencies

Armstrong's Axioms:

- Reflexivity: If Y is a subset of X then X->Y.
- Augmentation: Given a function dependency, you could append another subset of attributes on the LHS and RHS side.
- Transitivity : X->Y and Y->Z then it can be deduced that X->Z

Rules that can be applied to deduce new dependencies.

> Axiom is something that is fundamentally correct. Similar to theorem, but stronger.

The set of all functional dependencies _logically implied_ by F is called the _closure_ of F denoted as F+

## Redundancy of FDs

Some FDs in a given set of FDs can be inferred (redundant). And some attributes in an FD may be redundant.

### Canonical Cover

A canonical cover for F is a set of dependencies Fc such that :

- F and Fc are equivalent
- Fc contains no redundancy(Concise F)
- The LHS of each functional dependency in Fc is unique.
