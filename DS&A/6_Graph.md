# DSSSB TGT Computer Science — Data Structures Notes

## Topic: Graphs, Graph Representation, BFS and DFS

# 1. Graph Fundamentals

A **graph** is commonly represented as:

**G = (V, E)**

Where:

- **V** is the set of vertices.
    
- **E** is the set of edges connecting vertices.
    

### Example graph

Vertices: A, B, C, D, E

Edges: AB, AC, BD, CD, DE

Therefore:

- V = {A, B, C, D, E}
    
- E = {(A, B), (A, C), (B, D), (C, D), (D, E)}
    
- Number of vertices = 5
    
- Number of edges = 5
    

### Important graph terminology

|Term|Meaning|
|---|---|
|Vertex (node)|An individual point in a graph|
|Edge|A connection between two vertices|
|Adjacent vertices|Vertices directly connected by an edge|
|Degree|Number of incident edges in an undirected graph|
|Path|A sequence of vertices connected by edges|
|Cycle|A path that returns to its starting vertex|
|Connected graph|Every pair of vertices has a path between them|
|Self-loop|An edge from a vertex to itself|
|Isolated vertex|A vertex with no incident edges|

For example, A and B are adjacent, and vertex E has degree 1 in the example graph.

**Exam trap:** In an undirected graph, a self-loop contributes 2 to the degree of its vertex.

# 2. Directed vs Undirected Graphs

## 2.1 Undirected graph

An undirected graph has edges without directions. A connection between A and B can be followed in either direction.

Example: A — B

Applications:

- Two-way roads between cities
    
- Mutual friendship relationships
    

In an undirected graph, edge (A, B) is equivalent to edge (B, A).

## 2.2 Directed graph

A directed graph, also called a **digraph**, contains edges with directions.

Example: A → B

The edge A → B does not automatically permit travel from B to A.

Applications:

- One-way roads
    
- Website links
    
- Prerequisite relationships
    

A directed edge A → B is different from B → A.

### Directed vs undirected graph

|Feature|Directed graph|Undirected graph|
|---|---|---|
|Edge|Has a direction|Has no direction|
|Edge notation|A → B|A — B|
|Can an edge be followed backward automatically?|No|Yes|
|Degree terminology|In-degree and out-degree|Degree|
|Adjacency relationship|May be asymmetric|Symmetric|

For a directed graph:

- **In-degree:** Number of edges entering a vertex.
    
- **Out-degree:** Number of edges leaving a vertex.
    

Example: If A → B and C → B, then the in-degree of B is 2.

**Exam trap:** In a directed graph, the sum of all in-degrees equals the sum of all out-degrees. Both sums equal the number of edges.

# 3. Weighted vs Unweighted Graphs

## 3.1 Unweighted graph

An unweighted graph represents connections without assigning a numerical cost or weight to each edge.

```
A —— B
|    |
C —— D
```

A path's length is commonly measured by the number of edges traversed.

## 3.2 Weighted graph

A weighted graph assigns a numerical value to an edge. The value may represent distance, cost, travel time, or another quantity.

Example edge weights:

- A — B = 5
    
- A — C = 2
    
- B — D = 7
    
- C — D = 4
    

Path A → C → D:

Total weight = 2 + 4 = 6

Path A → B → D:

Total weight = 5 + 7 = 12

Therefore, A → C → D has the lower total weight.

**Important:** The lowest-weight path is not necessarily the path with the fewest edges. Weights can represent costs other than distance.

### Graph classification

These categories are independent. A graph may be:

- Directed and weighted
    
- Directed and unweighted
    
- Undirected and weighted
    
- Undirected and unweighted
    

# 4. Graph Representation

Graph representation describes how a graph is stored in a computer program.

The main representations are:

1. Adjacency matrix
    
2. Adjacency list
    
3. Edge list
    

Consider this undirected graph:

```
A —— B
|    |
C —— D
```

Its edge set is:

E = {(A, B), (A, C), (B, D), (C, D)}

## 4.1 Adjacency matrix

An adjacency matrix uses a two-dimensional matrix to represent connections.

For a simple unweighted graph:

- `1` means an edge exists.
    
- `0` means no edge exists.
    

Python implementation:

```
vertices = ["A", "B", "C", "D"]

matrix = [
    [0, 1, 1, 0],  # A
    [1, 0, 0, 1],  # B
    [1, 0, 0, 1],  # C
    [0, 1, 1, 0]   # D
]

for row in matrix:
    print(row)
```

Output:

```
[0, 1, 1, 0]
[1, 0, 0, 1]
[1, 0, 0, 1]
[0, 1, 1, 0]
```

Rows and columns follow the vertex order A, B, C, D.

Examples:

- `matrix[0][1] == 1` means A is connected to B.
    
- `matrix[0][3] == 0` means A is not connected to D.
    

For an undirected graph, the adjacency matrix is symmetric:

**M[i][j] = M[j][i]**

For a directed graph, this symmetry is not guaranteed.

### Advantages and disadvantages

- Checking whether a particular pair of vertices is connected takes O(1) time.
    
- Space complexity is O(V²), even for sparse graphs.
    
- It is often convenient for dense graphs.
    

For a weighted graph, matrix entries can store edge weights instead of 1 and 0. The absence of an edge needs a consistent representation, such as `None` or infinity, depending on the algorithm.

## 4.2 Adjacency list

An adjacency list stores the neighbors of every vertex.

Python implementation:

```
graph = {
    "A": ["B", "C"],
    "B": ["A", "D"],
    "C": ["A", "D"],
    "D": ["B", "C"]
}

for vertex, neighbors in graph.items():
    print(vertex, ":", neighbors)
```

Output:

```
A : ['B', 'C']
B : ['A', 'D']
C : ['A', 'D']
D : ['B', 'C']
```

For an undirected graph, each edge appears in both endpoint lists. For example, A — B appears as B in A's list and A in B's list.

### Advantages and disadvantages

- Space complexity: O(V + E).
    
- Efficient for sparse graphs.
    
- Convenient for iterating over a vertex's neighbors.
    
- Checking whether a particular edge exists may require searching the neighbor list, taking up to O(deg(v)) time with a simple list representation.
    

## 4.3 Edge list

An edge list stores the graph as a collection of edges.

```
edges = [
    ("A", "B"),
    ("A", "C"),
    ("B", "D"),
    ("C", "D")
]

for edge in edges:
    print(edge)
```

Output:

```
('A', 'B')
('A', 'C')
('B', 'D')
('C', 'D')
```

For weighted graphs, an edge can include its weight, for example:

```
("A", "B", 5)
```

### Graph representation comparison

|Feature|Adjacency matrix|Adjacency list|Edge list|
|---|---|---|---|
|Storage|V × V matrix|Neighbors per vertex|Collection of edges|
|Space|O(V²)|O(V + E)|O(E), plus vertex storage if needed|
|Check a specific edge|O(1)|Up to O(deg(v)) with simple lists|O(E) in a basic unsorted list|
|Iterate over neighbors|O(V)|O(deg(v))|Usually requires scanning edges|
|Suitable use|Often dense graphs|Often sparse graphs|Edge-oriented algorithms|

Here:

- V = number of vertices
    
- E = number of edges
    
- deg(v) = degree of vertex v in an undirected graph
    

**Exam trap:** An adjacency matrix uses O(V²) space, whereas an adjacency list uses O(V + E) space.

# 5. BFS — Breadth-First Search

**Breadth-First Search (BFS)** traverses a graph level by level.

It visits:

1. The starting vertex
    
2. Its unvisited neighbors
    
3. The neighbors of those vertices
    
4. The remaining reachable vertices in successive levels
    

BFS uses a **queue (FIFO)**.

Consider:

```
A —— B
|    |
C —— D
```

Start at A and assume neighbors are visited in the order listed in the adjacency list.

Steps:

1. Visit A. Queue: [B, C]
    
2. Visit B. Add D. Queue: [C, D]
    
3. Visit C. D is already discovered. Queue: [D]
    
4. Visit D. Queue becomes empty.
    

BFS traversal:

```
A → B → C → D
```

## 5.1 Python implementation of BFS

```
from collections import deque

graph = {
    "A": ["B", "C"],
    "B": ["A", "D"],
    "C": ["A", "D"],
    "D": ["B", "C"]
}

def bfs(graph, start):
    visited = {start}
    queue = deque([start])

    while queue:
        vertex = queue.popleft()
        print(vertex, end=" ")

        for neighbor in graph[vertex]:
            if neighbor not in visited:
                visited.add(neighbor)
                queue.append(neighbor)

bfs(graph, "A")
```

Output:

```
A B C D
```

### Why mark a vertex visited when adding it to the queue?

Marking a vertex when discovered prevents it from being added repeatedly by different neighbors. This is especially important in graphs containing cycles.

For example, A connects to B and C, and both B and C connect to D. Marking D as visited when enqueuing it avoids adding it more than once.

### Applications of BFS

- Finding shortest paths in an unweighted graph, measured by number of edges
    
- Finding vertices reachable from a starting vertex
    
- Level-order traversal of trees
    
- Exploring connections in social networks
    
- Network discovery
    

**Exam trap:** BFS uses a queue, not a stack. In an unweighted graph, BFS finds a shortest path by edge count, but not necessarily the lowest-cost path in a weighted graph.

# 6. DFS — Depth-First Search

**Depth-First Search (DFS)** explores as far as possible along one branch before backtracking to explore other branches.

DFS can be implemented using:

- Recursion, which uses the call stack
    
- An explicit stack
    

Consider:

```
A —— B
|    |
C —— D
```

Starting at A and visiting neighbors in the listed order:

1. Visit A.
    
2. Go to B.
    
3. From B, go to D.
    
4. From D, go to C.
    
5. Backtrack after all reachable vertices are visited.
    

DFS traversal:

```
A → B → D → C
```

The exact DFS output depends on the order in which neighbors are considered.

## 6.1 Recursive DFS implementation

```
graph = {
    "A": ["B", "C"],
    "B": ["A", "D"],
    "C": ["A", "D"],
    "D": ["B", "C"]
}

def dfs(graph, vertex, visited=None):
    if visited is None:
        visited = set()

    visited.add(vertex)
    print(vertex, end=" ")

    for neighbor in graph[vertex]:
        if neighbor not in visited:
            dfs(graph, neighbor, visited)

dfs(graph, "A")
```

Output:

```
A B D C
```

The `visited` set is essential. Without it, a graph with cycles could trigger endless recursion.

## 6.2 Iterative DFS using a stack

```
graph = {
    "A": ["B", "C"],
    "B": ["A", "D"],
    "C": ["A", "D"],
    "D": ["B", "C"]
}

def dfs_iterative(graph, start):
    visited = set()
    stack = [start]

    while stack:
        vertex = stack.pop()

        if vertex in visited:
            continue

        visited.add(vertex)
        print(vertex, end=" ")

        # Reverse preserves the listed neighbor order in this example.
        for neighbor in reversed(graph[vertex]):
            if neighbor not in visited:
                stack.append(neighbor)

dfs_iterative(graph, "A")
```

Output:

```
A B D C
```

This implementation uses a Python list as a stack:

- `append()` pushes an element.
    
- `pop()` removes the top element.
    

## 6.3 BFS vs DFS

|Feature|BFS|DFS|
|---|---|---|
|Full name|Breadth-First Search|Depth-First Search|
|Data structure|Queue|Stack or recursion|
|Exploration|Level by level|Deep along a branch, then backtracks|
|Shortest path in an unweighted graph|Finds shortest path by edge count|Does not guarantee shortest path|
|Common applications|Shortest-path distances, level traversal|Cycle detection, backtracking, graph exploration|
|Time with adjacency list|O(V + E)|O(V + E)|

Both algorithms need a visited set for general graphs with cycles.

**Exam trap:** BFS and DFS may produce different valid traversal sequences depending on neighbor order. Consider the starting vertex and adjacency-list order when tracing outputs.

# 7. Directed/Undirected Graphs and BFS/DFS

BFS and DFS work with both directed and undirected graphs, but reachability differs.

### Example: directed graph

```
A → B → C
    ↑
    D
```

Starting BFS from A can visit A, B and C, but not D, because there is no directed path from A to D.

Starting at D can visit D, B and then C.

In an undirected graph, each edge works in both directions. In a directed graph, traversal follows only outgoing edges from the current vertex.

## 7.1 What if the graph is disconnected?

A traversal starting at one vertex visits only the vertices reachable from that vertex.

To traverse every connected component of an undirected graph, run BFS or DFS from each vertex that has not yet been visited.

Example using the recursive `dfs()` function defined earlier:

```
def dfs_all(graph):
    visited = set()

    for vertex in graph:
        if vertex not in visited:
            dfs(graph, vertex, visited)
            print()  # Separate connected components
```

The outer loop ensures that components not reachable from the initial vertex are also explored.

**Exam trap:** BFS or DFS from a single starting vertex does not necessarily visit every vertex in a disconnected graph.

# 8. Weighted Graphs and Shortest Paths

A weighted graph associates each edge with a weight or cost.

Example:

```
A --2-- B
|       |
5       1
|       |
C --2-- D
```

Path A → B → D:

Total weight = 2 + 1 = 3

Path A → C → D:

Total weight = 5 + 2 = 7

Therefore, A → B → D has the lower total weight.

### Which algorithm should be used?

|Problem|Typical algorithm|
|---|---|
|Reachability in any graph|BFS or DFS|
|Shortest path by number of edges in an unweighted graph|BFS|
|Shortest path with non-negative edge weights|Dijkstra's algorithm|
|Shortest paths with negative edges, assuming no relevant negative cycle|Bellman–Ford|
|Minimum spanning tree in an undirected weighted graph|Prim's or Kruskal's algorithm|

**Important distinction:** A weighted graph can still be traversed using BFS or DFS, but ordinary BFS does not account for edge weights when finding minimum-cost paths.

# 9. Time Complexity Summary

Let V be the number of vertices and E be the number of edges.

|Operation|Adjacency list|Adjacency matrix|
|---|---|---|
|Storage|O(V + E)|O(V²)|
|Check whether an edge exists|Up to O(deg(v))|O(1)|
|Iterate over one vertex's neighbors|O(deg(v))|O(V)|
|BFS|O(V + E)|O(V²)|
|DFS|O(V + E)|O(V²)|

With an adjacency-list implementation, BFS and DFS take O(V + E) time because vertices are processed and edges are examined a bounded number of times.

# 10. Final Revision Sheet

|Topic|Must remember|
|---|---|
|Graph|G = (V, E)|
|Adjacency matrix|O(V²) space|
|Adjacency list|O(V + E) space|
|Directed graph|Edges have directions|
|Undirected graph|Edges work both ways|
|Weighted graph|Edges have associated weights|
|Unweighted graph|Edges have no assigned weights|
|BFS|Queue; level-by-level exploration|
|DFS|Stack or recursion; deep exploration and backtracking|
|BFS/DFS with adjacency list|O(V + E)|
|BFS shortest path|Shortest path by edge count in an unweighted graph|
|Dijkstra|Shortest paths with non-negative weights|

## Highest-priority exam concepts

1. Adjacency matrix vs adjacency list
    
2. BFS vs DFS
    
3. Queue vs stack
    
4. Directed vs undirected graphs
    
5. Weighted vs unweighted edges
    
6. The role of visited sets
    
7. BFS/DFS time complexity: O(V + E) with adjacency lists
    
8. Selecting an appropriate shortest-path algorithm