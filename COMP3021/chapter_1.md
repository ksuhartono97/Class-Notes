# Introduction to Java Programming

Java programs can be platform independent because of it's **bytecode** format after compilation. Allowing it to be used in any OS without needing recompilation due to the existence of JI (Java Interpreter).

Java bytecode file extension : `.class`

Class name must be exactly the same as the filename. Capitalization matters. This only applies to public classes.

Javac : Java compiler, the code to run the compilation is `javac file.java` and to run the program : `java file`. Observe that to run you don't need to put `.class` behind the file name as you only need to run the bytecode file.

Java has the same control constructs as Java, however `for each` is something that Java has that C++ doesn't have.

## Differences between C++ and Java

### Programming Paradigm

C++ is a combination of procedural and object-oriented paradigms. Example, you can put a function without wrapping it inside an object (structural programing) and you can also put it in classes (OOP concepts).

However, Java, which is a pure OOP language, you **must** have a class. Because Java was designed to be an OOP language.

Another point, no global variables and functions in Java, as all need to be wrapped inside a class.

### Primitive Datatypes

In java the variable you put in the parentheses of an if statement **MUST** be a `boolean`. Cannot be any other datatype. The same thing doesn't hold in C++.

In java datatypes other than the 8 primitive datatypes are reference types. Which means that it is similar to a pointer in C++.

```
//C++
Haha* p;

//Java
Haha p;
```

Note that in Java, you don't need asterisk operator, no pointer arithmetics, and no dereferences.

### Object Instantiation

In C++ you can either use new or not use new when declaring primitive datatype variables. In Java, you **cannot use new**, only the normal way. Similarly, in non primitive types, in Java you **must use new** meanwhile in C++ both ways are fine.

In Java, doing `Haha p` is fine, as it doesn't instantiate a `Haha` object. Only the pointer. To actually instantiate the object, one must write `Haha p = new Haha`

Instantiation of an array in Java **must** use `new`. Without it, there will only be a reference.

There is a runtime error in Java when you access out of bounds element. As there is bounds checking in Java.

### Memory Allocation and Deallocation

In java, no memory deallocation required from the user. Auto deallocation, meaning no memory leak.

### Support for GUI

In Java GUI programming support is built-in, unlike C++ there is no built-in libraries for GUI programming.

### Support for console I/O

Java doesn't support the use of operators for console I/O. Meanwhile C++ has `>>` and `<<`.

String concatenation with `+` operator only. Remember also operator precedence, left to right for this.

```
int a = 6;
int b = 2;

System.out.println("Value is " + a + b); //Gives Value is 62
System.out.println(a+b+"Value is"); //Gives 8Value is
```

## Scanners
When finished with the scanner, must close the scanner or there will be error.

## Class
No access keyword in Java means that it's access will be default.

C++ allows grouping of data members, in Java it is not allowed due to the existence of default.
```
//legal in c++ not legal in java
class A{
  public:
    int a;
    int b;
}


//In java must follow this
class A{
  public int a;
  public int b;
}
```

No member initialization list in Java.

```
//Illegal in C++
class A{
  public:
    int a = 1;
    int b;
}


//legal in java
class A{
  public int a = 1;
  public int b;
}
```

No constant member functions in Java.

> meaning Java is simpler
