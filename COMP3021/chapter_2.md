# Classes and Objects in Java
Class in Java is a way to define a new datatype.

Must put access modifier for instance variables and methods.

## Initialization of variables
Explicit initialization or constructors. Explicit as in initialize on declaration. Or use constructors.

> Constructors has no return type and the name must be the same as the class.

## Default Constructors
Default constructor given by Java does nothing. But if this doesn't exist, the following statement will cause errors for the following:

```Java
Person p = new Person();
```

## Objects
Are referred to as **instances** of a class. Must use `new` to create new instance of the class.

`default` access means that files that are in the same folder as the class with the default access rights, the other files can access the items with `default access`
