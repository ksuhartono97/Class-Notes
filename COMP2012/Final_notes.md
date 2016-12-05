#Final Review Notes

##Syllabus

Coverage of the final examination is as follows:

- Data Abstraction and Classes
- Const-ness
- Object Initialization, Construction and Destruction (including Member Initialization List)
- Generic Programming (Function / Class Templates, Operator Overloading, Friend Function / Class)
- Static Data and Methods
- Standard Template Library (Containers, Iterators and Algorithms)
- Namespace
- Inheritance, Polymorphism and Dynamic Binding (including Abstract Base Class)
- Abstract Data Types
- Binary Trees, Binary Search Trees, AVL Trees
- Hashing

##Data-abstraction and Classes

##Const-ness
Safety net, if a object shouldn't change make it `const`

`const` member functions cannot modify the class object (and its data members)

Syntax:
```cpp
int getA() const {};
```
As in put the `const` keyword after the parameter list.

`const` and `const` pointers:

Rule of thumb to this:
- `const` to the left of the `*` refers to the **object**
- `const` to the right of the `*` refers to the **pointer** 
 
>Pointer-to-const pointing to a non-const object 
>doesn't make the object itself become const

`const` function arguments:
- To prevent accidental modifications
- So that you can pass both const and non-const objects to a function that requires
`const` arguments. (if you remove the `const` it won't be able to receive `const` objects)

##Constructors Destructors
Types of Constructors:
- Default constructor: will be given by C++ if there are no other constructors
- Conversion constructor
- Copy constructor: only has exactly one argument, another object
of the same class. If it doesn't exist, default will be given by C++ that does
memberwise copying. (shallow copy)

`explicit` to prevent implicit conversion constructor calls.

Local variables are created on the **runtime stack**

Dynamic variables are created on the **heap**

Anything in the runtime stack will be destructed when the function/block
it is in terminates. However any dynamic variables in the heap needs to be
deallocated **manually** by the user. By using `delete`. If it is not
deleted then that dynamically allocated variable will remain in the heap,
resulting in a memory leak.

Such a thing is called **garbage**. 

Destructor: **no** arguments, **no return type**, can only be **one** destructor

Constructor: **can have** arguments, **no return type**, can have **multiple** constructors
 
When an object is constructed, all its **data members** are constructed
first in the order in which they appear in the class!

Member initialization list
```cpp
X::X() : a(b), c(d){];
```


##Generic Programming

###Function and Class Templates
Similar to standard function and class definitions, but the types
of objects they manipulate are parameterized with **type variables**.

Syntax:
```cpp
template <typename T> //Same as template <class T>
T my_max(const T& a, const T& b) {
    return (a > b) ? a : b
}
```

Note, defining a template does not mean the object or class has been created. This is **not an actual
function or class**. Needs to be used before actually generating any objects.

Also, writing `template<typename ...>` needs to be done for every single function you make,
if you don't do it for the function, you will get an error.

When you instantiate a template, it tries to determine the type `T` from the **arguments** of the
function call.

If you call the template with different types, you will get **different functions**, and the size of the 
program .exe will increase accordingly.

No automatic type conversion for template arguments.

Explicit instantiation of the template function

```cpp
cout << my_max<double>(4, 5.5);
```
Done to specify what is supposed to be T

A template can take more than 1 argument, e.g.:

```cpp
template <typename T1, typename T2>
T1 max (const T1& a, const T2& b) {return (a>b) ? a : b;}
```

A template function **must have a parameter** because the compiler
determines the type for T from the parameter. Without the parameters there
will be an error. Cannot determine from just the function calls.

Template is also available for classes

Syntax:
```cpp
template <typename T>
class A {
    public:
        A(T& data) : _data(data) {}
        
    T _data;
};
```

Within the template, <T> for anything in the class can be omitted. As can be
seen in the example. We do not have to put `A<T>` but if we want to
we can do it.

However if you declare the template say in the `.h` file and then
have the definition in the `.cpp` file, we **must** put both `template typename<T>`
and the `A<T>`.

>Extra, you can have a template class `.h` file do `#include ".cpp"` file so that
>we can separate the implementation in `.h` from the one in `.cpp`. 

###Operator Overloading
Operators that cannot be overloaded:
- .  the dot operator
- :: the scope operator
- ?: the ternary operator or the conditional operator
- .* access pointer
- sizeof

Also, you cannot change these properties of an operator
- Arity : number of arguments it accepts
- Associativity : e.g. : a + b + c is equivalent to (a + b) + c
- Precedence

Operator overloading is only allowed for user defined datatypes, not allowed
for native datatypes.

Two ways to do operator overloading
- As a global function
- As a member function

Global operator functions are called as global functions:

Ex:
```cpp
a + b //operator+(a,b);
a - b //operator-(a,b);
```

While member operator functions use the dot syntax to be called:

Ex:
```cpp
a + b //a.operator+(b);
a - b //a.operator-(b);
```
Meaning that it will only accept one operand instead of the usual two
operands for operator functions, because the first operand is implicitly
the object that it was invoked on.

For member operator functions, it is imperative that the class object
must be the **left operand**

In the example, `a` must be the object with the overloaded operator defined.
If not then there will be an error.

Solutions to this:
- Create a global non-member function operator+ for handling if the left side
of the operand is not an object.
- Or make that same non-member overload operator to accept two objects of the same type
resulting in the conversion to another datatype if needed.

You can only use **either one** of the possible methods for overloading
an operator. Defining both is an error!

If the left operand must be an object of another class,
it must be defined as a member function.

###Friend functions
Grant a global function or another class as its friends.

Not considered member functions

Member access qualifiers are irrelevant, they can access all data members

Notes:
- Friendship is not **symmetric**, e.g.: A is B's friend does not imply that
B is A's friend
- Friendship is not **transitive**, e.g.: A is B's friend, and B is C's friend
but it doesn't imply A is C's friend.
- Friendship is not **inherited**, friends of a base class do not become
the friends of its derived classes automatically

##Static Data and Methods
Static class data members are actually global variables specified by the
keyword `static` under the **scope** of a class

Only one copy exists and is shared by all the objects of the class.

Static variables exist even when no objects of the class are defined.

Static variables cannot be initialized in the class definition(except
for const static variables). Must be defined outside
the class definition, usually in the .cpp file of that class.

Static data / methods are also called class data / methods.

Static methods can be called in two ways:
- Globally, using the scope operator `::` 
- Like a member function of the class using the `.` operator

Some notes on static methods:
- Do not have the implicit `this`
- May be used even when there is **no** objects of the class
- Can only use the **static** data members of the class
- Cannot be `const` or `virtual` functions.

##STL
3 Main Components of STL:
- Containers : carry/store objects
- Iterators : works like pointers, for iterating through containers
- Algorithms : self explanatory, duh :p

###Containers
3 concepts of a container:
- Kind of the container
- Kind of objects stored
- Kind of operations

###Iterators

###Algorithms

####Function pointers
```cpp
int (*)(const void*, const void*);
```
Function name to be put after `*` in brackets, so `(*compare)` like that

####Function Objects
Function objects = functoid = functor.

Must have an operator() overloaded. May have **other** member functions, not just
the overloaded operator.

Can have data members so can store internal states, meaning that it is stronger
than function pointers that do not have data members.

>Predicate: function object that returns a boolean 

##Namespace
With the `namespace` keyword we are able to define regions in a program. Such
that if there are functions or variables with same names, the compiler will be able
to recognize a difference and will not report an error.

`using` to use a specific namespace so that you don't have to keep putting 
`namespace::` behind everything.

Using namespaces can create the ambiguity problem, that is if two instances of something
exist and both namespaces are used. Then the compiler cannot decide which one to use.

```cpp
... //includes and etc here
namespace ms = microsoft;
using namespace apple; //both namespace owns a stack
using namespace ms;

int main() {
    Some_Class sc;
    Other_Class oc;

    Stack S;    //Error : ambiguous, same name exists in both namespaces
    ms::Stack ms_stack;     // OK
    apple::Stack apple_stack;   //OK

    return 0;
}
```

Namespace in another namespace : nested namespace, allowed

Global namespace: for functions and variables defined globally

Explicit use of `using` declaration :
```cpp
using std::vector
using std::cout
using std::endl
using std::find
```

Reason for doing explicit `using` declaration :
- Readibility
- Performance, helps compiler find functions, no need to search through whole namespace


##Inheritance, Polymorphism, Dynamic Binding

##ADT

##Trees

##Hashing