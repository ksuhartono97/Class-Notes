# Exception Handling, Assertion, and File I/O

In some cases, if you don't do exception handling, program will not compile. (C++ has it too)

A common practice is using `if` statements to do error handling, this is not a good thing as you mix useful code and error checking code.

## Exception handling

Separation using `try` and `catch`. Put the useful code in the `try` section and put error handling in `catch` blocks. Actually does the same thing with the `if` statement error handling but code structure looks better.

Example in slides, computing average marks. There could be an issue if the number of students is 0, causing an error during division.

The way try catch works is basically, the `try` block runs the code, and then when there is an error, create an `Exception` object and then throw out of the `try` block. Then a `catch` block will catch it.

Syntax to create a new exception : `throw new Exception("Error message")`

There is a `finally` section that you can use to put in some code that will run when the try block finishes.

There are different exception objects, the `Exception` object is a superclass of all these other exception types.

The exception class has two constructors:

- `Exception()`
- `Exception(String message)`

And it has some methods that are useful:

- `getMessage()` : returns the message that you specified in the constructor.
- `printStackTrace()` : prints on screen a trace of all the methods that were called leading up to the method that throws the exception.
- `toString()` : will return the message, and some extra stuff about the exception.

Two types of exceptions in Java's exception hierarchy:

- Unchecked exceptions : compiler is **not** going the check for possible troubles in compilation time. Runtime exceptions fall in this category. Do not need to be handled by the programmer, but you can still catch them if you want to.
- Checked exceptions : during compilation time, possible troubles are checked. These type of exceptions **must** be handled.

After method parameters, you must put `throws new Exception` if the method is going to throw an exception. If you do not put this, the compiler will give an error. The exception should be catched by the method caller. If the exception is not caught, eventually the exception will be handled by JVM, which will cause a runtime error.

```java
public class Hehe {
  public void method1 () {
    throw new Exception("Do something func!");
  }
  public void method2() {
    method1();
  }
  public static void main (String[] args) {
    Hehe hehe = new Hehe();
    hehe.method2();
  }
}
//Free compilation error for you!
// Need to do this to method1
public void method1() {
  try {
    throw new Exception("Do something func!";)
  }
  catch (Exception e) {

  }
}

// or this
public void method1() throws Exception{
  throw new Exception("Do something func!";)
}

//but method2 must become this.
public void method2() {
  try {
    method1();
  }
  catch(Exception e) {

  }
}
```
