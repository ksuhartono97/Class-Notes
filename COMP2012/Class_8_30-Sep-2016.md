#Class 8

###Continuing on constructors

Surprise implicit conversion:
```cpp
class Word {
    ...
    public:
        Word(char c) {...}
        Word (const char* s) {...}
        void print() const {...}
    
}

void print_word (Word x) {x.print();}
int main () {
    print_word("Titanic"); //String will be converted to Word by conversion
    print_word('A'); //Char will be converted to Word by conversion
    
    //Why is this a surprise?
    //Because it is converted using the constructors without being asked to
    //Type conversion from string and char to word
    
    return 0;
}
```

How to prevent surprises like this? Use the keyword `explicit`. It will disallow
implicit conversion with the constructor.

**Copy Constructors** : a constructor that can use an object of its type
and use that object to initialize its data members.

Ex : 
```cpp
class A {
    private:
        int a;
        int b;
    public:
        A(const A& object) //Has to follow this structure, if not like this, not a copy constructor
        {
            a = dearDaniel.a;
            b = dearDaniel.b; //Same object, knows its data members
        }
}
```

Can also use `=` to pass an object, however this is an implicit call of the constructor.

If the return type of a function is the object (of the same class type), then you want to create a new object
with that returned value, it will call the copy constructor.

If there is no copy constructor is defined, C++ **will supply  a default copy
constructor** for the class. In the event that you try to create a new object by
copying, the default copy constructor would do **memberwise** assignment.
Meaning that it will copy all the data members of the object given to it to 
the new object.

>If you do not have constructors at all in your class, C++ compilers will provide you with **2 constructors**. The default constructor and a copy constructor.

Copying in this constructor works even for array members. However they will be sharing the array.
More commonly known as *shallow* copying (if the data member is a pointer or dynamic). 

Important note: If all class data types are primitive, you can utilise the default
copy constructor. Else define your own copy constructor is better.

Example of creating your own copy constructor to prevent such an error:
```cpp
class A {
    private:
        int* arr;
    public:
    A() {arr = new int[10];} //Size of array is hardcoded, lol
    A (const A& mrHappy) {
        arr = new int[10]; //Make a new array
        for(int i = 0; i<10; i++) //Copy contents of given array
            arr[i] = mrHappy.arr[i];
    } //code is for deep copying
    // if for some reason you want to do shallow
    // code : arr = mrHappy.arr;
};

int main () {
    A obj1;
    A obj2(obj1); //call the copy constructor
    //Both objects will have their own arrays!
    return 0;
}
```

Exceptions:
```cpp
    A (A& mrHappy) {...}
    //not recognized as copy constructor
    //default constructor will be given
    //However which one will get called??
    //if you call it with:
    //const A obj1;
    //A obj2(obj1);
    //This is an error, you don't get a constructor
```

```cpp
    A (const A mrHappy) {...}
    //Error
    //impossible situation
    //you haven't created the object but you put const
    //cannot modify
    //cannot make
```