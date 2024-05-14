# Chapter 05 - The Greedy Approach

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

## 5.1: Minimum Spanning Trees
To put it informally, the goal of the minimum spanning trees problem is to connect a collection of points/vertices together as 'cheaply' as possible. Consider the problem of removing edges from a connected, weighted, undirected graph G to form a sub-graph such that all the vertices remain connected, and the sum of the weights on the remaining edges is as small as possible.

This kind of problem has numerous real-life applications:
- Clustering (more on that later)
- Networking and Telecommunications
- Road Construction

Among many others...
