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

## Useful Classes

### The Date Class

Default constructor : current time. A certain date, use special constructor (pass in time).

> Almost all classes in Java has a `toString` method that gives you a string representation of the object. Is a Java convention.

### The Random Class

For obtaining random numbers. Better than `Math.random` class due to certain methods allowing more flexibility in random number generation. More general.

The constructor expects a random seed. However if you don't give it, the constructor will use the current time as a seed.

### Point 2D Class

Used to represent a point in 2D plane. Can also compute distance between 2 points.

## Access Modifier and Accessor/Mutator methods

- `public` : anyone can see
- `default` : in same folder / package
- `private` : only internally inside the class
- `protected` : restricts to only subclasses (in or different package).

Class keyword in Java is used to define new type, normally before `class` keyword you put the `public` (or `default` modifier. You are not allowed to put `protected` and `private`.

> Note, except when you have inner classes. Then you can give it `private`

Instance variables should be kept `private`. Methods are usually `public` however, you can assign a `private` to method if you only intend to use it inside the class.

If you only provide `getter` and no `setter` it implies that you don't want people to be able to modify the value of the instance variable.

To pass by value, you must use primitive type variables. Non-primitive are by default references, meaning you pass by reference by default.

## Array of Objects

Standard array manipulation:

```java
double[] arr = new double[10];
arr[1] = 1.234567;
```

Array of Objects:

```java
Haha[] hahaha = new Haha[10];
//Creates empty references to objects (10 pointers) not 10 object instances.
for(int i = 0; i< 10; i++) {
  hahaha[i] = new Haha();
}
```

Another example:

```java
// Suppose we have defined a class "Person" with a
// default constructors
// *** To create an array, of Person objects, we do ***

Person[] personArr = new Person[10]; // Remember as shown above, this is just 10 references
for (int i = 0; i<10; i++) {
  personArr[i] = new Person();  //Here is where the objects are created.
}

personArr[1] = null; //Deletes the single object instance
personArr = null; //Wipes the whole array
```

Often a method is defined to get back the array of objects. (create the array only) This is done for readability.

> `printf` for formatted printing, `%[-number]s`, the number will declare the size of each string, each `%s` means you'll substitute something. The `-` before the number means left-justified. For right-justified text, just remove the `-` or put a `+` instead.

## Immutable Objects and Classes

- All data fields are `private`
- No mutators, at all
- Can define get method, however can be risky. As you can return the reference to an object instead of the value only. Meaning you can mutate the object.

> To define an immutable class, then you need to satisfy, all instance variables are `private`, no set method, no get method that returns reference to instance variables.

## `this` keyword

Name conflict resolution `this`. When you do this you can differentiate between the variables of the class and argument variables.

Can also use to call the constructor from somewhere else.
