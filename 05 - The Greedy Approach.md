# 05 - The Greedy Approach

## Overview
The Greedy Algorithm, as the name suggests, takes the most that it can 
as quickly as it can. It grabs data in a sequence that will be discussed
in detail later on in the chapter.

This approach usually leads to a simple, straight-forward solution, which 
makes it a good approach in optimization problems. It is also
more straightforward than other approaches in the sense that it does not
require dividing problems into smaller instances in order to solve them.
Hence, algorithms that use the Greedy approach usually operate much faster 
than those that use dynamic programming, 
**although they may not always yield the most optimal solution** since
they make **locally optimal decisions**, meaning that they make the best 
possible decision at each step without looking any further than that.

## The Giving Change Problem
Suppose we live in a country where the following coins are available:
|Coin|Amount in Cents|
|---|---|
|Dollar|100|
|Quarter|25|
|Dime|10|
|Nickle|5|
|Penny|1|

We are asked to devise an algorithm for paying a given amount to a customer
using the smallest amount of coins. Say the customer expects $2.89 (289 cents)
back. **That number is our target.**

The first step we take is to select the coin with the greatest valaue that is still less than our target. 
In this scenario, the greatest number less than 289
is 100, so ```2 'Dollar' coins * 100 cents = 200 cents```.

We are now left with ```289 - 200 = 89 cents``` left to return. That is our new target. We can  no longer use 100 cents as they are greater than our target.
The next best/largest option, however, is 25 cents, which are smaller than the target.

```3 quarters = 75 cents``` => ```200 + 75 = 275```

Our new value is still not the final change that the customer needs back.
As we continue to apply the greedy approach and find the needed change,
we come to the following final solution:

```2 dollars, 3 quarters, 1 dime, 4 pennies``` = ```10 coins```

```(200)      (75)        (10)    (4)      ``` = ```289 cents```

### Pseudocode for this Approach:
A greedy algorithm usually starts with an empty set and adds items to the set in sequence until the set represents a solution to an instance of a problem.
Each iteration in a greedy algorithm consists of the following 3 components:

**1. A selection procedure:** chooses greedily the next item to add to the set. The selection is preformed according to a greedy criterion that satisfies some locally optimal consideration at the time

**2. A feasibility check:** determines if the new set is feasible by checking whether it is possible to complete this set in such a way as to give a solution to the instance

**3. A solution check:** determines whether the new set constitutes a solution to the instance
> Note that: sometimes the selection procedure and feasibility check are combined into 1 step


```
while (there are more coins && the instance is not solved) {
  // selection procedure
  grab the largest remaining coin;	

  // feasibility check
  if (adding the coin make the change exceed the amount owed)
      reject the coin;
  else
      add the coin to the change;

  // solution check
  if (the total value of the change equals the amount owed)
      the instance is solved;
}
```

As aforementioned, the Greedy Approach may not always yield the most optimal
results. For example, in the scenario used for the Giving Change problem, if there existed a 12-cent coin and the target was 16 cents, the usage of this
specific approach ends up with us returning **5 coins** ```(12+1+1+1+1 = 16 cents)```.

And yet, the answer is optimizable to **3 coins** ```(10+5+1 = 16 cents)```.

While it is true that this algorithm is not always the best use-case in certain scenarios, **it still yields optimal results for the following problems:**
1. Minimum Spanning Trees
2. Single Source Shortest Path - Dijkstra's Algorithm (SSSP)
3. Scheduling
4. Data Compression (Huffman Code)
5. Fractional Knapsack Problem

## 5: Minimum Spanning Trees
To put it informally, the goal of the minimum spanning trees problem is to connect a collection of points/vertices together as 'cheaply' as possible. Consider the problem of removing edges from a connected, weighted, undirected graph G to form a sub-graph such that all the vertices remain connected, and the sum of the weights on the remaining edges is as small as possible.

This kind of problem has numerous real-life applications:
- Clustering (more on that later)
- Networking and Telecommunications
- Road Construction

Among many others...

_Recall that an undirected graph is called 'connected' if there is a path between every pair of vertices._ In an undirected graph, a path from a vertex to itself, which contains at least 3 vertices and in which all intermediate vertices are distinct, it is called a simple cycle. If an undirected graph contains no simple cycles, it is 'acyclic'.

A **free tree** is an acyclic connected undirected graph (it has **no root** and **no cycle**, not even a simple cycle).

### The name 'Minimum Spanning Tree' suggests the following:
- _Minimum:_ The sum of weight of selected edges must be as small as possible
- _Spanning:_ It overs all vertices and remains a connected graph
- _Tree:_ Free Tree (0 cycles)

**Few additional notes:**

A spanning tree for a graph G is a connected subgraph that contains all the vertices in G and is a tree.

A connected subgraph of minimum weight must be a spanning tree, but not every spanning tree has minimum weight.

A spanning tree of minimum weight is called a minimum spanning tree (note the terminology used: 'a' minimum spanning tree suggests that there may be other trees avaliable).

A graph can have more than one minimum spanning tree
  - All have the same minimum amount
  - But they have different edges that connect the vertices

```A spanning Tree T for G = (V, E) has the same set of vertices V as G```.
But the set of edges of T is a subset F of E.
We denote a spanning tree T = (V, F) ; where 𝐹 ⊆𝐸
i.e. F is a subset of E.

Our problem is to find a subset F of E such that T = (V, F) is a minimum spanning tree for G.
The brute force method of considering all spanning trees is worse than exponential in the worst case, it is more like a factorial.

### Pseudocode for a high-level greedy algorithm:
```
// initialize set of edges to empty
F = 0;

while (instance is not solved) {
   // selection procedure
   select an edge according to some locally optimal procedure;

   feasibility check
   if (adding the edge to F does not create a cycle) {
      add it;
   }

   // solution check
   if (T = (V,F) is a spanning tree) {
      instance is solved;
   }
}
```

That is why we can look into 2 different Greedy algorithms for this problem: Prim's algorithm and Kruskal's algorithm. Each one of them uses different locally optimal properties, but both of them always produce minimum spanning trees (i.e. both are optimal for their use cases).

## 5.1: Prim's Algorithm for Minimum Spanning Trees
To start, we create an empty list that tracks which nodes we have touched. The next step is to pick an arbitrary node which will be used as a starting point for the algorithm. Say we start with node V<sub>1</sub>: V<sub>1</sub> is immediately added to the set 'visited'.

**Pseudocode:**
```
F = 0      // initialize set of edges to empty
Y = {v1};  // initialize set of vertices to contains only the 1st one

while (the instance is not solved) {
   // selection procedure and feasibility check
   select a vertex in V – Y that is nearest to Y;

   add the vertex to Y;
   add the edge to F;

   // solution check
   if (Y == V)
      the instance is solved;
}
```
Notes:
- The selection procedure and feasibility check are done together because taking the new vertex from V – Y guarantees that a cycle is not created
- If we pick up a different vertex than V1, we end up with a different Minimum Spanning Tree but _the cost remains the same_

The previous algorithm is suitable for small graphs, but for the purposes of writing an algorithm that can be implemented using a computer language, we need to describe a step-by-step procedure. We use an adjacency matrix W to represent the weighted graph:

- W[i][j] = weight on edge (if there is an edge between Vi and Vj)
- W[i][j] = ∞ if there is no edge between Vi and Vj
- W[i][j] = 0 if i = j

We also maintain two arrays: ```nearest``` and ```distance``` (for i = 2 ... n)
- nearest[i] = index of the vertex in Y nearest to Vi... Vi is not in Y -> Vi ∈ {V - Y}
- distance[i] = weight on edge between Vi and the vertex indexed by nearest[i]

At the start Y = {v1} -> nearest[vi] = 1 and distance[vi] = W[v1][vi]

To determine which vertex to add to Y in each iteration, we compute the index for which distance[vi] is the smallest
- Call the index: V<sub>near</sub>
- Set distance[vnear] = -1 to mark that it was added to Y

**Pseudocode:**
```
void prims ( int n, const number W[][], set_of_edges & F ) {
   index i, vnear;
   number min;
   edge e;

   index nearest[2..n];                  // because v1 belong to Y
   number distance[2..n];                // because v1 belong to Y
   F = 0;                                // F is the set of edges which is initially empty

   for ( i = 2; i <= n; i++ ) {          // For all vertices in V-Y, initialize v1
      nearest[i] = 1;                    // to be the nearest vertex in Y and
      distance[i] = W[1][i];             // initialize the distance from Y to be the
   }                                     // weight on the edge of v1

   // Add all n-1 vertices to Y, replace solution check
   repeat ( n – 1 times ) {
      min = ∞;
      for ( i = 2; i <= n; i++ ) {          // Check each vertex for being nearest to Y
         if ( 0 <= distance[i] < min ) {    // and pick the vertex with the
            min = distance[i];              // shortest distance
            vnear = i;
         }
      }

      e = edge connecting vertices indexed by vnear and nearest[vnear];
      add e to F;
      distance[vnear] = -1; // Add vertex indexed by vnear to Y

      // For each vertex not in Y, update its distance from Y
      for ( i = 2; i <= n; i++ ) {	
         if ( W[i][vnear] < distance[i] ) {	
            distance [i] = W[i][vnear];
            nearest[i] = vnear;
         }
      }
   }
}

```

**The time complexity depends on the data structure used:**
- Binary Heap, Adjaceny List: O(VlogV + ElogV)
- Adjacency Matrix, Searching: O(v<sup>2</sup>)

Prim’s algorithm produces a spanning tree, because Y = V at the end
**But is it minimal?** Although greedy algorithms are easier to develop than dynamic programming algorithms, it is usually more difficult to determine whether or not the greedy algorithm produces an optimal solution.
For a dynamic algorithm, we need only to show that the principle of optimality applies.
On the other hand, for a greedy algorithm we usually need a formal proof:

### Proof of Correctness


## 5.2: Kruskal's Algorithm for Minimum Spanning Trees
