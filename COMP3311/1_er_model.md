# Entity Relationship Models

Entity is an object that exists independently and is distinguishable from other objects (not an official definition, no specific definition exists).

> TLDR : Entity = Object

## Attributes

Definition: Properties of an entity or relationship

Types:

- Simple : contains a single value
- Composite : consists of several components
- Multivalued : contains more than one value (double circle)
- Derived : can be computed from other attributes (dotted line)
- Key : used to identify an entity (underline) (**only primary key may be underlined**)

> Note: composite key can be expressed by underlining the elements of the keys.

## Relationship

An association among entities

**Degree** : number of entity sets that participate in a relationship set

> Binary: degree two

### Cardinality constraints:

- Directed line : one
- Undirected line : many
- Double line : double line

## Weak Entity Sets

Doesn't have a primary key, its distinctive attribute is called **discriminator** or partial key.

If it exists, relationship must be drawn with double diamond.

Its existence depends on the existence of an identifying entity set. Must be related via a total or one-to-many from identifying to weak entity set.

## ISA (is a) Hierarchies

If overlap constraints are disallowed then you must specify with a tag **disjoint**.

Covering constraints use total relationship sign (double line)
