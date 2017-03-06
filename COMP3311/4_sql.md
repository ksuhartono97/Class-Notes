# SQL

## SQL Structure and Basic Operations

Basic structure of SQL consists of three things:

- select : can put as many entities as you want
- from : which tables, can have as many tables/relations as you want
- where : condition/predicate. Only take rows that fit the condition, because we don't want all the rows, only several that interest us.

The result of a SQL query is a relation (set of tuples) or tables. However, it **may** contain duplicates.

> SQL Queries **can** be nested

If there is a schema that contains the primary keys of other relations, you know that this must be a relationship schema for a many to many relationship.

### Projection : Select

```sql
select branch_name
from loan;
```

Select all branch names in the loan relation(table). Similar to the projection operation in relational algebra.

An `*` denotes "**all** attributes."

> Attributes selected **must** exist in the table

> Duplicates are not removed by default, because duplicate removal is very expensive.

### Projection : Duplicate removal

Keyword `distinct` forces removal of duplicates.

```sql
select distinct branch_name
from loan;
```

Only take distinct elements, if there are elements that are the same, ignore.

### Projection : Arithmetic operations

You can manipulate the values that the query returns by modifying it with arithmetic operations

```sql
select branch_name, loan_number, amount*100
from loan;
```

The returned table will have values exactly like loan, however the loan amount will be scaled by 100.

### Selection : Where

As mentioned, where clause allows specifying a condition that tuples in the from clause must satisfy in order to be included in the result. Some tools given by this clause:

- `between` for a value in range of something.
- `not between` negation of `between`
- `and`, `or`, and `not` as well as arithmetic expressions.

### Natural Join : Where

```sql
select client_name, borrower.loan_number
from borrower, loan
where borrower.loan_number = loan.loan_number
/* is equivalent to */
select client_name, loan_number
from borrower natural join loan;
```

For queries to be equivalent, the attributes must be compatible, then they can be joined.

### Cartesian Product : from

```sql
select *
from borrower, loan
```

> Rarely used without a `where` clause

### Set Operations : Union, Intersect, Except

Automatic duplicate removal included.

> Oracle uses `minus` rather than except

To keep duplicates use:

- Union all : the only one supported by Oracle
- Intersect all
- Except all

### Rename Attributes : As

Attributes can be renamed using the `as` clause:

```sql
old-name as new-name
/*Example*/
select distinct client_name, borrower.loan_number as loan_id
from borrower, loan
```

### String Matching : like

Two operators:

- % : matches any substring
- - : matches any character

```sql
select client_name
from client
where client_street like '%Main%';
```

> Usually **case-sensitive**

Special escaper characters:

- \ to escape % and _
- " to escape '

### Ordering result tuples: Order By

```sql
select distinct client_name
from borrower, loan
where borrower.loan_number = loan.loan_number and branch_name='Perryridge'
order by client_name;
```

Ordering options:

- `asc` : ascending
- `desc` : descending By default it will be in alphabetical order (ascending).

Can also sort on multiple attributes.

```sql
order by client_name desc, amount asc
```

The order at which the arguments are given is a priority order.

## Nested Subqueries

### Set Membership : In

All members in the result of a query.

```sql
select distinct client_name
from borrower
where client_name in select client_name from depositor;
```

> Code block above wants to get all clients who have an account and a loan in the bank.

### Set Membership : Not In

The not version of `in`

### Set Comparison : Some

Any one in a set (at least one).

Example: Query : Find the names of all branches that have greater assets than some (i.e., at least one) branch located in Brooklyn

```sql
select branch_name
from branch
where assets> some (select assets
                  from branch
                  where branch_city='Brooklyn');
```

> = some is equivalent to in, however not = some is not equivalent to not in

### Set comparison : All

Check all.

```sql
select branch_name
from branch
where assets>all (select assets
                  from branch
                  where branch_city='Brooklyn');
```

> not = all is equivalent to not in, = all is not equivalent to in.

### Empty relations test

`exists` condition returns true if argument subquery is **not** empty.

`not exists` condition returns true if argument subquery is empty.

> Be very careful of scope when writing SQL. Any correlation names defined inside an inner scope can only be used in that scope.

### Duplicate tuples test : Unique

`unique` tests for the **non-existence** of duplicate tuples in a subquery.

`not unique` tests for the existence. (returns true if there are two or more duplicates.)

> Not implemented in Oracle.

Note, this fails if tuples contain null values.

## Aggregate Functions

### Computation:

- `avg` : averages the **numbers** in a table. Input **must be** numbers.
- `min` : minimum value
- `max` : maximum value
- `sum` : sum all numbers. Input **must be** numbers.
- `count` : number of values

> Remember, * stands for all attributes

### Group By

Permits display of aggregate results. Without group by, an aggregate query will display a single number.

All attributes in a `select` clause must be in the `group by` clause. However, it is not true in the other way. You can put attributes in the `group by` clause even if they are not in the `select` clause.

### Having

Applies a condition on the group level. The same as `where`, however `where` is applied to tuples. `having` is applied to groups.

### Subqueries in the from clause

To make a derived relation. In order to limit the contents of the domain.

### With

Basically allows you to define something globally, to counter a scope problem.

> Special Note: **All** aggregate function except COUNT ( * ) ignore nulls!

## Database definition

### Data definition language (DDL)

SQL DDL allows the special:

- Schema for each relation (attributes)
- Types of values: no array, queues, boolean, no advanced datatypes. Only simple datatypes.
- User defined types and domains
- Integrity constraints (ICs) : domain, key, foreign key, general. Ex: How do you define a key in the database.
- Physical storage structure
- Set of indices to be maintained
- Security and authorization information for each relation

### Basic Types

Null values are allowed in all the domain types.

Some attributes you need to specify as **not null** such that its value can never be `null`. Example of such an attribute are attributes that you want to use as a primary key.

### User defined types

Use the `create type` command to define a user defined datatype.

Example:

```sql
create type Person_name as char(2) final;
```

> Not all relational systems support user-defined datatypes.

### User defined domains

Using the `create domain` clause to define a new domain. Example:

```sql
create domain hourly_wage numeric(5,2);
```

### Create table

`create table` command for defining and creating a new relation.

### Integrity constraints

An integrity constraint (IC) ensures that authorized changes to the database do not result in a loss of data consistency.

Based upon real world semantics.

### Domain constraints

Define valid values for attributes. Test values and queries to ensure the comparison makes sense.

## Assertions
