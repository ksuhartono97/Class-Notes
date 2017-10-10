# Inheritance and Polymorphism

Only **public** inheritance available in Java.

An arrow in UML means that the class inherits from the object that the arrow is pointing to.

Remember that you use `extends` to inherit from a superclass.

```java
public class Haha {
  private int a;
  private int b;
  Haha(int a, int b) {
    this.a = a;
    this.b = b;
  }
  public String toString() {
    return "a : " + a + ", b : " + b;
  }
}

public class TestHaha {
  public static void main (String[] args) {
    Haha h =  new Haha(1,2);
    System.out.println(h.toString()); //not necessary!!
    // Can simply do:
    System.out.println(h); //Java will invoke the toString method automatically.
  }
}
```

## Superclass constructors

Superclass constructors are **not inherited**, they can be used but the subclass does not have it. Every other method and instance variable is still inherited though.

> Remember again, every Java class inherits from the `Object` class! Even if you don't explicitly say extends from `Object`, the Java class by default inherits from `Object`.

If you don't explicitly invoke the superclass's constructor with `super`, Java will call `super()` for you.

```java
class A {
  A() {
    System.out.println("Default constructor of A");
  }
}

public class B extends A {
  public B() {
    //Java will call super() here for you even if you don't explicitly call it

  }
}

public class C {
  public static void main (String[] args) {
    B obj = new B();
  }
}
```

The above code will output the code in the default constructor of A

Say we modify class B to this :

```java
public class B extends A {
  // public B() {
  //   //Java will call super() here for you even if you don't explicitly call it
  //   
  // }
}
```

Still same output as the default constructor of Java will still the `super` method.

Even if you define an extra constructor, Java will still call the super() method if you don't call it.

Let's say we modify A and B to this

```java
class A {
  // A() {
  //   System.out.println("Default constructor of A");
  // }
  public A(int a) {

  }
  public class B extends A {
    public B(int a) {

    }
  }
}
```

In this case, in the B class constructor Java puts a `super()` call. However, the A class constructor doesn't have a **default constructor**. So this edit would cause a compilation error.

A call to `super()` must be the **first statement** when it is called explicitly. This will cause a compilation error.

When you call `this()` it means that you will call the constructor of the **same** class!

## Subclass

When doing method overriding, the access modifier must be exactly the same. Also, you can't always do method overriding. You can only override those methods with `public` and `protected` access modifiers. `private` methods cannot be overridden.

You can redefine a static method in a subclass even though it has inherited a static method with the same name from the superclass. However, when you redefine it, the two static methods are completely unrelated even though they have the same name. But when you do this, there is absolutely no way to call the static method that you inherited from the superclass.

Static methods **cannot** be overridden in Java! As mentioned above it just seems like you are overriding but in reality you are not.

```java
public class A {
  protected void func (){
    ...
  }
}

public class B extends A {
  protected void func() {
    ...
  }
}
//Here method overriding is being done, as the method is exactly the same as the superclass

//What if we change to
public class B extends A {
  public void func() {
    ...
  }
}
//Here, overriding is still happening.
```

In Java, when you change the access modifier, method overriding is still done.

What if we do this

```java
public class B extends A {
  private void func() {
    ...
  }
}
//Compilation error.
```

If it is originally protected, you can either change the modifier in `B` to be `protected` or `public`. `default` will also give an error in this case.

Java's rule is that you cannot make the access modifier more **restrictive**, you can relax it but not restrict it.

On overriding, it is possible to have different return types. If the overriding method's return type is a subclass of the overridden method.

```java
//Suppose we have class A, and B is a subclass of A
public class C {
  public B func() {...}
}

public class D {
  public A func() {...}
}
```

Here we can see that the function in class `D` is overriding the function in class `C`. In this case, class `A` is **not** a subclass of class `B`. It is the other way around! Meaning that in this case, this overriding is illegal.

But if you swap the two functions, then it is completely legal.

> Easy way to memorize, in the subclass, the function should return a subclass. In the superclass, the function should return a superclass.

## `toString()` method

When defining a class you should always override this method so that it can be used to print out the contents of the object.

## Polymorphism

Generally defined as a variable of the supertype can refer to a subtype object. (Liskov Substitution Principle)

Passing an `integer` to something that expects an `Object` to print out, it will still work. You won't have to convert it to `String` first as autoboxing will be done for you.

See slides for details, pretty clear.

### Dynamic Binding

The chain of searching always starts from the subclass. It will start calling the function in the subclass and then go up.

Easy way to remember is you always call the function of the object itself, if you cannot find it, check in the superclass.

> Dynamic binding for method overriding, method matching for method overloading.

Dynamic binding is done automatically, meaning that we cannot call the function in superclass (when you want to choose).

```java
public class A {
  public final void func () {
    ...
  }
}

public class B {
  public void func () {
    ...
  }
}
// This will result in an error.
```

`final` means that this method **cannot be overridden**.

```java
public class A {
  public final void func () {
    ...
  }
}

public class B {

}

public class C {
  public static void main (String[] args) {
    A haha = new B();
    haha.func(); //Calls the method in A
  }
}
```

This is the only scenario in which you can call the superclass's method using the subclass object.

### Generic Programming

Can be achieved through the use of polymorphism

### Explicit Casting

Can be done to force an object of the superclass to become a subclass.

Should only be done if you are confident that it completely makes sense. In the sense that the it should only be done if the superclass reference is pointing to a subclass object. If you are not sure what the superclass reference is referencing, it might be dangerous if this is done.

### `instanceof` operator

Is an operator that is used to check whether a certain object is an instance of a class/interface.

### `equals()` method

The equals method in `StringBuffer` is inherited from the `Object` class. Meaning that it only does address comparison, not content comparison. Unlike in the `String` class where the `equals()` method is overridden so it compares content.

This is a tricky problem, beware!

Common practice is always override the `equals()` method to do content comparison in your classes.

```java
class Haha {
  private int a;
  public Haha (int a) { this.a = a; }
}

public class TestHaha {
  public static void main (String[] args) {
    Haha obj1 = new Haha(10);
    Haha obj2 = new Haha(10);
    if(obj1.equals(obj2))
      System.out.println("Yes, same!");
    else
      System.out.println("No, different!");
  }
}

// The output of the above program is No, different!
// As we compare the address

//But if you add this method to Haha class
public boolean equals(Object o) {
  return (a == ((Haha)o).a);
}
```

### The Protected modifier

Allows all descendants and files in the same folder to access something. Meaning that `default` is more restrictive compared to `protected`.

### `final` keyword

Makes a method not overrideable. Also makes it such that something is constant.

For a class marked `final`, it means that no inheritance can be done to this class.

### Initializing Instance Variables

There are 3 ways:

- Field Initializer
- Instance Initializer Block
- Constructor

```java
double height = 183.5;
{ height = 10; }

//The later one overrides the previous
//Final height value is 10
```

## Extra Notes

Put `@Override` before a method that is going to be overridden, the point is to inform Java that we want to override a method. Java will check if you are doing method overriding properly

The `@Override` is called an annotation. Examples are :

- `@Override`
- `@param`
- `@return`

All these are annotations.

Arrays are **objects** in Java!!
