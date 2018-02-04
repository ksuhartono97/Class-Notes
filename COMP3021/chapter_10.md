# Generics

Generics is similar to template in C++, but they are not exactly the same!

> Arraylists can be used to store different type of variables at different times. But we can't store different kinds of elements in the same container! (Note that it is doable, but risky)

We can put different elements (different datatypes) in a container, by using an unparameterized arraylist, then simply add stuff into the arraylist.

We can make both method and class as generic.

```Java
public class Haha <E> {
  public<E> Hehe waow (E huh) {

  }
}
```

Class as generic:
```Java
//Definition
public class GenericStack<E> {...}
//Usage
GenericStack<String> stackOfString = new GenericStack<String>;
```

A compiler error will occur if we attempt to use the class or method with an incompatible object (this is a benefit of using generics).

Prior to JDK 1.5, this would give a runtime error instead of a compilation error. Now it'll give a compilation error, which is better since we can see it and fix it.

An unparameterized generic class or interface is called a "raw type", it is roughly equivalent to putting `Object` to the type.

The ? symbol is the wildcard symbol.
