#Continuing on Constructor

All constructors have the same name, because C++ has function overloading

>Side fact: Also known as method overloading in Java

Constructors are often overloaded, so that users can pass different parameters to construct 
a new object.

> The signs +, - ,\ are all functions in C++, they have different uses because they are overloaded


##Function Default Arguments
```cpp
class A{
    public:
        void func (int a, int b, int c) { 
            // Suppose you only have 2 default values for the variables
            // Where should you put them?            
        }
        //Ans:
        func(int a, int b=3, int c= 2) {
            //Rule, you should give default values to the ones on the right
        }
};
```

>Rule : In a function default values should be given to the arguments **on the right** first

```cpp
class A{
    private: 
        int a;
        int b;
        int c;
    public:
        A(int aHaha = 1, int bHaha = 2, int cHaha = 3) {
        // Why does constructors often have default values?
        // Because then the constructor will have flexibility in creating
        // new objects. Instead of defining a lot of constructors for different cases
        // We can define one constructor for all
        }      
};
```

Generally using default function arguments is more preferrable to using function overloading

A parameter can only have its `default argument` specified only **once** in a file, usually in the 
header, not in the function definition. If done twice, there will be an error. Because it is redundant.

`default arguments` are usually specified in the .h file is so that other people knows exactly how many values 
other people who are going to use the function need to give it.

##Member Initialization List

``` cpp
class A{
    private: 
        int a;
        int b;
        int c;
    public:
        A() : a(1), b(2), c(3) //This is a member initialization list
        { 
            //Does the same thing as:
            //a = 1;
            //b = 2;
            //c = 3;
        }      
};
```
Member initialization list is only available for use in the `constructor`.
It is not allowed to be put in member functions!

The reason why this is needed is because the mechanism of creation and initialization is different.
Without the member initialization list, you need to:
- Create the data members first, e.g.: `int a`, `int b`, `int c`
- After all of them are created, put in data members 

With the member initialization list:
- Create the data members and assign the value at the same time, 
i.e. create a variable then assign the value directly.

Why is this important? Say one of your data member is a `const`, then the normal method,
using assignment, would not work. As for a `const` variable it needs to get its value
when its created. Thus you would need the member initialization list. Another example that 
needs this is if you have reference variables (`&`).

```cpp
class A {
    int a,b;
    public:
        A() {a = 1; b =2;}
        A(int x, int y) { a = x; b = y;}
        void setA(int x) {a = x;}
        void setB(int y) {b = y;}
};

class B {
    A haha;
    A hehe;
    B() {
        haha.setA(10);
        haha.setB(20);
        hehe.setA(30);
        hehe.setB(40);
    }
};
       
// Is it better to use member initialization here?
// Yes, because here, the default construction calls are redundant
// So: 
class B{
    A haha;
    A hehe;
    B() : haha(10, 20), hehe(30, 40) {}
}
//Is much better because we do not waste constructor calls.
```

Data member initialization list should be used in initializing:
- `const` data members
- Reference data members
- Other objects

#Destructors
When you define anything with `new` it will get memory from the heap
of your computer. 

```cpp 
class A  {
    int* arr;
    A() {
        arr = new int[9999999];
    }
}
int main() {
    A haha;
}
//the memory is not returned here, and then when the main exits
//no one has the address of the arr anymore. Memory leakage.

//So in class A definition:
~A() {
    delete [] arr;
} 
```

To prevent this thing from happening, we need the destructor
which is called when we call `delete` on the object or when the 
object is about to be destroyed, e.g. : leaving the function.

You can only have one destructor, as we are not gonna pass any values
to the destructor, then there is no way to overload a destructor.

If no destructor is defined, C++ will define a destructor for you.


