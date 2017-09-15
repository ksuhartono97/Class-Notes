# Classes and Objects in Java

Class in Java is a way to define a new datatype.

Must put access modifier for instance variables and methods.

## Initialization of variables

Explicit initialization or constructors. Explicit as in initialize on declaration. Or use constructors.

> Constructors has no return type and the name must be the same as the class.

## Default Constructors

Default constructor given by Java does nothing. But if this doesn't exist, the following statement will cause errors for the following:

```java
Person p = new Person();
```

## Objects

Are referred to as **instances** of a class. Must use `new` to create new instance of the class.

`default` access means that files that are in the same folder as the class with the default access rights, the other files can access the items with `default access`

Demonstration of access rights in classes :

```java
//A.java
public class A {
  int a; // Default access rights, if same folder can access
  private int cool; //The only way to access this would be the methods in the class
  void func() {
    System.out.println("Hello");
  }
}

public class B {
  int b;
  private void haha() {
    A obj = new A();
    obj.a = 20; //Legal
    obj.cool = 40; //Illegal
    obj.func(); //Legal
  }
}
```

> Java defines even the `main` function inside a class. This is due to the OOP design, only thing you can put outside of a class are `import` statements and comments.

Every class can have a main method. So for example if you have 10 different classes, each with a main method. You can choose which main to start with JVM. This is useful as you can create a main in each file for testing purposes. So you are able to call the functions of the object and test its functionalities.

If a class is marked with a `public` keyword, it means that the filename has to be the same as the class name. If it doesn't have the `public` keyword, it means that you don't need to name the class the same as the file. **However**, you will still need to have a single class with the same class name as the file. You can only have one class with `public` accessor in a file.

Folder is the same as **package** in Java.

### UML (Unified Modelling Language) Class Diagram

Top part of diagram is the classname. The next part of the diagram has the instance variables of the class. Written in format name: datatype for both methods and variables.

Symbols :

- `+` for `public`
- `-` for `private`
- `#` for `protected`
- `none` or `~` for `default`

### Reference Instance Variables

```java
public class Person {
  String name = new String("desmond"); //is legal, java supports initialization on declaration
  int age;
  char gender;
  boolean isScienceMajor;
}
```

If you don't initialize a reference instance variable, its default value is `null`. 0 for numeric(int short byte long double), `\u0000` for chars, `false` for boolean.

### Local variables

If you declare local variables and didn't initialize them, the default values are garbage values. Java only initializes instance variables for you. You are not allowed to use variables with garbage values in Java, will cause compilation error.

### Copying

If its not reference variables it is simple copying.

For reference variables:

```java
Circle c1 = new Circle();
Circle c2 = new Circle();
c1 = c2;
//Will copy the address of the object in c2 to c1\. Meaning these two have a reference
//to the same object.
//Causing the original object that was pointed to by c1 to be killed by JVM.
```

### Garbage Collection

To let JVM know that you'd like to delete the object, you can set the reference variable to `null` and it shall be dead.

### Instance vs Class

Recall that instance is a specific instance of a class. Instance variables belong to a certain instance, while class variables are shared by all the instances of the class.

### Static

Static methods can be called even when you don't have an object. You simply need to call it. However, you mustn't put instance variables in static methods, as the instance variables doesn't exist yet.

An instance can access class variables. Even though you are able to achieve the same result by using the classname. But for instance variables, only way to access is with the object name.
