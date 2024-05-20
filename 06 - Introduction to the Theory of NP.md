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

### 3 - Problems That Have Not Been Proven to be Intractable, But for Which No Polynomial-Time Algorithms Have Never Been Found
Many problems belong to this category such as 0-1 Knapsack, the Sum-of Subsets, Traveling Salesperson, m-Coloring, Hamiltonian Circuits, etc.
There is a close and interesting relationship among many of the problems in this category.
_The development of this relationship is the purpose of the next section._

## The Theory of NP
It would be more convenient to develop the theory of NP by restricting ourselves to decision-problems only where the output of a decision problem is a simple “yes” or “no” answer. In general, each optimization problem has a corresponding decision problem. For example:
The Traveling Salesperson Decision problem is to determine, for a given positive number "d", whether there is a tour having total weight no greater than "d".
This problem has the same parameters as the Traveling Salesperson Optimization problem, plus the additional parameter "d".

For the Traveling Salesperson problem, we have not found a polynomial-time algorithms for either:
1. The decision problems
2. The optimization problems
   
If we could find a polynomial-time algorithm for the optimization problem,
then we would also have a polynomial-time algorithm for the corresponding decision problem.
That is because a solution to an optimization problem produces a solution to the corresponding decision problem.

### The Sets S and P
```P```
“P" is the set of all decision problems that can be solved by a polynomial-time algorithms. All decision problems for which we have found a polynomial-time algorithms are certainly in the set "P".
For example, searching an array:
- The problem of determining whether a key is present in an array
- The problem of determining whether a key is present in a sorted array

And other decision problems corresponding to several optimization problems we have seen are in the set "P"

_Can a decision problem for which we have not found a polynomial-time algorithm also be in "P"?_
An example is the Traveling Salesperson problem: The answer is un-known for now, and it is the 1 million dollar question of whether P = NP.

Even though no one has ever created a polynomial-time algorithm that solves this problem, no one has ever proven that it cannot be solved with a polynomial time algorithm.
**Therefore, it could possibly be in the set "P".**
To know that a decision problem is not in "P", we have to prove that it is not possible to develop a polynomial-time algorithm for this decision problem
There are relatively few decision problems which we know are not in “P"

```NP```
NP represents the class of decision problems which can be solved in polynomial time by a non-deterministic model of computation.
A non-deterministic model can make the right guesses on every move and race towards the solution much faster than a deterministic model.
i.e. A problem is solvable in polynomial-time on a non-deterministic model of computation

A deterministic machine, at each point in time, executes an instruction.
Depending on the outcome of executing the instruction, it then executes some next instruction, which is unique, and so on…

A non-deterministic machine, on the other hand, has a choice of next steps. It is free to choose any one that it wishes.
For example, it can choose a next step that leads to the best solution for the problem.
It may also produce a “nonsense” solution.

>In set “P” we find a solution in polynomial-time
>
>In set “NP” we verify a solution in polynomial-time

Suppose someone claimed to know that the answer to some instance of the decision problem version of TSP was “yes”.
That is, the person said that, for some graph and number "d", a tour existed in which the total weight was no greater than "d".
It would be reasonable for us to ask the person to “prove” this claim by actually producing a tour with a total weight no greater than "d".
If the person then produced something, we could write an algorithm to verify whether what he produced was a tour with weight no greater than "d".
The input to the algorithm is:
- The graph "G“
- The distance "d“ and
- The string "S" that is claimed to be a tour with weight no greater than “d”

```
bool verify (weighted_digraph G, number d, claimed_tour S) {
   if (S is a tour && the total weight of the edges in S is <= d)
      return true;
   else
      return false;
}
```

Returning false means only that this claimed tour is not a tour with total weight no greater than “d” and **_does not mean that such a tour does not exist_**, because there might be a different tour with total weight no greater than “d”.
It is not hard to prove that this verification algorithm runs in polynomial time.

To decide if a problem is in the set NP we need 2 things:
- A non-deterministic algorithm that solves a problem in polynomial-time
- A deterministic algorithm that verifies a claimed solution in polynomial-time

It is this property of polynomial-time verifiability that is possessed by the problems in the set NP.
This does not mean that these problems can necessarily be solved in polynomial time:
When we verify that a candidate tour has total weight no greater than "d", we are not including the time it took to find that tour.
We are only saying that the verification part takes polynomial time.

**A non-deterministic algorithm is composed of two separate stages:**
- Guessing Stage:	non-deterministic in polynomial-time
- Verification Stage: deterministic also in polynomial-time

**Guessing Stage – Non-Deterministic:**

Given an instance of a problem:
This stage simply produces some string "S“ in a non-deterministic manner.
The string can be thought of as a guess at the solution.
However, it could just be a string of nonsense.

**Verification Stage – Deterministic:**

The instance and the string "S" are the input to this stage.
This stage then proceeds in an ordinary deterministic manner.
Either: 
- Halting with an output of “true” OR
- Halting with an output of “false” OR
- Not halting at all

## NP Complete Problems
The following problems may not appear to have the same difficulty:
- The dynamic programming algorithm for the TSP is worst-case theta(n<sup>2</sup>2<sup>n</sup>)
- The dynamic programming algorithm for the 0–1 Knapsack problem is worst-case theta(min(2<sup>n</sup>, nW))
- The state space tree in the branch-and-bound algorithm for the TSP has (n – 1)! leaves
- The state space tree in the branch-and-bound algorithm for the 0 – 1 Knapsack problem has 2n + 1 nodes

It may seem that the 0 – 1 Knapsack problem is inherently easier than the Traveling Salesperson problem, however we show that these two problems, and thousands of other problems, are all equivalent in that if one is in "P", they must all be in "P".
**These problems are called NP-complete.**

Suppose we want to solve decision problem "A", and we have an algorithm that solves decision problem "B". Suppose further that we can write an algorithm that creates an instance "y" of problem "B" from every instance "x" of problem "A" such that an algorithm for problem "B" answers “yes” for "x".
Such an algorithm is called a transformation algorithm.

- If there exists a polynomial-time transformation algorithm from decision problem "A" to decision problem "B", we say that problem "A" reduces to problem "B"
- If decision problem "B" is in "P" and decision problem "A" reduces to "B", then "A" is also in "P"

A problem "B" is called NP-Complete if both of the following are true:
- "B" is in NP
- For every other problem "A" in NP, A reduces to "B"

If we could show that any NP-complete problem is in "P", we could conclude that P = NP

In 1971 Stephen Cook managed to prove that CNF-Satisfiability is NP-complete.
The proof does not consist of reducing every problem in NP individually to CNF Satisfiability; instead it exploits common properties of problems in NP to show that any problem in this set must reduce to CNF-Satisfiability

## Theorem
A problem "C" is NP-complete if both of the following are true:
- "C" is in NP
- For some other NP-complete problem "B", "B" reduces to "C"

**Examples of NP-Complete Problems:**
1. Clique Decision Problem:
Given a graph and an integer "k", are there "k" vertices in the graph, which are all adjacent to each other?
CNF-Satisfiability reduces to Clique Decision Problem

2. Hamiltonian Circuits Decision Problem because CNF-Satisfiability reduces to it
3. TSP decision problem (undirected) as Hamiltonian Circuits Decision Problem reduces to it
4. TSP decision problem as TSP decision problem (undirected) reduces to it

**How does the set of NP-complete problems fit into the picture?**

First, by definition, it is a subset of NP.
Therefore, Presburger Arithmetic, the Halting problem, and any other decision problems that are not in NP are not NP-complete.
A decision problem that is in NP and is not NP-complete is the trivial decision problem that answers “yes” for all instances (or answers “no” for all instances).
This problem is not NP-complete because it is not possible to transform a nontrivial decision problem to it.

If P ≠ NP, then P ∩ NP-Complete = Ჶ

This is so because, if some problem in "P" were NP-complete, this would imply that we could solve any problem in NP in polynomial time.

Theorem:
If P ≠ NP, the set NP – (P 𝖴 NP-Complete) is not empty
