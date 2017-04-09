# Continuing on Destructor

> Rule of thumb: If you have pointers as data members, define your own destructor to delete it.

Destructor will be called every time the object is destructed!

On lecture note, bug slide:

Number of bugs: 3, list of bugs:

- The `"Titanic"` string was never destructed, meaning that it causes a memory leak.
- At line `x=bug`, `bug` is locally created variable, on leaving scope, destructed, thus causing movie to have a dangling pointer. Because no copying was done here.
- When object `movie` is destroyed, however it has a dangling pointer, which means that it is trying to delete something doesn't exist.

Assignment operator (`=`) does memberwise assignment.

# Order of construction and destruction

> Important: if you create an object with `new` then to call it's destructor, you need to use the `delete` operator.

Data members are constructed as the order in which they are defined. However they are destroyed in the reverse order. Note that only possible if there are no dynamic data types, if there are any dynamic data types, order may be different.

The reason why the destruction order is always reverse of the construction order is because of the **stack**. FILO principle.

> Class data members are **private** by default

Ex:

```c++
class A () {
...
}

class B () {
...
}

class C () {
    A objA;
    B objB;
}
//Construction order: objA, objB
//Destruction order: objB, objA
```

Temporary objects are always destructed when it is out of its scope
