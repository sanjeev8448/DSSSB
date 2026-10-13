# Graph Algorithms: BFS and DFS

## 1. BFS — Breadth-First Search

Breadth-First Search (BFS) visits a graph **level by level**. It explores all immediately reachable neighbors before proceeding to the next level.

BFS uses a **queue**, which follows FIFO (First In, First Out).

### 1.1 Example Graph

```
        A
       / \
      B   C
     / \   \
    D   E   F
```

Its adjacency list is:

```
graph = {
    "A": ["B", "C"],
    "B": ["A", "D", "E"],
    "C": ["A", "F"],
    "D": ["B"],
    "E": ["B"],
    "F": ["C"]
}
```

Starting from vertex `A`, BFS proceeds level by level.

|Level|Vertices|
|---|---|
|Level 0|A|
|Level 1|B, C|
|Level 2|D, E, F|

With the neighbor order shown in the adjacency list, the BFS traversal is:

```
A → B → C → D → E → F
```

The exact traversal order can differ if neighbors are visited in a different order.

### 1.2 Python Implementation of BFS

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

**Output:**

```
['A', 'B', 'C', 'D', 'E', 'F']
```

### 1.3 How the Queue Changes

|Step|Vertex processed|Queue after adding unvisited neighbors|
|---|---|---|
|1|A|[B, C]|
|2|B|[C, D, E]|
|3|C|[D, E, F]|
|4|D|[E, F]|
|5|E|[F]|
|6|F|[]|

**Important exam point:** A vertex is marked visited when it is added to the queue, not when it is removed. This prevents the same vertex from being enqueued multiple times through different paths.

---

## 2. BFS Time Complexity

The time complexity of BFS depends on the graph representation.

### 2.1 BFS Using an Adjacency List

An adjacency list stores the neighbors of each vertex.

Consider the main BFS operations:

```
while queue:
    vertex = queue.popleft()

    for neighbor in graph[vertex]:
        if neighbor not in visited:
            visited.add(neighbor)
            queue.append(neighbor)
```

There are two main sources of work.

**Step 1: Process vertices**

Each vertex is enqueued and dequeued at most once. This requires O(V) total vertex-processing work, assuming expected constant-time set operations.

**Step 2: Examine edges**

The algorithm examines every adjacency-list entry.

- For a directed graph, the total number of stored outgoing-edge entries is E.
    
- For a conventional undirected graph, each edge appears in both endpoint lists, producing 2E entries.
    

Both require O(E) work.

Therefore:

```
Total time = O(V) + O(E)
```

The standard BFS time complexity is:

**O(V + E)**

For a complete traversal of all vertices and adjacency-list entries, the tight bound is Θ(V + E).

### 2.2 BFS Complexity Table

|Operation|Complexity|
|---|---|
|Initialize queue and visited set for one start vertex|O(1)|
|Process all vertices|O(V)|
|Examine adjacency-list entries|O(E)|
|Total time|O(V + E)|
|Auxiliary space|O(V)|

The auxiliary space includes the queue, visited set, and traversal-order list.

### 2.3 Example Calculation

Suppose a graph has:

- V = 100 vertices
    
- E = 200 edges
    

Then:

```
V + E = 100 + 200 = 300
```

The complexity is O(V + E). Substituting the input sizes gives O(300) as an illustration of the expression, not an exact count of machine operations.

**Exam trap:** BFS with an adjacency list is O(V + E), not simply O(V), because the algorithm must also examine edges.

### 2.4 BFS Using an Adjacency Matrix

An adjacency matrix has V columns for each vertex.

For every vertex processed by BFS, the algorithm scans the entire matrix row to identify neighbors. This takes O(V) work per vertex.

Across all V vertices:

```
V × O(V) = O(V²)
```

Therefore, BFS using an adjacency matrix has time complexity **O(V²)**.

|Graph representation|BFS time|Auxiliary space|
|---|---|---|
|Adjacency list|O(V + E)|O(V)|
|Adjacency matrix|O(V²)|O(V)|

These auxiliary-space figures exclude the graph representation itself.

**Why does representation matter?**

- An adjacency list examines only the neighbors that actually exist.
    
- An adjacency matrix checks all possible neighbors, including non-edges.
    

This difference is especially important for sparse graphs.

---

## 3. DFS — Depth-First Search

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

Starting from `A` and visiting neighbors in the listed order, the DFS traversal is:

```
A → B → D → E → C → F
```

The algorithm visits A, explores B, goes deeper to D, backtracks to B, visits E, and then returns to A to explore C and F.

**Important:** DFS traversal order depends on neighbor order and implementation.

### 3.1 Python Implementation of Recursive DFS

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

**Output:**

```
['A', 'B', 'D', 'E', 'C', 'F']
```

The function marks each vertex visited before recursively exploring its neighbors. This prevents repeated visits in cyclic graphs.

### 3.2 DFS Traversal Steps

|Step|Action|Visited order so far|
|---|---|---|
|1|Visit A|A|
|2|Go to B|A, B|
|3|Go to D|A, B, D|
|4|Backtrack and visit E|A, B, D, E|
|5|Backtrack and visit C|A, B, D, E, C|
|6|Visit F|A, B, D, E, C, F|

Unlike BFS, DFS does not finish visiting all immediate neighbors of A before exploring B's descendants.

---

## 4. DFS Time Complexity

### 4.1 DFS Using an Adjacency List

Consider the main part of recursive DFS:

```
visited.add(vertex)

for neighbor in graph[vertex]:
    if neighbor not in visited:
        dfs(graph, neighbor, visited)
```

**Vertex processing:** Each vertex is visited at most once, requiring O(V) work.

**Edge examination:** Every adjacency-list entry is examined a bounded number of times, requiring O(E) work.

Therefore:

```
T(V, E) = O(V) + O(E)
```

The standard DFS time complexity is **O(V + E)**.

### 4.2 DFS Complexity Table

|Resource|Complexity|Reason|
|---|---|---|
|Visit vertices|O(V)|Each vertex is visited at most once|
|Examine edges|O(E)|Each adjacency entry is examined a bounded number of times|
|Total time|O(V + E)|Vertex and edge processing|
|Visited set|O(V)|Stores discovered vertices|
|Recursive call stack|O(V) worst case|A path may contain all vertices|
|Total auxiliary space|O(V)|Visited set and recursion stack|

For a graph with 100 vertices and 200 edges, the complexity expression becomes O(100 + 200).

**Exam trap:** Recursive DFS does not use O(1) auxiliary space. Its recursion stack can contain up to O(V) active calls in the worst case.

### 4.3 DFS Using an Adjacency Matrix

For each vertex visited, DFS scans all V possible neighbors.

```
V vertices × O(V) work per vertex = O(V²)
```

Therefore, DFS using an adjacency matrix has time complexity **O(V²)**.

|Graph representation|DFS time|Auxiliary space|
|---|---|---|
|Adjacency list|O(V + E)|O(V)|
|Adjacency matrix|O(V²)|O(V)|

Again, auxiliary space excludes the graph representation itself.

---

## 5. BFS vs DFS

|Feature|BFS|DFS|
|---|---|---|
|Adjacency-list time|O(V + E)|O(V + E)|
|Adjacency-matrix time|O(V²)|O(V²)|
|Auxiliary space|O(V)|O(V) worst case|
|Main data structure|Queue|Stack or recursive call stack|
|Exploration style|Level by level|Depth first|
|Shortest path by edge count in an unweighted graph|Guaranteed|Not guaranteed|
|Handles cycles safely|With visited tracking|With visited tracking|

**Key exam point:** BFS and DFS have the same standard traversal time complexity when they use the same graph representation. Their main difference is the order in which they explore vertices and the data structure they use.

---

## 6. Disconnected Graphs

A graph can contain multiple connected components.

Example:

```
A —— B —— C       D —— E
```

There are two connected components:

- Component 1: A, B, C
    
- Component 2: D, E
    

If BFS or DFS starts at A, it visits only A, B, and C. It does not automatically visit D and E.

### 6.1 Traversing Every Component

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

This function uses the earlier `dfs()` implementation.

### 6.2 Complexity of a Complete Traversal

With an adjacency list:

- The outer loop examines all V vertices.
    
- Each vertex is visited once.
    
- Each edge is examined a bounded number of times.
    

Therefore, the complete traversal across all components has complexity:

**O(V + E)**

This applies to both BFS and DFS when implemented to visit every component.

**Exam trap:** A traversal from one source visits only reachable vertices. A full-graph traversal launches a new search for every still-unvisited component.

---

## 7. How to Solve Graph Complexity Questions

Use this three-step method:

1. Identify what is processed: vertices, edges, or both.
    
2. Count how often each part executes: once per vertex, once per edge, or repeatedly.
    
3. Add the work and simplify by removing constants and lower-order terms.
    

### Example A: Vertex-Only Processing

```
for vertex in vertices:
    print(vertex)
```

Each vertex is processed once.

**Complexity: O(V)**

### Example B: Processing Every Neighbor Using an Adjacency List

```
for vertex in graph:
    for neighbor in graph[vertex]:
        print(vertex, neighbor)
```

The outer loop processes vertices, and the inner loops collectively process adjacency entries.

**Complexity: O(V + E)**

### Example C: Matrix Row Scanning

```
for vertex in range(V):
    for neighbor in range(V):
        if matrix[vertex][neighbor]:
            print(vertex, neighbor)
```

Both loops run V times:

```
V × V = V²
```

**Complexity: O(V²)**

This is the typical cost of scanning every entry of an adjacency matrix.

### Example D: Running BFS Independently from Every Vertex

Suppose a new full BFS is run independently from every vertex without reusing previous results.

Each BFS has an O(V + E) upper bound using an adjacency list. Repeating it V times gives:

```
O(V × (V + E))
```

This differs from one BFS because the graph may be traversed repeatedly.

---

## 8. BFS and DFS Formula Sheet

|Algorithm and representation|Time complexity|Auxiliary space|
|---|---|---|
|BFS, adjacency list|O(V + E)|O(V)|
|DFS, adjacency list|O(V + E)|O(V)|
|BFS, adjacency matrix|O(V²)|O(V)|
|DFS, adjacency matrix|O(V²)|O(V)|
|BFS/DFS from one source|O(V + E) upper bound|O(V) upper bound|
|Full BFS/DFS across components|O(V + E) with adjacency lists|O(V)|
|Full BFS independently from every vertex|O(V(V + E)) upper bound|Depends on storage and implementation|

For a single-source traversal that reaches only part of a graph, a more precise adjacency-list bound is O(Vᵣ + Eᵣ), where Vᵣ and Eᵣ are the vertices and edges in the reachable portion.

The common O(V + E) expression is the graph-wide upper bound.

---

## 9. Why BFS Finds Shortest Paths in Unweighted Graphs

BFS visits vertices in nondecreasing distance from the source, where distance is measured by the number of edges.

Example:

```
A —— B —— D
 \       /
  \— C —/
```

Starting from A, BFS discovers B and C at distance 1 before discovering D at distance 2.

Therefore, BFS can find shortest paths by **edge count in an unweighted graph**.

**Exam traps:**

- DFS may find a path but does not guarantee the shortest path.
    
- Ordinary BFS does not guarantee a minimum-cost path when edge weights matter.
    
- For weighted shortest-path problems, the appropriate algorithm depends on the edge weights and problem constraints.
    

---

## 10. Final Revision Sheet

Memorize these formulas:

- BFS with adjacency list: **O(V + E)**
    
- DFS with adjacency list: **O(V + E)**
    
- BFS with adjacency matrix: **O(V²)**
    
- DFS with adjacency matrix: **O(V²)**
    
- BFS auxiliary space: **O(V)**
    
- DFS auxiliary space: **O(V)**
    
- Full traversal of a disconnected graph using adjacency lists: **O(V + E)**
    
- BFS shortest path in an unweighted graph: **Guaranteed shortest path by edge count**
    
- DFS shortest path: **No shortest-path guarantee**
    

### Highest-Priority DSSSB Exam Strategy

Whenever a question asks for BFS or DFS complexity:

1. Identify the graph representation.
    
2. Count vertex processing.
    
3. Count neighbor or edge processing.
    
4. Distinguish a traversal from one source from a traversal of the entire disconnected graph.
    

The most important distinction is **O(V + E) for adjacency lists versus O(V²) for adjacency matrices**.