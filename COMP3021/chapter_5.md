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

Before executing code in the `throw` block you must do all the things in the `finally` block.

If the method is going to have an exception, and the method doesn't catch it, the method header must have `throws <exception class name>` and it can have multiple exception classes.

### Exception Propagation

Remember that when there is exception object thrown, the code lines under the part where the exception happened is not executed. Even in the case of nested function calls, the function where the exception happened is considered an exception until the exception is caught.

### Multiple Throws and Catches

One `try` block can have more than one `catch` blocks. Also works for `throws`, the method can have more than 1 `throw`.

```java
try {
  ...
}
catch(Exception e1) {
  ...
}
catch(ArithmeticException e2) {

}
catch(IOException e3) {
  ...
}
// This code would say that that e2 and e3 are unreachable
// Due to e2 and e3 being a subclass of e1\. Meaning that any exceptions
// will get caught by e1.
```

So if you want to do something like the above code, put the more **specific** ones before the more general one.

### Rethrowing Exceptions

A thrown exception can be rethrown in the `catch` block. The reason why we would do that is that we want to tell the method that calls it that there was an error, even though it has been handled. The keyword used is still `throw`.

### Notes on using exceptions

- Must use `try`, without `try` cannot put a `catch` block
- A `try` must be followed with `catch` or `finally`
- Don't put statements in between `try` and `catch`
- A `try` with only `finally` must still declare the exception in the function header

### Define Custom Exception Classes

Define a class that extends `Exception`.

> Notes, remember that even if there is a `return` statement, the line under `finally` will be executed. The only way that the finally will not be executed is by calling `System.exit(0)`

> If you throw a **checked** exception, and then it gets rethrown, you must still put a `throws` in the function header.

## Assertions

Asserts an assumption about your program. The syntax is `assert <boolean expression>`. Used to deal with the correctness of the program. Mainly used for the programmer's own problems (tackling programming bugs). But for exceptions, it is mostly used to handle user and other programmer problems.

You generally don't use assertion to check whether method input parameters are correct or not.

> Solution to slide 50:

> - if else
> - exception
> - assertion
> - exception
> - assertion

## File I/O

Need to access data stored in long term memory.

### File Class

`File <varname> = new File("<pathname>")` is how you define a new file object.

The file class has multiple methods to check the validity of the file and get information about the file.

### PrintWriter Class

Used to write data into a file, but you can only write **plaintext** to write into a file.

Remember, must `close()` the file if you do not close the file, **the data will not be written to the file**. The data is written to the file when the file is closed.

### Reading Data from the Web

Need a URL object, `URL url = new URL("<url>")`, then you open it with `Scanner input = new Scanner(url.openStream())`. This will allow you to access data from a file on the web.
