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

`length` for `Array` is a *variable*. Meanwhile `length` is a **method** for String.
