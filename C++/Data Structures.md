# C++ Reference

Here is some implementation for higher level data structures that may be useful, as well as a brief manual on their uses.

# Union Find (Disjoint Set)
```cpp
// initialize set with numbers counting up to N
void initialize ( int vec[], const int N) {
    for (int i = 0; i < N; ++i) {
        vec[i] = i;
    }
}

// helper func
int root(int vec[], int i) {
    while (vec[i] != i) {
        i = vec[i];
    }
    return i;
}

// union, i.e. joins the two sets that have elements A, B
void s_union(int vec[], int A, int B) {
    int root_a = root(vec, A);
    int root_b = root(vec, B);
    Arr[ root_a ] = root_b; // this is doing "path compression"
}

// used to check if two items are in the same set
bool find(int vec[], int A, int B) {
    return root(vec, A) == root(vec, B);
}
```
