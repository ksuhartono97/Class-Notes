#STL (Standard Template Library) for Generic Programming

###Reviews:
Generic programming: programming with **types** as parameters

>Template defined does not mean that the object is defined, template needs
> to be used for object to be defined.

Syntax:
`Template <typename T>` 

Ternary operator `?:` also known as conditional operator. Takes
three arguments, unlike most operators that only take two.

When we implement a function template, and in that function template
we use certain operators, we should ensure that in any of our class
definitions that might use this function, that class must support said operator.

###Introduction to STL:

3 Main Components in STL:
- Containers : used to carry elements / objects. Ex: Linked Lists, 
trees
- Iterators : more or less the same as pointers, can do dereference, pre or post increments, etc
- Algorithms : sorting, max, min

####Container
A class that can carry collections of objects.

Arrays are very inefficient as in if the size of the data is larger
than the size of the array, we cannot simply resize the array. Even if
we use a dynamic array, we have to create a new array and copy everything.
Which is very inefficient. However access speed is very fast.

Meanwhile linked lists, have slower access speed, because we have to iterate through
the list. However it is more efficient as its size can be expanded or shrunk according to need
with relative ease.

3 Concepts about containers
- The kind of **container** : is it a linked list? or an array?
- The kind of **objects** stored in the container: the datatypes in it
- The kind of **operations** on the elements in the container : 
the functions we can use to manipulate the elements.

STL Containers:
- A class that holds a collection of **homogenous** objects. All the objects
should be in the same datatype.
- Typical use of **class templates** : to support different datatypes

Example:
`vector` class in STL which is a flexible array.

How to use vector template:

```cpp
//Note this is not all the member functions, only some important ones
#include <vector> //To enable use
#include <iostream>
using namespace std;

int main() {
    vector<int> vec;
    vec.push_back(4); //Push to the back of the vector
    vec.push_back(5);
    vec.push_back(-10);
    //vec {4, 5, -10};
    
    for(int i=0; i<vec.size(); i++) {
        cout<<vec[i]<<endl;
    }
    
    return 0;
}
```

Return type may be flexible