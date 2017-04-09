# Final Review Notes

## Syllabus

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

## Data-abstraction and Classes

## Const-ness

Safety net, if a object shouldn't change make it `const`

`const` member functions cannot modify the class object (and its data members)

Syntax:

```c++
int getA() const {};
```

As in put the `const` keyword after the parameter list.

`const` and `const` pointers:

Rule of thumb to this:

- `const` to the left of the `*` refers to the **object**
- `const` to the right of the `*` refers to the **pointer**

> Pointer-to-const pointing to a non-const object doesn't make the object itself become const

`const` function arguments:

- To prevent accidental modifications
- So that you can pass both const and non-const objects to a function that requires `const` arguments. (if you remove the `const` it won't be able to receive `const` objects)

## Constructors Destructors

Types of Constructors:

- Default constructor: will be given by C++ if there are no other constructors
- Conversion constructor
- Copy constructor: only has exactly one argument, another object of the same class. If it doesn't exist, default will be given by C++ that does memberwise copying. (shallow copy)

`explicit` to prevent implicit conversion constructor calls.

Local variables are created on the **runtime stack**

Dynamic variables are created on the **heap**

Anything in the runtime stack will be destructed when the function/block it is in terminates. However any dynamic variables in the heap needs to be deallocated **manually** by the user. By using `delete`. If it is not deleted then that dynamically allocated variable will remain in the heap, resulting in a memory leak.

Such a thing is called **garbage**.

Destructor: **no** arguments, **no return type**, can only be **one** destructor

Constructor: **can have** arguments, **no return type**, can have **multiple** constructors

When an object is constructed, all its **data members** are constructed first in the order in which they appear in the class!

Member initialization list

```c++
X::X() : a(b), c(d){};
```

## Generic Programming

### Function and Class Templates

Similar to standard function and class definitions, but the types of objects they manipulate are parameterized with **type variables**.

Syntax:

```c++
template <typename T> //Same as template <class T>
T my_max(const T& a, const T& b) {
    return (a > b) ? a : b
}
```

Note, defining a template does not mean the object or class has been created. This is **not an actual function or class**. Needs to be used before actually generating any objects.

Also, writing `template<typename ...>` needs to be done for every single function you make, if you don't do it for the function, you will get an error.

When you instantiate a template, it tries to determine the type `T` from the **arguments** of the function call.

If you call the template with different types, you will get **different functions**, and the size of the program .exe will increase accordingly.

No automatic type conversion for template arguments.

Explicit instantiation of the template function

```c++
cout << my_max<double>(4, 5.5);
```

Done to specify what is supposed to be T

A template can take more than 1 argument, e.g.:

```c++
template <typename T1, typename T2>
T1 max (const T1& a, const T2& b) {return (a>b) ? a : b;}
```

A template function **must have a parameter** because the compiler determines the type for T from the parameter. Without the parameters there will be an error. Cannot determine from just the function calls.

Template is also available for classes

Syntax:

```c++
template <typename T>
class A {
    public:
        A(T& data) : _data(data) {}

    T _data;
};
```

Within the template,

<t> for anything in the class can be omitted. As can be
seen in the example. We do not have to put <code>A&lt;T&gt;</code> but if we want to
we can do it.</t>

However if you declare the template say in the `.h` file and then have the definition in the `.cpp` file, we **must** put both `template typename<T>` and the `A<T>`.

> Extra, you can have a template class `.h` file do `#include ".cpp"` file so that we can separate the implementation in `.h` from the one in `.cpp`.

### Operator Overloading

Operators that cannot be overloaded:

- . the dot operator
- :: the scope operator
- ?: the ternary operator or the conditional operator
- .* access pointer
- sizeof

Also, you cannot change these properties of an operator

- Arity : number of arguments it accepts
- Associativity : e.g. : a + b + c is equivalent to (a + b) + c
- Precedence

Operator overloading is only allowed for user defined datatypes, not allowed for native datatypes.

Two ways to do operator overloading

- As a global function
- As a member function

Global operator functions are called as global functions:

Ex:

```c++
a + b //operator+(a,b);
a - b //operator-(a,b);
```

While member operator functions use the dot syntax to be called:

Ex:

```c++
a + b //a.operator+(b);
a - b //a.operator-(b);
```

Meaning that it will only accept one operand instead of the usual two operands for operator functions, because the first operand is implicitly the object that it was invoked on.

For member operator functions, it is imperative that the class object must be the **left operand**

In the example, `a` must be the object with the overloaded operator defined. If not then there will be an error.

Solutions to this:

- Create a global non-member function operator+ for handling if the left side of the operand is not an object.
- Or make that same non-member overload operator to accept two objects of the same type resulting in the conversion to another datatype if needed.

You can only use **either one** of the possible methods for overloading an operator. Defining both is an error!

If the left operand must be an object of another class, it must be defined as a member function.

### Friend functions

Grant a global function or another class as its friends.

Not considered member functions

Member access qualifiers are irrelevant, they can access all data members

Notes:

- Friendship is not **symmetric**, e.g.: A is B's friend does not imply that B is A's friend
- Friendship is not **transitive**, e.g.: A is B's friend, and B is C's friend but it doesn't imply A is C's friend.
- Friendship is not **inherited**, friends of a base class do not become the friends of its derived classes automatically

## Static Data and Methods

Static class data members are actually global variables specified by the keyword `static` under the **scope** of a class

Only one copy exists and is shared by all the objects of the class.

Static variables exist even when no objects of the class are defined.

Static variables cannot be initialized in the class definition(except for const static variables). Must be defined outside the class definition, usually in the .cpp file of that class.

Static data / methods are also called class data / methods.

Static methods can be called in two ways:

- Globally, using the scope operator `::`
- Like a member function of the class using the `.` operator

Some notes on static methods:

- Do not have the implicit `this`
- May be used even when there is **no** objects of the class
- Can only use the **static** data members of the class
- Cannot be `const` or `virtual` functions.

## STL

3 Main Components of STL:

- Containers : carry/store objects
- Iterators : works like pointers, for iterating through containers
- Algorithms : self explanatory, duh :p

### Containers

3 concepts of a container:

- Kind of the container
- Kind of objects stored
- Kind of operations

### Iterators

Iterators are generalized pointers.

For each kind of STL sequence, there is an iterator type:

```c++
list<int>::iterator
vector<string>::iterator
deque<double>::iterator
```

Inside the `<>` is the type of whatever we store in the array.

E.g. :

```c++
vector<double> vv;
//Input values here
vector<double>::iterator it;
it = vv.begin();
vector<double>::iterator itit;
itit = vv.end();

for(vector<double>::iterator haha = it; haha != itit; haha++) {
...
}
```

Using `typedef` to rename an iterator:

```c++
int main() {
    vector<int> a;
    vector<int>::iterator it;
}
//Long right, so:
typedef vector<int>::iterator intIterator;
typedef vector<int> an;

int main() {
    an a;
    intIterator it;
}
```

### Algorithms

#### Function pointers

```c++
int (*) (const void* , const void*);
```

Function name to be put after `*` in brackets, so `(*compare)` like that

#### Function Objects

Function objects = functoid = functor.

Must have an operator() overloaded. May have **other** member functions, not just the overloaded operator.

Can have data members so can store internal states, meaning that it is stronger than function pointers that do not have data members.

> Predicate: function object that returns a boolean

## Namespace

With the `namespace` keyword we are able to define regions in a program. Such that if there are functions or variables with same names, the compiler will be able to recognize a difference and will not report an error.

`using` to use a specific namespace so that you don't have to keep putting `namespace::` behind everything.

Using namespaces can create the ambiguity problem, that is if two instances of something exist and both namespaces are used. Then the compiler cannot decide which one to use.

```c++
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

```c++
using std::vector
using std::cout
using std::endl
using std::find
```

Reason for doing explicit `using` declaration :

- Readibility
- Performance, helps compiler find functions, no need to search through whole namespace

## Inheritance, Polymorphism, Dynamic Binding

### Inheritance

Finding common data members of classes and putting it into a parent class, then make the new classes inherit from the parent class.

Parent class called base class, children called derived class.

New members and functions are added to the derived class.

Inheritance implements an **is-a** relationship as in the derived class is a base class. This is shown in the Polymorphic Substitution Principle or Liskov Substitution Principle.

#### Polymorphic Substitution Principle

If there is a function that accepts base class object, you can pass a base class type object and the derived class object to it.

Example of this:

```c++
UPerson up;
Student stu;

UPerson* upointer  = &up; //OK, normal usage
UPerson* upointer = $stu; //Also OK, because of Liskov

Student& hehe = up; //NOT OK

UPerson uobj = stu; //OK, because of Liskov, however this is a bit weird, because of slicing
```

Indirect inheritance: when a class inherits from a derived class, meaning that it is indirectly inheriting from the base class.

Initialization of inherited classes, through member initialization list, using a call to the constructor of its parent class. As in inherited data members must be initialized with the constructor of the parent class. Derived class's data members can still be initialized with it's own constructor.

Order of construction:

- Base Class
- Data Members
- Derived Class

Order of destruction:

- Derived Class
- Data Members
- Base Class

As always, order of construction persists, data member first (in order of definition) then the class itself.

#### Slicing

Slicing happens due to assignment from derived class object to a base class object. Resulting in the loss of all elements that the derived class has. Including the member functions!

Happens even when assigned by **reference** and by **pointer**!

Note, if you use `virtual` on the members, and then do assignment by either reference or pointer, then the member function from the derived class will be preserved. As in you are still able to use the derived class specific implementations of the virtual member functions. But still lose anything owned by the derived class.

> Constructors and Destructors are **never** inherited

#### Access Control Public, Private, Protected

3 levels of access control:

- `public` : can be accessed by:

  - Member functions of the class
  - Any member functions of other classes
  - Globally

- `protected` : can be accesed by:

  - Member functions and friends of the class
  - Member functions and friends of the derived classes

- `private` : can be accessed by:

  - Member functions and friends of the class

#### Public, Protected, and Private Inheritance:

`public`: access level control stays as it originally was.

`protected`: `public` **becomes** `protected`, the rest stays the same

`private` : **Everything** becomes `private`

Protected and Private Inheritance disallows slicing, because it disables the Liskov Substitution Principle!

Assignment that results in slicing is only possible using `public` inheritance.

### Polymorphism & Dynamic Binding

Static Binding: The object type is what is displayed in the code during compilation

**Dynamic Binding:**

Supported through the use of `virtual` functions.

The actual method called is selected through the actual data type of the object, but only if the object is passed by reference or pointer.

Static binding means that which function that is called is determined during compilation.

Dynamic binding means that which function that is called is determined during runtime.

> Possible object types **do not** need to be known during compile time.

> Note: Refer to the note on slicing, that is due to dynamic binding.

#### Virtual Methods

Declared by putting `virtual` in the **class definition** not the method implementation. (Put in front of the method name).

Method `virtual` in base class means that it is also `virtual` in all the derived classes, even if there is no `virtual` tag.

A little bit slower in performance.

#### Polymorphism

We can work with objects without knowing their actual type during compile time.

As in the object used can take multiple forms (due to Liskov)

Must use pointers or reference.

#### RTTI (Run Time Type Information)

`typeid` to check the type of something during runtime.

Usage:

```c++
#include<typeinfo>

int main() {
    UPerson* u = new Student;
    cout<<typeid(*u).name();
}
```

This function expects an object to be passed to it. Will return another object, need to use `.name()` to get the name of the class.

#### Function overriding

Derived class defining a function with the same name as a function in the base class

Made possible through the use of `virtual`

> Overriding **not** possible without using `virtual`

Overriding is specializing the behaviour, not changing the semantics!! As in not changing the way it works.

The decision on which class's member function to use is done during **run-time** not during compilation.

Virtual destructors are a strong hint that the class is a base class.

Do not use virtual functions in constructors! Because the object itself hasn't even been created yet, how can you use the functions?

#### Abstract Base Class

Giving a class a **pure virtual function** makes the class an Abstract Base Class.

Example of a pure virtual function:

```c++
virtual double compute_net_worth() const = 0;
```

Basically add an `=0` in the end.

Properties of an Abstract Base Class:

- Cannot be instantiated
- Its derived class must implement the pure virtual function, or they automatically become an abstract base class also.

A pure virtual function basically means that this class doesn't have an implementation for this function yet. Meaning you want to delay making the implementation for this function.

That also means that you cannot create any objects of this class. Because the class itself is not complete!!

Calling a pure virtual function from an ABC is **undefined**.

Abstract base classes cannot be used as:

- Function argument PBV
- Return type for a function that returns by value
- Type of an explicit conversion

## ADT

An abstraction of data structures and is defined by its **behaviour** from the user's perspective and is independent of implementation.

### Stack and Queue ADT

Allows adding and removal only at the ends of the container

Stack : LIFO

Queue: FIFO

### List ADT

Can be implemented with arrays or singly linked lists

With Arrays:

- Fast element access
- Slow in deleting and inserting in the middle
- Require size to be known

With SLL:

- Dynamic size
- Slow element access
- Efficient insertion and deletion

Linked list destructor: Recursive call by creating a smaller sized linked list

Happens in the destructor:

```c++
if(head == 0) return; //Termination condition
{
 LINKED_LIST REMAINING_NODES(head->next);
}  //Recursively create smaller linked lists

delete head; //delete curr node.

head = 0; //Null pointer
```

### Doubly linked list

Similar to a singly linked list, difference is that this has a pointer pointing to the previous node.

Insertion in DLL:

- Step 1 : Create new node
- Step 2 : Find the node before which the new node is to be added

  - Head
  - Somewhere in the list
  - End

- Step 3: Insert the new node between the found node and its previous node

Deletion in DLL:

- Step 1 : Find the item to be deleted
- Step 2 : Bypass the item

  - Special case: item is the head
  - Special case: last item

- Step 3 : Free memory of deleted item

## Trees

A collection of nodes connected by edges

Root : the only node with no parents

Parent and child:

- Every node except root has exactly 1 parent
- Can have zero or more children

Leaves: nodes with no children

Siblings: nodes with same parent

Path: a sequence of nodes to get from one node to another

Length of a path: number of nodes in the path (note they must be connected)

Depth: Root to a node, how many edges do you pass through

Height: Length of the longest path from a node to a leaf. All leaves have a height of 0.

Height of a tree:

- Height of the root
- Depth of the deepest leaf

### Binary Trees

A tree in which no node can have more than two children.

A well balanced tree with N nodes has a height order of log N

A balanced binary tree has roughly an equal amount of nodes in its subtrees.

Traversal orders:

- Inorder: LCR (infix notation)
- Preorder: CLR (prefix notation)
- Postorder: LRC (postfix notation)

The inorder prints out a result that is in order! Preorder and postorder prints out in a weird order for humans but maybe easier to understand for computers.

Example, the postfix notation (from postorder) is commonly used to evaluate math operations with a stack. Also known as RPN (Reverse Polish Notation)

Infix to postfix conversion:

- Step 1: Initialize an empty stack
- Step 2: while no errors and not end of expression:

  - read the next token
  - in case of:

    - operand : display
    - ( : push to stack
    - ) pop until ( but don't display (, the ( is also popped
    - operator:

      - if higher precedence than stack top, push the operator
      - pop stack, print, then compare again to the next operator in stack

- Step 3: Pop all operators in the stack and display

RPN Expression evaluation:

- Scan expression from left to right to find an operator
- If operator found, pop two operands and evaluate with operator, push back result
- When finish with everything, last remaining operand is result

### Binary Search Trees

BST Property for every node x:

- All values in the left subtree is smaller than the value in x
- All values in the right subtree is larger than the value in x

May not be unique for the same set of data.

Minimum element is always left most node

Maximum element is always right most node

Insertion algorithm:

- Proceed down the tree as you do with search
- If found, do nothing (or something, depends on what you want)
- If reached end, insert node at the last spot

Deletion:

- If leaf: delete immediately
- If have one child: make grandfather point to child(bypass)
- If have two child: replace the deleted node with maximum node in its left sub tree, or the minimum node in the right sub tree. Then remove the chosen node.

### AVL Trees

Binary Search Trees can become unbalanced due to insertion and deletion of nodes. Therefore there is a need for an algorithm that can rebalance the trees.

AVL Trees are self-balancing binary search trees, where at most the heights of the two child subtrees differ at most by one. Each node stores a height value, which refers to the height of the node.

If at any moment the height difference differ by more than one, rebalancing is done to fix this problem. (Usually happens due to insertion or deletion)

Efficiency of any operation on an AVL tree always has **order of logn**.

Rotation: operation to make a tree balanced. Types of rotation:

- Single rotation
- Double rotation

Rebalancing done by **left** or **right** rotation. Or a combination of the two (left-right or right-left)

Problematic node is the node that has a height difference of > 1 for its subtrees

Problem causing node is the source of the problem (usually the inserted or deleted node) and is useful to judge what type of rotation should we use.

For single rotation, always perform the rotation on the problematic node

If there are more than one problematic node, always fix the bottom problematic node first.

You should perform first rotation on the node **directly under** the problematic node! And the second rotation **on the** problematic node directly!

## Hashing

Hash table: array of fixed size, containing all data

Key is a something that is needed to determine the location to be used (compute the location of your data). A key should be unique.

Hash function is the formula to determine which location of the hash table to use for certain data.

These operations are not supported in a hash table:

- find_min and find_max
- Finding successor and predecessor
- Reporting data in a certain range
- Listing out the data in order.

Hash function design that is most typical : **h(k) = k mod m**

Value of m should be a prime number and not too close to exact powers of 2, and shouldn't be a power of 10. Should also consider amount of data in hash table, don't be too small or too big.

### Dealing with string keys:

#### Method 1

Add up the ASCII values of the characters in the string.

Is not a nice method because ASCII values add up to a large number.

It is nicer to just assign integer values to the alphabets. As in 1 to A and 26 to z, then simply add up the values together.

Most hash functions assume that keys are **natural numbers**, so if the keys aren't natural numbers, have to find a way to interpret them as **natural numbers**.

Problem with this problem, keys do not distribute well

#### Method 2

Use the first 3 letters in the word.

h(key) = (key[0] + 27 _key[1] + 27^2_key[2]) mod m

where m is hash table size

It can have a reasonably equitable distribution if the first 3 characters are random.

However, letters in an English word are not random, making most of the table empty.

In example, if we use m = 10,007 then only at most 28% of the table can actually be hashed.

#### Method 3

Use all the characters in the word.

Hash function involves all characters in the key and the hash values are expected to distribute well.

### Collision Handling

#### Separate Chaining

Keys having the same hash values are chained on separate linked lists. So the hash table is a table of linked lists.

So basically ignore the collisions.

New node is always put before the head of the linked list. (insertion is done on the head).

Problem with this is there can be one single long linked list in the table, and the others are short. This implies that the hash function is bad.

So inserting a key to k:

- Compute h(k) this is the index of the item
- If T[index] is empty, then init to a linked list and store the value
- If T[index] is not empty, then insert before the head (beginning of the list)

To delete a key k:

- Compute h(k) to again find the index
- Search for the key k in that entry in the table
- Delete the item with key k if it is found

Constant time for separate chaining operations (Search, insertion and deletion)

Also means that if the hash function is nice, then there will be little to no collisions of data in the hash table.

Disadvantage: slow, because of linked lists

Advantage: deleting is easy.

Separate chaining means keeping all the values by making a linked list (to solve collision)

#### Open Adressing

Entry we want to use is occupied, then find another within the hash table (to solve collision)

Three common methods for resolving collisions in open adressing:

- Linear probing
- Quadratic probing
- Double hashing

Difference in method of finding another entry.

##### Linear Probing

If entry is occupied, keep moving downwards until we find an empty entry.

> Hash table, generally speaking, you don't remove data. If you remove value, you just put markers to show that this is gone already.

Total number of collisions in example in slides: 7

##### Quadratic probing

Use the same hash function as linear probing, but when collision is encountered, then you move downward in a quadratic manner.

So:

- 1st collision move down 1 location
- 2nd collision move back to start, move down 4 location
- 3rd collision move back to start, move down 9 location
- 4th collision move back to start, move down 16 location

And so on, so basically other than the 1st collision just move down by n^2 but don't forget to **go back to starting pos**.

Using the same example, the number of collisions is lower.

This is better than linear probing because in linear probing you only move down by one step. Meaning that everytime there is a collision there is going to be a cluster of data that forms. Causing the data to bunch up somewhere causing a lot of collisions.

Quadratic probing is better because you jump further the more collisions you get.

Still has the competing for same location problem, also jump amount is also the same (1, 4, 9, 16, ...) (so can still collision)

##### Double Hashing

So for each collision and each value the jump value will be calculated with a hash function again. Resulting in different jump values per jump steps. Meaning that it is less likely for the collision to happen again.

So there will be 2 hash functions.

Only have 2 collisions with same example in lecture notes.

> Using linear problem will result in the primary cluster problem. Which is you move down constantly till you find an empty cell but it is a huge cell.

Criteria for 2nd hash function:

- Second hash function should never give 0 value.
- For any key k, hash2(k) must be relatively prime to the table size m, a solution is to make the m prime and then R be a prime number that is smaller than m.

> Relatively prime: the only common factor of the two numbers is 1

Deletion in Open Adressing:

Cannot be actually performed otherwise the probing sequence will be broken. You do deleting by marking it with a symbol.

### Re-Hashing

Re-hashing is based on the percentage of usage in the hash table, if the percentage (alpha) is too big, then we double the table size, and rehash all data items with a new hash function.

This percentage is called load factor.

> Load factor only affects Open Adressing, not important for Separate Chaining

Note: this operation is very expensive on the computer, but must be done when space is running low.

Reason why we double the size is because we don't want to do rehashing soon.
