#Continuing on STL

###Iterators: 
Iterators are **generalized** pointers. Not exactly the same, but
its behaviour will be more or less the same. As in what we can do on pointers,
we can also do on iterators.

Why are they important? For scanning through the contents of a container.

For each kind of STL sequence, there is an iterator type:
- `list<int>::iterator`
- `vector<string>::iterator`
- `deque<double>::iterator`

More or less the same for most containers, only need to modify
the name of the container. Several containers have different syntax.

Inside the `<>` is the type of whatever we store in the array.

E.g. :
```cpp
vector<double> vv;
//Input values here
vector<double>::iterator it;
it = vv.begin();
vector<double>::iterator itit;
itit = vv.end();

for(vector<double>::iterator haha = it; haha != itit; haha++) {

}
```

Better practice: (credits: _Kenta Iwasaki_)
```cpp
vector<double>::const_iterator it = vv.begin();

for (vector<double>::const_iterator it = vv.begin(); it != vv.end(); it++) {
    // Function body.
}
```

>Can also do `vector<double>.const_iterator it`

What is iterator itself? A static class. 

`typedef` to rename something basically.

```cpp
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

###Algorithms

Predicate: boolean function. So when u need to pass a Predicate to the function
it means that you have to pass a function that returns a bool output to the function. (passing function to a function)

```cpp
//Predicate example:
bool coolcool(int v) {
    return v < 15;
}

//How to use?
int main() {   
    vector<int> temp;
    temp.push_back(42);
    temp.push_back(20);
    temp.push_back(10);
    
    vector<int>::iterator p = find_if(temp.begin(), temp.end(), coolcool);
}
```

```cpp
class GreaterThanBTester {
    private:
        int a;
    public:
        GreaterThanBTester(int a) : a(a) {}
        bool operator()(int b) {return a > b;}
}
```

In the `find()` function, it will always only return the first element it finds.
Same case for the `find_if()`. So if you need to find more than one, you always have to do
a `for` loop. 

`void*` is a pointer to any type.

e.g.:
```cpp
int a = 10;
double* b = &a; //CANNOT
void* b = &a; //Can
```

Function pointer:

Pointer that points to a function.

```cpp
int myMax(int a, int b) {
    return (a > b) ? a : b;
}

int main() {
    //We want to define a pointer that points to myMax!
    int (*haha) (int a, int b);
    haha = myMax;
    
    int max = haha(1,2);
}
```

