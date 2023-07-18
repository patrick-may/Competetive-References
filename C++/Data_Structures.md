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

# Djikstra's Algorithm using Priority Queue
```cpp
// don't actually have to do templating.
// current implementation: takes in an adjacency list, where each index of adj_list has edges with every
// second element of the vector it references (type N), with weights of type T. 
// returns a vector of size n, where n is the number of nodes, and T being a construction of weights used to 
// get from start point to end. start point is hard coded as 0, just change initial pq push to change
template<class T, class N>
vector<T> pq_djikstras(vector<vector<pair<T, N>>>& adj_list) {
    vector<bool> visited(adj_list.size(), false);
    vector<T> distances(adj_list.size(), 0.0); // or 0, or false, etc.
    priority_queue<pair<T, N>> pq:
    pq.push({1, 0}); // meaning start at note 0, with `weight` of 1. could be 0, etc. 

    while (!pq.empty()) {
        N currnode = pq.top().second;
        T size = pq.top().first;
        pq.pop();

        if(visited[currnode]) {
            continue;
        }

        dist[currnode] = size;

        for(auto i: adj_list[currnode]) {
            N next = i.second;
            T edge_cost = i.first;
            pq.push({size * edge_cost, next});
        }
    }

    return distances;
}

// then, get cost of total path to target node by:
...
    vector<T> dists = pq_djikstras...;
    T soln = dists[<node_idx>];
```
