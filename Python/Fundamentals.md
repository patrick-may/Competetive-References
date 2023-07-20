# Python Reference
Python, while a computationally slower language, can syntactically simplify a lot of the boilerplate code required to implement certain structures and execute various algorithms.

## I/O
Coming from `C++`, getting stdin input from python can sometimes feel a bit more obtuse than otherwise. 
Fundamentally:
```py
input_line = input().strip() # will read in one line from input as a string

# to delimit by spaces, one can:
firstval, secondval = input().strip().split()

# or, for arbitrary amounds of input on one line
input_list = input().strip().split() # input_list will be a list where each element is a space separated word from input

# All input in python is conserdered a string at first. To change to a different type, we must cast it to the right value.
int_input = int(input())
float_input = float(input())
```
These are the fundamental blocks that one can do all input off of. However, to be *proper*, the following way is faster:
```py
import sys
for line in sys.stdin:
    # process line as if it were an input() call.
    # also, this method automatically ends at EOF chars
```

Some people also do immediate processing with input using `map()`.
```py
def my_func(val1):
    return len(val1)

input_lengths = map(my_func, input().strip().split())
# input_lengths will be a map of the lengths of every word in input.

# to turn to a list, simply do the:
input_lengths = list(input_lengths)
```

**Fast IO**
```py 
input() # very very slow. instead:

from sys import stdin # import and use readline() in lieu of input() 
stdin.readline() 
```
## Built In Datastructures
Python has lists, which are collections of objects that can be of various types. They also are commonly used as a stack.
```py
my_list = []

my_list.append("value here") # adds element to back of list
top_of_stack = my_list.pop() # removes and returns the "top" element of the list, which is at the back
my_list.insert(0, "value") #inserts item into location of list. O(n)
my_list.remove("value") #remove item with certain value
```

Dictionaries (like maps)
```py
from collections import defaultdict, counter, deque

my_dict = defaultdict(int) #defaul value of 0
my_dict["key"] = "val"
keys = my_dict.keys()
vals = my_dict.vals()
pairs = my_dict.items()

# if not using a defaultdict, just check if a key is in the dict before modifying it, otherweise insert

freq_ct = couter(iterable)
# a constructor that will automatically make a dictionary of iterable, where every item is a key and every value is the frequency it appears in iterable

de = deque()
# like a regular list, but supports these O(1) operations:
de.popleft()
de.appendleft()
```

Sets
```py
my_set = set()
my_set.add("value")
```

## Quick Algos
```py
def binary_search(a_list: list[int], item: int) -> bool:
    if len(a_list) == 0:
        return False
    midpoint = len(a_list) // 2
    if a_list[midpoint] == item:
        return True
    if item < a_list[midpoint]:
        return binary_search(a_list[:midpoint], item)
    else:
        return binary_search(a_list[midpoint + 1 :], item)


def bfs_shortest_path(graph: dict, start, goal) -> list[str]:
    #graph is an adjacency matrix here

    explored = set()
    # keep track of all the paths to be checked
    queue = [[start]]

    # return path if start is goal
    if start == goal:
        return [start]

    # keeps looping until all possible paths have been checked
    while queue:
        # pop the first path from the queue
        path = queue.pop(0)
        # get the last node from the path
        node = path[-1]
        if node not in explored:
            neighbours = graph[node]
            # go through all neighbour nodes, construct a new path and
            # push it into the queue
            for neighbour in neighbours:
                new_path = list(path)
                new_path.append(neighbour)
                queue.append(new_path)
                # return path if neighbour is goal
                if neighbour == goal:
                    return new_path

            # mark node as explored
            explored.add(node)

    # in case there's no path between the 2 nodes
    return []

def bfs_shortest_path_distance(graph: dict, start, target) -> int:
    """Find shortest path distance between `start` and `target` nodes.
    Args:
        graph: node/list of neighboring nodes key/value pairs.
        start: node to start search from.
        target: node to search for.
    Returns:
        Number of edges in shortest path between `start` and `target` nodes.
        -1 if no path exists.
    Example:
        >>> bfs_shortest_path_distance(demo_graph, "G", "D")
        4
        >>> bfs_shortest_path_distance(demo_graph, "A", "A")
        0
        >>> bfs_shortest_path_distance(demo_graph, "A", "Unknown")
        -1
    """
    if not graph or start not in graph or target not in graph:
        return -1
    if start == target:
        return 0
    queue = [start]
    visited = set(start)
    # Keep tab on distances from `start` node.
    dist = {start: 0, target: -1}
    while queue:
        node = queue.pop(0)
        if node == target:
            dist[target] = (
                dist[node] if dist[target] == -1 else min(dist[target], dist[node])
            )
        for adjacent in graph[node]:
            if adjacent not in visited:
                visited.add(adjacent)
                queue.append(adjacent)
                dist[adjacent] = dist[node] + 1
    return dist[target]
```
