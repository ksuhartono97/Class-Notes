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
