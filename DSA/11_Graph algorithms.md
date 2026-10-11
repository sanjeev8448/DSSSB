# 1. BFS — Breadth-First Search

Breadth-First Search (BFS) visits a graph level by level. It explores all immediately reachable neighbors before proceeding to the next level.

BFS uses a queue, which follows FIFO (First In, First Out).

Consider this undirected graph:

```
        A
       / \
      B   C
     / \   \
    D   E   F
```

Its adjacency list is:

```
graph = {    "A": ["B", "C"],    "B": ["A", "D", "E"],    "C": ["A", "F"],    "D": ["B"],    "E": ["B"],    "F": ["C"]}
```

Starting from `A`, BFS proceeds level by level.

### BFS traversal levels

### Level 0

A

### Level 1

B, C

### Level 2

D, E, F

BFS finishes the current level before visiting the next level.

With the neighbor order shown in the graph's adjacency list, the BFS traversal is:

```
A → B → C → D → E → F
```

The exact order can differ if the neighbors are visited in a different order.

## 1.1 Python implementation of BFS

```

from collections import deque

def bfs(graph, start):
    visited = {start}
    queue = deque([start])
    order = []

    while queue:
        vertex = queue.popleft()
        order.append(vertex)

        for neighbor in graph[vertex]:
            if neighbor not in visited:
                visited.add(neighbor)
                queue.append(neighbor)

    return order


graph = {
    "A": ["B", "C"],
    "B": ["A", "D", "E"],
    "C": ["A", "F"],
    "D": ["B"],
    "E": ["B"],
    "F": ["C"]
}

print(bfs(graph, "A"))

```

Output:

```
['A', 'B', 'C', 'D', 'E', 'F']
```

### How the queue changes

|Step|Vertex processed|Queue after adding unvisited neighbors|
|---|---|---|
|1|A|`[B, C]`|
|2|B|`[C, D, E]`|
|3|C|`[D, E, F]`|
|4|D|`[E, F]`|
|5|E|`[F]`|
|6|F|`[]`|

Important: A vertex is marked visited when it is enqueued, not when it is removed from the queue. This prevents a vertex from being added multiple times through different paths.

# 2. BFS time complexity — the most important part

The complexity depends on the graph representation.

## 2.1 BFS using an adjacency list

An adjacency list stores the neighbors of each vertex. For example:

```
graph = {
    "A": ["B", "C"],
    "B": ["A", "D"],
    "C": ["A", "D"],
    "D": ["B", "C"]
}
```

The key BFS operations are:

```
while queue:
    vertex = queue.popleft()

    for neighbor in graph[vertex]:
        if neighbor not in visited:
            visited.add(neighbor)
            queue.append(neighbor)
```

Let's count the work.

Step 1: Visit vertices.

Each vertex is enqueued and dequeued at most once. That produces \(O(V)\) total queue processing and visited-set work, assuming expected constant-time set operations.

Step 2: Examine edges.

The algorithm iterates through each vertex's adjacency list. Across all vertices, the total number of neighbor entries is:

- \(E\) for a directed graph with \(E\) stored outgoing edges.
    
- \(2E\) for a typical undirected adjacency list, because each undirected edge appears in both endpoint lists.
    

Both are \(O(E)\).

Therefore:

\[ T(V,E)=O(V)+O(E) \]

So the standard time complexity is:

\[ \boxed{O(V+E)} \]

For a full traversal of all vertices and all adjacency-list edges, the tight bound is \(\Theta(V+E)\).

### BFS complexity using an adjacency list

|Operation|Complexity|
|---|---|
|Initialize the visited set and queue|\(O(1)\) for the single start vertex|
|Process all vertices|\(O(V)\)|
|Examine all adjacency-list entries|\(O(E)\)|
|Total time|\(O(V+E)\)|
|Auxiliary space for queue, visited set, and traversal order|\(O(V)\)|

The returned `order` list stores up to \(V\) vertices. If we use only the queue and visited set, auxiliary space is still \(O(V)\).

### Example calculation

Suppose a graph has:

- \(V=100\) vertices
    
- \(E=200\) edges
    

Then:

\[ V+E=100+200=300 \]

The complexity is \(O(V+E)\), or \(O(300)\) when substituting those input sizes into the expression. This is an illustration of the input-size expression, not a guarantee of exactly 300 machine operations.

Exam trap: BFS on an adjacency list is \(O(V+E)\), not simply \(O(V)\), because the algorithm must also examine the edges.

## 2.2 BFS using an adjacency matrix

An adjacency matrix contains \(V\) columns for each vertex.

For every vertex processed by BFS, the algorithm scans its entire matrix row to find neighbors. That takes \(O(V)\) work per vertex.

Across all vertices:

\[ T(V)=V\times O(V) \]

Therefore:

\[ \boxed{O(V^2)} \]

|Graph representation|BFS time|Auxiliary space|
|---|---|---|
|Adjacency list|\(O(V+E)\)|\(O(V)\)|
|Adjacency matrix|\(O(V^2)\)|\(O(V)\)|

The space column excludes the graph representation itself. If total memory is being asked, add \(O(V+E)\) for an adjacency list or \(O(V^2)\) for an adjacency matrix.

### Why does the representation change complexity?

An adjacency list lets BFS examine just the neighbors that actually exist.

An adjacency matrix requires checking all possible neighbors, including non-edges. This can be more costly for sparse graphs.

For a simple undirected graph, \(E\le V(V-1)/2\), so \(O(V+E)\) is \(O(V^2)\) in the dense worst case. The adjacency-list bound is still more informative, especially for sparse graphs.

# 3. DFS — Depth-First Search

Depth-First Search (DFS) explores one branch as deeply as possible before returning to explore another branch.

DFS uses either:

- Recursion, which uses the call stack.
    
- An explicit stack.
    

Using the same graph:

```
        A
       / \
      B   C
     / \   \
    D   E   F
```

If DFS starts at `A` and visits neighbors in the listed order, the traversal is:

```
A → B → D → E → C → F
```

The algorithm visits A, explores B, goes deeper to D, backtracks to B, then visits E before returning to A and exploring C.

Important: DFS traversal order depends on neighbor order and the implementation. The output above assumes the adjacency lists shown earlier.

## 3.1 Python implementation of recursive DFS

```

def dfs(graph, vertex, visited=None):
    if visited is None:
        visited = set()

    visited.add(vertex)
    order = [vertex]

    for neighbor in graph[vertex]:
        if neighbor not in visited:
            order.extend(dfs(graph, neighbor, visited))

    return order


graph = {
    "A": ["B", "C"],
    "B": ["A", "D", "E"],
    "C": ["A", "F"],
    "D": ["B"],
    "E": ["B"],
    "F": ["C"]
}

print(dfs(graph, "A"))

```

Output:

```
['A', 'B', 'D', 'E', 'C', 'F']
```

The function marks each vertex visited before recursively exploring its neighbors. This prevents it from following the same vertex repeatedly in cyclic graphs.

### DFS order on the same graph

|Step|Action|Visited order so far|
|---|---|---|
|1|Visit A|A|
|2|Go to B|A, B|
|3|Go to D|A, B, D|
|4|Backtrack and visit E|A, B, D, E|
|5|Backtrack and visit C|A, B, D, E, C|
|6|Visit F|A, B, D, E, C, F|

Unlike BFS, DFS does not finish all immediate neighbors of A before exploring B's descendants.

# 4. DFS time complexity — detailed analysis

## 4.1 DFS using an adjacency list

Consider the main part of the recursive DFS algorithm:

```
visited.add(vertex)

for neighbor in graph[vertex]:
    if neighbor not in visited:
        dfs(graph, neighbor, visited)
```

There are two main sources of work.

1. Vertex processing:

Each vertex is visited at most once. This costs \(O(V)\).

2. Edge examination:

The algorithm iterates over all adjacency lists. The total number of examined neighbor entries is \(O(E)\), or \(2E\) for a conventional undirected graph representation, which is still \(O(E)\).

Therefore:

\[ T(V,E)=O(V)+O(E) \]

The standard DFS time complexity is:

\[ \boxed{O(V+E)} \]

For a complete traversal of all reachable vertices and their adjacency-list entries, the tight bound is \(\Theta(V+E)\).

### DFS complexity table

|Resource|Complexity|Reason|
|---|---|---|
|Visit vertices|\(O(V)\)|Each vertex is visited at most once|
|Examine edges|\(O(E)\)|Each adjacency entry is examined a bounded number of times|
|Total time|\(O(V+E)\)|Vertex and edge processing|
|Visited set|\(O(V)\)|Stores discovered vertices|
|Recursive call stack|\(O(V)\) worst case|DFS may go through a path containing all vertices|
|Total auxiliary space|\(O(V)\)|Visited set and recursion stack|

For a graph with \(100\) vertices and \(200\) edges:

\[ T(V,E)=O(V+E)=O(100+200) \]

The complexity expression scales with both vertices and edges.

Exam trap: Recursive DFS does not use \(O(1)\) auxiliary space. Its recursion stack can hold up to \(O(V)\) active calls in the worst case.

## 4.2 DFS using an adjacency matrix

With an adjacency matrix, for every vertex visited, DFS scans all \(V\) possible neighbors.

That is \(O(V)\) work per vertex.

Across \(V\) vertices:

\[ T(V)=V\times O(V) \]

Therefore:

\[ \boxed{O(V^2)} \]

|Graph representation|DFS time|Auxiliary space|
|---|---|---|
|Adjacency list|\(O(V+E)\)|\(O(V)\)|
|Adjacency matrix|\(O(V^2)\)|\(O(V)\)|

Again, this auxiliary space excludes the graph's own representation.

## 4.3 BFS vs DFS complexity

|Feature|BFS|DFS|
|---|---|---|
|Adjacency-list time|\(O(V+E)\)|\(O(V+E)\)|
|Adjacency-matrix time|\(O(V^2)\)|\(O(V^2)\)|
|Auxiliary space|\(O(V)\)|\(O(V)\) worst case|
|Main data structure|Queue|Stack or recursive call stack|
|Shortest path by edge count in an unweighted graph|Guaranteed|Not guaranteed|
|Handles cycles safely|With visited tracking|With visited tracking|

The key exam point is that BFS and DFS have the same standard traversal time complexity when using the same graph representation. Their main difference is the order in which they explore vertices and the data structure they use.

# 5. Disconnected graphs — important complexity trap

A graph can contain multiple connected components.

Consider this undirected graph:

```
A —— B —— C       D —— E
```

There are two connected components:

- Component 1: A, B, C
    
- Component 2: D, E
    

If BFS or DFS starts at A, it only visits A, B, and C. It does not automatically visit D and E.

### Traversing every component

To traverse the entire graph, start a new BFS or DFS from every vertex that has not already been visited.

```

def dfs_all(graph):
    visited = set()
    order = []

    for vertex in graph:
        if vertex not in visited:
            component_order = dfs(graph, vertex, visited)
            order.extend(component_order)

    return order

```

This uses the `dfs()` function defined earlier.

### What is the complexity of a complete traversal?

With an adjacency list, the outer loop examines all \(V\) vertices. Across all components, every vertex is visited once and every edge is examined a bounded number of times.

Therefore:

\[ \boxed{O(V+E)} \]

This remains true for both BFS and DFS across all components.

Exam trap: A traversal from one source visits only reachable vertices. A full-graph traversal launches a new search for every still-unvisited component.

# 6. Complexity questions: how to solve them in exams

Use this three-step approach:

1. Identify what gets processed: vertices, edges, or both.
    
2. Count how many times each part executes: once per vertex, once per edge, or repeatedly.
    
3. Add the work and simplify: discard constants and lower-order terms.
    

Let's practise with common patterns.

## Example A: Vertex-only processing

```
for vertex in vertices:    print(vertex)
```

The loop visits each vertex once.

\[ \boxed{O(V)} \]

## Example B: Processing every neighbor

```
for vertex in range(V):
    for neighbor in range(V):
        if matrix[vertex][neighbor]:
            print(vertex, neighbor)
```

The outer loop visits each vertex. The inner loop processes the adjacency entries. Across the entire graph, the sum of all adjacency-list lengths is \(O(E)\).

Therefore:

\[ \boxed{O(V+E)} \]

It is not necessarily \(O(V^2)\), because sparse graphs may have far fewer than \(V^2\) edges.

## Example C: Matrix row scanning

```
for vertex in range(V):
    for neighbor in range(V):
        if matrix[vertex][neighbor]:
            print(vertex, neighbor)
```

Both loops run \(V\) times:

\[ V\times V=V^2 \]

Therefore:

\[ \boxed{O(V^2)} \]

## Example D: Repeated reachability checks

Suppose you run a new complete BFS independently from every vertex in a graph, without reusing visited results between searches.

With an adjacency list, each BFS costs \(O(V+E)\) in the full-traversal worst case. Repeating it \(V\) times gives the upper bound:

\[ \boxed{O\big(V(V+E)\big)} \]

This differs from a single BFS because the graph can be traversed repeatedly.

# 7. A complexity formula sheet for BFS and DFS

|Algorithm and representation|Time complexity|Auxiliary space|
|---|---|---|
|BFS, adjacency list|\(O(V+E)\)|\(O(V)\)|
|DFS, adjacency list|\(O(V+E)\)|\(O(V)\)|
|BFS, adjacency matrix|\(O(V^2)\)|\(O(V)\)|
|DFS, adjacency matrix|\(O(V^2)\)|\(O(V)\)|
|BFS/DFS from one source|Depends on reachable vertices and edges|\(O(V)\) upper bound|
|Full BFS/DFS across components|\(O(V+E)\) for adjacency lists|\(O(V)\)|
|Run full BFS independently from every vertex|\(O(V(V+E))\) upper bound|Depends on whether results are stored or reused|

For a single-source traversal that reaches only part of a graph, a more precise adjacency-list bound is \(O(V_r+E_r)\), where \(V_r\) and \(E_r\) are the vertices and edges in the reachable portion. The common \(O(V+E)\) bound is the graph-wide upper bound.

## 7.1 Why BFS shortest-paths work in unweighted graphs

BFS visits vertices in nondecreasing distance from the source, where distance is measured by the number of edges.

For example:

```
A —— B —— D
 \       /
  \— C —/
```

Starting from A, BFS discovers B and C at distance 1 before discovering D at distance 2.

Thus, BFS can find shortest paths by edge count in an unweighted graph.

Exam trap: DFS may find a path to a destination, but it does not guarantee finding the shortest path. Ordinary BFS also does not guarantee a minimum-cost path when edge weights matter.

## Final revision sheet

Memorize these formulas:

- BFS with adjacency list: \(O(V+E)\)
    
- DFS with adjacency list: \(O(V+E)\)
    
- BFS with adjacency matrix: \(O(V^2)\)
    
- DFS with adjacency matrix: \(O(V^2)\)
    
- BFS/DFS auxiliary space: \(O(V)\)
    
- Full traversal of disconnected graph using an adjacency list: \(O(V+E)\)
    
- BFS shortest path in an unweighted graph: Yes, by edge count.
    
- DFS shortest path guarantee: No.
    

Most important exam strategy: Whenever a complexity question mentions BFS or DFS, first identify the graph representation. Then count vertex processing and neighbor/edge processing. This quickly distinguishes \(O(V+E)\) from \(O(V^2)\), the two most important complexity answers in this topic.