# Relational Data Model

Entities and relationships are represented by tables

Supports physical data independence and frees the user from optimization and implementation issues.

All popular DBMSs(database management systems) are based on relational data model. (or an extension, ex: object-relational data model, gives more support on the idea of OOP).

## The Relational Model

Represents data for an application as a collection of tables

- Relation (product of sets, mathematically) : table
- Attribute : column
- Domain: type and range of attribute values
- Tuple / Record : row
- Attribute value : value in table cell

### Cartesian Product

A relation is **any subset** of the Cartesian product of the domains of values.

### Properties of Relations

- Records are unordered
- All values are atomic (nothing can be multivalued or composite)
- `null` value is used to represent values that are

  - Not applicable
  - Missing
  - Not known

    #### Keys

- Superkey : any **set** of attributes that can identify a unique tuple/record
- Candidate key : A superkey that is minimal (cannot remove any member of the key, if you remove it then it is no longer a key, or it only has one value), can have multiple candidate keys.
- Primary key : One of the candidate keys (chosen by database designer)

> In relational model **every** relation needs a candidate key. However in relational DBMS (practical use) a relation is **not required** to have a candidate key

#### Bank Schema example

Payment Has Loan : A loan has many payments, but the existence of payments itself relies on the existence of loan. (this is a weak relationship)

Account deposits to Customer : many to many

A weak entity should be in total participation with a strong entity

Simplification:

- Account generalization: here there are 2 options available, in this context using option 2 for context cannot be accepted because account still has additional relationships which ensures that there needs to be an account schema. However if there are no additional relationships, both options are correct for choosing
- Address Composite Attribute :
