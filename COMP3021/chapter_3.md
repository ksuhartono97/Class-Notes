# Strings and Wrapper Classes

String is not a primitive type!

With string, you don't need to use `new` keyword to create it even though it is non primitive. This is due to `Strings` being really common.

When you do `String asd;` this is a reference variable. No object instantiated.

`String msg3 = new "Welcome to COMP3021"` is allowed. However it is not recommended as it is weird.

String object is immutable.

```java
String str = "Desmond";
str = "Discman";
```

The above code doesn't modify the content of `str`. It changes the reference of `str`. Meaning the first object gets killed while the second one is still there.

## String Comparison

Creating two string objects that contain the same thing will cause Java to point the two objects to the same thing. This is done to save memory. This happens if you don't use `new`, if you use `new`, it **will not** point it to the same object, it will be different.

```java
String a = "haha";
String b = "hehe";
if(a == b) { // Will always return false
  ...
}
//If you do the above, what happens is that it compares the
//strings address instead of the content
//Causing it to always return false

// To compare content you must use
a.equals(b);

//Assume different code
String a="haha";
String b=new String("haha");
a == b; //is false
a.equals(b); //true

String c= new String("Haha");
b.equals(c); //false
b.equalsIgnoreCase(c); //true
```

There are other methods in the Java string class for comparison of the contents.

`compareTo` to check if a string is smaller than, bigger than, or equals.(based on alphabetical order, as in ASCII code comparison). The comparison is done by subtracting the value in the first string with the value in second string. So based on the positive or negativeness of the result.

`length` for `Array` is a _variable_. Meanwhile `length` is a **method** for String.

## Listening to inputs

To listen to a keyboard character input:

```java
import java.util.Scanner;

public class Testing {
  public static void main (String args[]) {
    Scanner sc = new Scanner(System.in);
    sc.next().charAt(0); //Gets the first character of the string input
  }
}
```

Remember, you **must** close the `Scanner` object when you finish using it.

## String Concatenation

You can use two ways `string1.concat(string2)` or `string1 + string2` can use either one. It's the same thing.

## Substring extraction

Using the method `substring()` to extract a substring from the string. Use cases:

- `str.substring(startIndex, endIndex)` : will extract characters from and including the `startIndex` all the way until but not including the `endIndex`. So for example `str.substring(0,9)` will extract from 0 index to 8th index.
- `str.substring(startIndex)` if you only put one value, then it will extract values from the startIndex (inclusive) till the end of the string.

> Remember that substring is a **single** word. Do not do the function call with `subString`.

For other string methods you can access the slides for other functions regarding converting, replacing, and splitting strings. Also methods for finding a character or a substring in a string.

Getting a string representation of a non string variable (without `valueOf` method):

```java
int a = 10;
String str = "" + a; //Gives '10' in string format.
```

Java treats decimal numbers as a double by default. If you want to make it into a float, then you must add `F` to the number. Same thing applies to normal numbers that are considered `int` by default. If you want to make it say, `long` then you must add `L` to the number. Only these 2 are available by default in Java.

For others you must do this:

```java
import java.util.Scanner;

public class Testing {
  public static void main(String args[]) {
    System.out.println((byte)10);
  }
}
```

Basically doing typecasting.

## `StringBuilder` and `StringBuffer`

Are mutable classes as opposite to normal strings who are immutable. More useful in cases when you want to manipulate the `String` multiple times. Unlike the default `String` object where you'll keep on recreating a new object everytime you change it. It is much better to use the `StringBuilder` class.

## Converting string type to other types

`<Datatype>.parse<Datatype>()`, examples:

- `Integer.parseInt(string)`
- `Double.parseDouble(string)`

## Wrapper Classes

> Recall: You cannot pass primitive datatypes by reference in Java. To pass something by reference you must use non-primitive datatypes.

However, if you'd like to pass by reference, there are wrapper classes for the 8 primitive datatypes. A wrapper class is a class that can encapsulate the datatype's data. Achieved through owning an instance variable of the datatype to contain the datatype's value. It also provides methods to modify the data.

```java
public class Example {
  public static void main (String args[]) {
    int a = 10;
    Integer aa = new Integer(10); //Create a wrapper class

    int b = aa; // Legal
    //Java knows that the primitive type and the wrapper object is actually equivalent
    //So it will extract the value and assign it for you
    //This is called UNBOXING

    aa = 20; //Is also legal
    //This is called boxing
    //However, here it instantiates a new object instead of modifying the value.

    aa++; //Also works
  }
}
```

**Autoboxing** means both boxing and unboxing. This basically allows the wrapper class to be used the same way as the data type.

There are no default constructors for the `Integer` and `Double` classes, but it has 2 conversion constructors, one expects the primitive type input the other expects a String input.

When you attempt to convert a non numerical value to the wrapper class String constructor, it will give an exception.

To get the stored value, you can use the accessor `<datatype>Value()`, for instance `intValue()` and `doubleValue()`. You can also use these methods to convert a datatype to a different datatype.

`valueOf()` method can be used to convert a numeric string to the wrapper class.

```java
public class Example {
  public static void main(String args[]) {
    Integer haha = new Integer(123);
    int a = haha; //unboxing
    int b = haha + haha; //2 unboxing
    Integer c = haha + haha; //2 unboxing and 1 boxing
  }
}
```

> %h is used to print out the hashcode.
