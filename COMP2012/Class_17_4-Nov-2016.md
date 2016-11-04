#Continuing on STL

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
and the `A<T>` for **every** function that exists.

Also, if it only has the template file implementations, we can
replace the `.cpp` file with the `.tpp` file.

>Extra, you can have a template class `.h` file do `#include ".cpp"` file so that
>we can separate the implementation in `.h` from the one in `.cpp`. 

If you have a member function that will be implemented as a friend function
inside a template class, you need to put another `template <typename>`

E.g.:
```cpp
template <typename T>
class A {
    public:
        template <typename S>
        friend ostream& operator<< (ostream& os, const A&<S> obj) {
        ...
        }
}
```

However if you define that kind of friend function in a separate file, it 
is fine to use the same typename.

Important: in the case above. The `<S>` next to the `const A&`
must be there, it cannot be omitted.

Containers in STL:
- Sequence Containers: examples : arrays
    - Represent linear data structures
    - Start from index/location 0
- Associative containers :
    - Non-sequential containers
    - Store key/value pairs: We store data as a pair, not standalone data, example 
    `1: desmond`
- Container adapters
- "Near-containers" C-like pointer-based arrays

###Sequence Containers
Deque : Double-ended queue

Basically works like a circular linked list, faster than a vector. 

List is like a doubly linked list.

Vectors basically work as a dynamic array, although not as inefficient
as a dynamic array.

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> goodGrade;
    goodGrade.push_back(100);
    goodGrade.push_back(99);
    goodGrade.push_back(101);
    
    int* p = &(goodGrade[0]);
    //Shouldn't be done, you should use an iterator!
    
    vector<int>::iterator it = goodGrade.begin(); 
    //Gives something like the address of the first element of the vector
    //Note, not the actual address!
    *it = 200;
    vector<int>::iterator itMore = goodGrade.end();
    *itMore = 400;
    //THIS IS NOT ALLOWED
    //end is at the end, say the vector is size 10,
    //end will be at 10, not 9, so it is out of bounds
    
    for(vector<int>::iterator it = goodGrade.begin(); it != goodGrade.end(); it++) {
        cout<<*it<<endl;
    }
    //for looping through
}
```

