# Chapter 03 - Graph Algorithms

## Introduction
An approach we take to problem-solving in the real world is converting the 
problem at hand into a graph. A proper choice of data structure can help reduce the 
running time of these algorithms.
> For example: In the single shortest route problem, using a data structure
> such as a queue or a stack is possible, however swapping it for Dijkstra's
> algorithm instead (min heap) would result in a faster, more optimal running
> time.


## Definitions
### Vertices & Edges
- A Graph G = (V,E) consists of a set of verticles V and a set of edges E.
  Each edge is a pair (V1,V2) where V1 and V2 are vertices that belong to V.
  - A set of vertices V would be: W = {V1, V2, V3, V4}
  - And a set of edges E is: E = {(V1,V2), (V1,V4), (V1,V3), (V3,V4)}
- If the edges do not have any direction, then (V1,V2) = (V2,V1)

### Directed and Undirected Graphs
If the pairs in a graph are ordered, then the graph is called a **directed
graph (digraph)**. If not, it is **undirected**. In a directed graph, V2 is
adjacent to V1 _if and only if_ the edge (V1,V2) belongs to E. On the other
hand, in an undirected graph, that same edge (V1,V2) has both its vertices
adjacent to one another.

### Weight/Cost
A 'weight' or 'cost' is a third component of the edge that may be present
in the graph. The cost of the traversal from one vertex to another should
be calculated to find the most efficient route during path-finding.

### Paths & Cycles
- A path in a graph is a sequence of vertices W1, W2, …, Wn  										
such that (W<sub>i</sub>, W<sub>i+1</sub>) belongs to E; where 1 ≤ i < n
- The moment a vertex is repeated, we say that this path contains a **cycle**.

> ## Applications
> As aforementioned, graphs are used in real life scenarios to solve problems.
> For example:
> 1. In an airport system: V = airports, E = direct flights
>    between airports. We look for the shortest or cheapest route.
> 2. The Web Graph (Search Engine): V = web pages, E = hyperlinks
> 3. Networking Routing Systems: V = devices, E = network cables, we want
>    to find the fastest network path

## Representations of Graphs in Memory MEM
There are two ways to represent a graph, each used in a specific situation:
Dense Graphs & Sparse Graphs.
   - **Dense Graphs:** Which use adjacency matrices (ex: 2D arrays) and contain many edges.
   - **Sparse Graphs:** Which use adjacency lists (ex: 1D array, linked lists) and have fewer 
   edges than a dense graph.

## Graph Traversals via BFS (Queue)
BFS (Breadth First Search) is an algorithm used to traverse or search a tree
or a graph. It starts at a certain vertex (tree/root) and **explores all of the
neightboring vehicles at the same depth**. Once it is done, it moves on to the
vertices at the next depth level.

Since a queue is used, the first vertex to be queued will be the first vertex
to be dequeued.

## Graph Traversal via DFS (Stack)
DFS (Depth First Search) is another algorithm used to traverse or search a tree
or a graph. The algorithm starts at the root node and explores **as far as 
possible along each branch** before backtracking.

Since a stack is used, the first vertex to be stacked will be the last vertex
to be popped.

## Topological Sort
Topological sorts are used in real life applications such as course prerequisite structures in universities, instruction scheduling in computers, evaluating and executing function calls, etc.

A topological sort of a Directed Acyclic Graph G is a linear ordering of all its vertices such that: 
* If G contains an edge (U,V), then U appears before V in the ordering
* For U -> V, we say we have out-degree from U and in-degree to V
**Note:** This does not work on cyclic and undirected graphs.

Every Directed Acyclic Graph has **at least** 1 topological sort, but the more there are edges in a graph, the more the number of dependencies, and the less the number of topological orders.

### Systematic Approach for Topological Sort:
- Find any vertex with no incoming edges (in-degree = 0)
- Print this vertex
- Remove the vertex along with its edges from the graph
- Repeat the above steps until graph is empty
```
void Graph::topsort() { 
  for (int counter=0; counter<NUM_VERTICES; counter++) {     // running time = O(|V|)
    Vertex v = findNewVertexOfIndegreeZero();                // running time = O(|V|)

    if (v==NOT_A_VERTEX) {
      throw CycleFoundException();
    }

    v.topNum = counter;

    for each Vertex w adjacent to v {                        // running time = O(|V|)+O(|E|)
      w.indegree--;
    }
  }
}

// total running time = O (|V|^2+|E|)         
```

**This can be improved** by keeping all vertices of in-degree 0 in a data structure like a linked list, a sack, or a queue. So, we do the following:
* Place all vertices of in-degree 0 in an initially empty queue Q
* While Q non-empty, remove a vertex V, and increment the in-degrees of all vertices adjacent to V
* Put a vertex on the queue as soon as its in-degree is 0
> Note: The topological ordering is the order in which the vertices de-queue
> 
> Note: if “Q” was empty from the beginning, then we have a cycle

Its implementation would look as such (in pseudocode):
```
void Graph::topsort() {
  Queue<Vertex> q;
  int counter=0;

  q.makeEmpty;

  for each Vertex v                     // running time = O(|V|)
    if (v.indegree==0) {
      q.enqueue(v);
    }

  while (!q.isEmpty()) {                // running time = O(|V|)
    Vertex v = q.dequeue();
    v.topNum = ++counter;               // assign next number

    for each Vertex w adjacent to v     // running time = O(|E|)
      if(--w.indegree==0) {
        q.enqueue(w);
      }
  }

  if (counter!=NUM_VERTICES) throw CycleFoundException();
}

// total running time = O(|V|+|E|)
```
