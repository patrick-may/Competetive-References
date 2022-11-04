# C++ Reference

The most common language used for competetive programming. Fast, not a ton of boilerplate, and hack-ish.

If you are comfortable importing specific C++ libraries, import them individually. Even though it is bad form, I like to just include the following two lines in every c++ solution:
```cpp
#include <bits/stdc++.h> //the entire standard template library of c++
using namespace std;
```

Additionally, some people like to define macros to shorten the amount of keystrokes you have to type. Macros are created with
```cpp
#define [text used in code] [text to replace macro at compliation]
// commonly,
#define pb push_back //shorten vector operations

// you can also create aliases for existing types
typedef long long int ll; //for big ints, now you only have to type "ll"!
``` 
Feel free to add more robust descriptions here. This is about the highest amount of macro/namespacing/library management that really matters in competetive programming (in my opinion).

## I/O
C++ famously has weird input management. At a certain point, some would argue c-style collecting user input is faster (which I would generally agree with), but it is so miniscule that I do not think it matters if you are at the level of using this quick reference :). 
You can:
```cpp
//take in one known value of a known type
string inp;
int pc; //"Problem count" some problems start by saying, "there will be *pc* test cases"
cin >> inp; // gets the first string from input.
cin >> pc; //cin will automatically wrap to the next line for collecting input

//chaining cin
int x, y, z;
cin >> x >> y >> z; //will attempt to read 3 integers from standard input

//looping through i/o of known amount of entries
//commonly used for repeating multiple values on one line, or similar input on multiple lines
vector<int> my_vec(array_size)
for (size_t i = 0; i < my_vec.size(); ++i) {
    cin >> my_vec[i];
}

// looping through i/o until EOF
// some problems specify that 
int num;
while(cin >> num) {
    // if num is not EOF, input will write to num
    // do bulk processing here
}

// getting space separated strings
string input_line;
getline(cin, &input_line); // gets an entire line until "/n" character delimits.
``` 

When trying to perform output, you can:
```cpp
int soln = 1;
string other_soln = "you win";
vector<int> other_other_solns = ...;

cout << soln << '\n'; // print soln and go to newline
cout << other _soln << '\n'; // << operator works with many different types
for(int i: other_other_solns){
    cout << i << " "; // by default, cout does not flush the output line.
}

```

**Output formatting** can be accomplished through various hack-y ways, but some of the most common are detailed below:
```cpp
//outputting displaying a boolean value
cout << boolalpha << bool_variable_val;

//limiting width of any output
cout << setw(num_chars_in_width) << output_str << output_int ...

// limiting floating point precision
cout << setprecision(decimal_precision) << format_float << other_stuff ...
```

## Fundamental Datastructures
Below are the main built-in STL structures available, along with the most notable functions of each.

### Vectors
Vectors are dynamic arrays that are nice because they automatically resize when adding elements to them.
```cpp
//blank, empty vector
vector<Certain_Type> my_vec;

//you can nest other non-primitive types into a vector
vector<vector<int>> matrix; //common 2D array
vector<map<string, int>> array_of_frequencies;

size_t size_of_vec = my_vec.size(); //get number of elements in vector
my_vec.push_back("%Data Entry Here%"); // add element to vector
my_vec[0] += 1 // access elements by [] indexing, WILL ERROR IF INDEX Out-of-bounds
my_vec.insert(my_vec.begin() + 2, 54) // insert an element to a vector. First argument is iterator to location to insert 
my_vec.remove(my_vec.begin()) // removes the element at certain iterator. this removes first item

// Loop Through a vector:
for(size_t i = 0; i < my_vec.size(); ++i) {
    cout << my_vec[i] << " ";
}
// Do with a range thingy, feels kinda like python
for(int i: my_vec) {
    cout << i << " ";
}

//basic vector iterators:
my_vec.begin() // iterator to start of vector
my_vec.end() // iterator to END of vector, past all valid elements
my_vec.rbegin() // reverse begin iterator, i.e. last element
my_vec.rend() // reverse end iterator, i.e. first element
my_vec.back() // direct reference to the last element of a vector
my_vec.front() // direct reference to the front of a vector

//sorting a vector
// under the algorithms library:
sort(my_vec.begin(), my_vec.end()) //sorts elements in least-to-greatest order
sort(my_vec.begin(), my_vec.end(), my_sorting_func) // sorts elements based on the my_sorting_func, something we implement
```

### Deques
Deques are similar to vectors, with the main exception being that you can modify the front and back of the deque in constant time 
(vectors can only work on the end)

```cpp
deque<int> deck; //empty deque, can also initialize a certain size, repeat vals, etc

//main difference, and thus important to know:
deck.push_front(1);
int front_val = deck.front(); // same as saying deck[0]
deck.pop_front(); // pop front item from deck

```
Iterating through a deque is very similar to a vector.

### Stacks
Some problems require stacks. While they can be simulated using deques, you can also use the built in stack class

```cpp
stack<int> s; // empty constructor

// add elements to stack
s.push(24);

// get the top element of the stack
int top_val = s.top();

// remove the top element of the stack
s.pop();

// get size of the stack
s.size();
```
Not sure of a great way to traverse a stack with a loop aside from popping through it. You can hack something together -- but that is up to you to figure out.

### (Unordered) Sets
Perhaps one of the less utilized built-in structures in classes. Conceptualized as a collection of elements with unique hashes, which allows for
constant time lookups if something is contained within the set.
Commonly sets are used to make sure there is no repeat solutions and/or see if we have touched on a subproblem before.
Additionally, unordered_sets are similar in that they hold no internal order. In many use cases, an unordered_set is faster and works the same as a regular set.
```cpp
set<string> names; //default_constructor
unordered_set<int> vals; 
unordered_set<pair<int, int>> visited_nodes; // if you had a graph with each node denoted by x/y pairs

// insert an element to the set
my_set.insert("John");

// remove an element in the set
my_set.remove("John");

// see if an item with within the set
my_set.count("John") == 1 // count will be 1 if the key is present, otherwise 0

// iterating over the set can be done through the following:
for( auto it = my_set.begin(); it != my_set.end(); ++it){
    cout << *it << "\n";
}
//iterators can also be done backwards. my_set.rbegin(), and go until it != my_set.rend()
// have to use iterators, as there is no simple indexing of the set
// range style for loop
for (auto el : my_set) {
    cout << el << "\n";
}
```

### (Hash) Maps
The legendary datastructure :O

