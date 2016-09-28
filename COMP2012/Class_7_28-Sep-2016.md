#Class 7 


###Continuing on const-ness
```cpp
class Haha{
    private:
        int arr[100000000]; //Huge array size
    public:
        void set(int i, int value) {arr[i] = value;} //Even though already pass by reference, this still poses a problem
        //Array may be modified.
};

void func(Haha var) {
    ...
}

int main() {
    Haha obj;
    func(obj); //Is this a good idea???
    
    //bad because this is pass by value, thus you copy 
    //the content of the array. (too large)
    
    //Better to pass by reference:
    //void func(Haha& var);
    
    //void func(const Haha& var); <-- Do not allow changing.
    
    return 0;
}
```

Rule of thumb:
- If you want to pass a big object, use **PBR**
- If you **don't** want the function to modify something, put a `const`

If function has a `const` reference parameter, both const and non-const parameter
can be accepted.

Example:
```cpp
void cbr(Large_Obj& LO) {cout<<LO.height;}
void cbcr(const Large_Obj& LO) {cout<<LO.height;}

int main() {
    Large_Obj dinosaur(50);
    const Large_Obj dinosaur(100);
    // Which gives error
    cbr(dinosaur); //OK
    cbcr(dinosaur); //OK
    cbr(rocket); //NO
    cbcr(rocket); //OK
}
```

Difference betwwen pointer and reference:
1. _Pointer_ can point to **nothing** (NULL), but _reference_ is **always bound**
to an object (pointer can be made uninitialized, but _reference_ has to be initialized)
2. _Pointer_ can point to different objects at different times. _Reference_ is only 
bound to **one** object.
    > Question raised: What about when you PBR you assign different reference to different objects. Difference, when you PBR, at the end of function call, the name it was assigned to is **freed** thus allowing for a new object to be bound
3. Name of *pointer* refers to the **pointer object**, *reference* always refers to **the object itself**

## Object Initialization, Construction, and Destruction.

Data members are `public`, can be initialized with the brace {} initializer.

Ex: `int main() {Word movie = {1, "Titanic"};} //Word has two public variables` 

However only available if all members are `public` if any data members
is `private`, cannot use this method.

Standard approach to initializing : using **constructors**

####Constructors:
Default constructors: a constructor that can be called with **no** arguments
Meaning that you don't need to pass anything to the constructor.

>Desmond's definition: If you call the constructor without passing anything to it, it is still happy

Making a private constructor, possible?
Answer: Yes. Purpose? If you want the constructor to be called only in member functions.

If **no** user defined constructor exists, the compiler will generate a default constructor
for it `X:X(){}`.

Conversion constructors: Accepts a single argument, which specifies a conversion from its
argument type to the type of its class.

```
class A{
    private:
        int a;
        int b;
        int c;
    public:
        A(int u, int v=2, int w = 3) {
            a=u;
            b=v;
            c=w;
        }
};

int main() {
    A obj(1); //Conversion constructor -> explicit
    A objHaha = 10; //IMPLICIT conversion constructor, NOT an assignment!!
    ...
}
```


