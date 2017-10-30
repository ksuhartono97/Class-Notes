# Abstract Class and Interface

Putting an `abstract` keyword will make the class into an abstract class. Note, put the `abstract` before `class`. So an example declaration is `public abstract class`. An abstract class should have one or more abstract method is only true in C++, in Java this is not always the case.

Also applicable to methods, an abstract method means that it has an `abstract` keyword and the method doesn't have to be implemented (empty body). In the UML, abstract methods are _italicized_.

Even if the class has no abstract method, there will be no compilation error in Java.

Important:

- Abstract class cannot be instantiated using the `new` operator
- Abstract class cannot contain private methods (cannot be overridden if private)
- Abstract class can have constructors to be called by the subclasses
- Subclass need to provide definitions for all the abstract methods, unless the subclass is also abstract.
- A subclass can override a method in superclass and make it abstract ```Java class Haha { public void desmond() {

  } }

public abstract class Hehe extends Haha{ public abstract void desmond() {

} }

````

## Interfaces
Similar to class, but only put constants (`public static final` variables) and abstract methods.

In an interface, even if `public` and `static` keywords are removed, interface will make it `public` and `static` automatically. Also, methods are `abstract` by default.

In Java, you can implement multiple interfaces. `class ... implements <interfaceA>, <interfaceB>, ...` but remember, it can only extend one superclass.

```Java
public interface Haha {
  public abstract void laughing();
}

// Assume this wrapped in a class
public static void main (String[] args) {
  Haha a = new Haha(); // cannot
  Haha b; //OK
}
````

An interface is able to inherit from multiple interfaces using this syntax: `<access modifier> interface <interface name> extends <interfaces>`

## Pre Defined Interface

A generic interface is defined by putting `<E>` after the name of the class/interface. This sort of interface is comparable to generics in C++.

### Comparable interface
In this case, theres a comparable interface used to compare the objects with each other. The class would have to implement `Comparable<datatype>`

If this is implemented, you can implement the `compareTo` method which means that the objects in your class will be sortable.
Overriding `equals` method is not enough to be able to check which object is larger than the other, need `compareTo` to do this.

Return values of `compareTo` :
- Positive value: first one bigger than second one
- Negative value: first one smaller than second one
- Zero: same

Sample of using comparable
```Java
public class ComparableRectangle
  extends Rectangle
  implements Comparable<ComparableRectangle> { //Needs to be like this, the object is put in parentheses
    public ComparableRectangle(double width, double height) {
      super(width, height);
    }

    @Override //must be implemented to be able to compareTo
    public int compareTo(ComparableRectangle o) {
      //.... put implementation here.
    }
  }
```

Remember, casting needs to be done from a general method to a more specific method to be able to call the method there. Example if you get an `Object` class from argument, you must cast it to `Comparable` to be able to call `compareTo`.

### Clonable interface

```Java
public class Haha {
  //Clone method is here, but method is protected and it is inherited from Object
}

public class Test {
  public static void main (String[] args) {
    Haha a = new Haha();
    Haha b = a.clone(); //This does not work
    // clone method is protected you can't call it here
  }
}

//Can be solved by overriding the method to
public Object clone() {
  return super.clone(); //This is an error BUT WHY?
}

//Because when you're overriding clone method you must put
public class Haha implements Cloneable {
  public Object clone() {
    return super.clone();
  }
}

//Side note, the cloneable interface is empty. We do implements Cloneable only because we want to specifically say that we want to override clone method
```
Note that only shallow copying is done by `super.clone()` from the `Cloneable` interface. So when you have reference variables, you must do deep copying by yourself. Can't just do `super.clone()`.

The `clone` method may throw the `CloneNotSupportedException`, so it must be caught with a try-catch block.

```Java
@Override
public Object clone() {
  House h = null;
  try {
    h = (House)super.clone(); //Can be done for the native datatypes
    h.whenBuilt = (Date)whenBuilt.clone();
    //The above needs to be done when cloning reference objects.
    //Can be done as the Date object itself has already overriden a clone method.
  }
  catch (CloneNotSupportedException ex) {

  }
  return h;
}
```

### Conflict Interfaces
Method overriding for throws statement, if the original methods has a throws statement, do we need to keep it?

You can omit any of the exceptions thrown, but you can't add new exceptions (fewer was okay but more is not).s
