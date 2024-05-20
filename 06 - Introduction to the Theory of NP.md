# 06 - Introduction to the Theory of NP
## Overview
The Traveling Salesperson problem and thousands of other problems are equally hard in the sense that, if we had an efficient algorithm for any one of them, we would have efficient algorithms for all of them.
Such an algorithm has _never been found yet_, and it has not been proven to not exist.
This kind of problem is called the NP Complete problem, or ```N```on-deterministic ```P```olynomial-time ```complete```.

If we have a problem _A_, we may have plenty exponential solution to this problem, but we may have some polynomial running time algorithms.
If we manage to find 1 algorithm that runs in polynomial time, then _A_ belongs to the set _P_ where _P_ is the set of problems that has polynomial algorithm

A problem for which an efficient algorithm is not possible (and proven to be not possible) is said to be **intractable**.
When we are concerned with determining whether or not a problem is intractable, we must note the _input size_ of the algorithm. 

This chapter will cover three general categories into which problems can be grouped as far as intractability is concerned
1. Set _P_: which is the set of problems that has polynomial algorithm
2. Set of intractable: which is the set of problems that we have proven that no efficient solution exist for them
3. Set of problems for which we haven’t ben able to find efficient solution, but we weren’t able to prove that we cannot find such an efficient solution

Finally, we will discuss the theory of NP and NP-complete problems

## Intractability
In the field of computation, a problem is said to be 'intractable' if a computer has difficulty solving it
(that is, _it is impossible to solve it with a polynomial-time algorithm_).
A polynomial-time algorithm is one whose worst-case time complexity is bounded above by a polynomial function of its input size.

Generally speaking, polynomial-time algorithms are better than non-polynomial time algorithms.
Many algorithms whose worst-case time complexities are not polynomials have efficient running times for many actual instances...
This is the case for many backtracking and branch-and-bound algorithms, among many other algorithms.

We stress that intractability is a property of a problem; it is not a property of any one algorithm for that problem.
For a problem to be intractable:
- There must be no polynomial-time algorithm that solves it
- There must be a **proof** that show that it is impossible to find a polynomial time algorithm

On the other hand, obtaining a non-polynomial-time algorithm for a problem does not make it intractable, for example:
For many of the algorithms that we discussed earlier we have found that brute force runs in 𝑂(2^𝑛) or 𝑂(𝑛!), and we found a greedy, dynamic, divide and conquer,... etc. algorithm that runs in 𝑂(𝑛 log⁡(𝑛))

_When we are determining whether an algorithm is polynomial-time, it is necessary to be careful about what we call input size._

## Input Size (Revisited)
For a given algorithm, **the input size is defined as the number of characters it takes to write/represent the input.**
In other words, to count the characters it takes to write the input, we need to know how the input is encoded.
For example, if we encode it in binary, the characters used for the encoding are binary digits, and the number of characters it takes to encode a positive integer “n” is
```floor(log2(n)) + 1```.
**The input size is the count of the number of bits it takes to encode them.**

## The Three General Problem Categories
There three general categories in which problems can be grouped as far as intractability is concerned:
1. Problems for which polynomial-time algorithms have been found
2. Problems that have been proven to be intractable
3. Problems that have not been proven to be intractable, but for which no polynomial-time algorithms have never been found

### 1 - Problems for Which Polynomial-Time Algorithms Have Been Found
Any problem for which we have found a polynomial-time algorithm falls into this category.
Problems for which we have developed polynomial-time algorithms but for which the brute-force algorithms are non-polynomial include:

Sorting problems (and not merge sort, heap sort, or quicksort, ... ),
The Minimum Spanning Tree problem,
Single Source Shortest Path (Dijkstra, ... ), etc.

### 2 - Problems that Have Been Proven to be Intractable
There are two types of problems in this category

1. The first type is problems that require a non-polynomial amount of output such as the problem of determining all Hamiltonian Circuits in a complete graph.
If there is an edge from every vertex to every other vertex, then there would be ```(n - 1)!``` such circuits.
To solve the problem, an algorithm would have to output all of these circuits, which means that our request is not reasonable.

2. The second type of intractability occurs when our requests are reasonable (i.e. the output is “Yes” or “No”)
and we can prove that the problem cannot be solved in polynomial time.
There are relatively few such problems. They fall again in 2 sub-categories:

  - **Undecidable problems:** Proven that no algorithm exist to solve these problems. These problems are usually artificially constructed, out of which the most well-known is the Halting Problem.
  - **Decidable Problems:** Proven that no efficient algorithm exist to solve these problems. In the early 1970s, some natural decidable decision problems were proven to be intractable.
The output for a decision problem is a simple “yes” or “no” answer,
therefore, the amount of output requested is certainly reasonable.
One of the most well-known of these problems is Presburger Arithmetic, which was proven intractable by Fischer and Rabin in 1974.
This problem, along with the proof of intractability, can be found in Hopcroft and Ullman (1979).

**Note:** 'Efficient' means that the problems cannot be solved in polynomial-time

### 3 - Problems that Have not Been Proven to be Intractable, but for Which No Polynomial-Time Algorithms Have Never Been Found
Many problems belong to this category such as 0-1 Knapsack, the Sum-of Subsets, Traveling Salesperson, m-Coloring, Hamiltonian Circuits, etc.
There is a close and interesting relationship among many of the problems in this category.
_The development of this relationship is the purpose of the next section._

## The Theory of NP



