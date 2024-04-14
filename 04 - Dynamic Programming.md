# Chapter 04 - Dynamic Programming

## Overview
Dynamic programming tackles real life problems similarly to the divide and conquer
approach, and that is by dividing a task into smaller instances. However, unlike 
the divide and conquer algorithms, dynamic programming opts to solve
a problem using a **bottom-up approach**. We then solve these 
small instances first, store the results in an array/table, then look them up when we 
need them.

We use dynamic programming in situations where the divide and conquer algorithms
fails. In problems where the smaller instances are related, a divide and conquer
algorithm often ends up repeatedly solving common instances, making it highly
inefficient in certain scenarios. _For example: Solving a Fibonacci series._

## The Fibonacci Sequence
While we usually use a recursive function to calculate the Fibonacci number of a 
given integer, that approach is naive in a sense that _it takes up too much time
and space_.
A recursive function of, say, Fib(6) would first have to calculate Fib(5) and Fib(4).
Since it is recursive, it would then have to find Fib(5), resulting in Fib(4) and Fib(3).
There are two instances of Fib(4) where the Fibonacci sequence of 4 is being
recalculated multiple times in the same function, and that holds true for other
numbers that reappear multiple times and have to be recalculated many times, making
the program inefficient. Duplicates are being tackled twice when they could just be
calculated once and stored for later usage.

**To evade this problem, we use dynamic programming.** To find the Fibonacci sequence 
of a number using dynamic programming, we need to initialize an empty
array and fill up the first two positions so that they are set to 0 and 1;

```int Fib[n] = {0, 1, x, x, x, ..., n-1};```

We then iterate through the array without the base cases (positions 0 and 1)
```
for (int i=2; i<n; i++) {
  Fib[i] = Fib[i-1] + Fib[i-2];
}
return Fib[n-1];
```
This approach takes a linear time O(n) and space complexity O(n), making it a 
lot more efficient than
a recursive function.

## The Binomial Coefficient
This algorithm is used to calcuate the possibility of choosing one instance k out of n. 

Mathematically, to find the binomial coefficient, we use the following formula:
C(n,k) = <sup>n</sup>C<sub>k</sub> = n! / [β! . (n-β)!]
> So for example, <sup>5</sup>C<sub>3</sub> = 5! / 3!((5-3)!)
> 
> = 5x4x3x2x1 / (3x2x1)(2x1)
> 
> = 5x4 / 2x1
> 
> = 10

the code would look like this:
```
int bin(int n, int k) {
  if (k==0 || n==k) {
    return 1;
  }
  else return bin(n-1, k-1) + bin(n-1, k);
}
```

To find that same binomial coefficient of <sup>5</sup>C<sub>3</sub> using Dynamic Programming:


## Floyd Warshall's Algorithm for Shortest Paths
### All Pairs Shortest Path:
Finding the shortest path from each vertex to all other vertices in a graph is an optimization problem that has many applications. Since there may be more than one shortest path from one vertex to another, we can find any one of them. 

_(Note the language being used: Here we find 'A shortest path', signifying that other short paths possibly exist. Saying 'THE shortest path' suggests that there exists only one shortest path.)_

A shortest path must be a simple path where no cycling occurs, meaning that a path cannot pass through the same vertex twice. In the instance where we have multiple simple paths from one vertex to another, we should choose the one with the **minimum value.**

### Floyd's Algorithm for Shortest Paths
We define D<sup>k</sup>[i,j] to be the weight of the shortest path from V<sub>i</sub> to V<sub>j</sub> having considered all vertices between V<sub>1</sub> and V<sub>1</sub> as intermediates.

But first, we construct the weight matrix D<sup>0</sup> (using adjacency matrix) according to the folowing:
* D<sup>0</sup>[i,j] = w(i,j) if V<sub>i</sub> and V<sub>j</sub> have direct connection.
* D<sup>0</sup>[i,j] = ∞ if they are not connected
* D<sup>0</sup>[i,j] = 0
Then, we construct D<sup>1</sup> by using V<sub>1</sub> as an intermediate, then D<sup>2</sup> with V<sub>2</sub>, and so on.

* The shortest path between V<sub>i</sub> and V<sub>j</sub> = D<sup>n</sup> = D<sup>|V|</sup>[i,j]
* D<sup>0</sup> (adjacency matrix) is the input to Floys-Warshall's algorithm
* D<sup>n</sup> = D<sup>|V|</sup> = the first output ('n' = number of vertices)
* P = the second output ('P' = path matrix)
#### Dynamic Programming Methodology for Floyd's Algorithm for Shortest Path
STEP 1: Establish a recursive property with which we compute D<sup>k</sup> from D<sup>k-1</sup>. STEP 2: Solve an instance of the problem in a bottom-up way by repeating Step 1 from k=1 to n=k.
> Time Complexity = O(n<sup>3</sup>)

## Dynamic Programming and Optimization Problems
If the **principle of optimality** applies to a certain problem, then you can use dynamic programming to solve it. The prerequisites to developing a dynamic algorithm are (1) determining the shortest path(s), (2) constructing it. Only then can we construct an optimal solution by doing the following:
* Establishing a recursive property that gives the optimal solution to an instance of a problem
* Computing the value of an optimal solution using a bottom-up method
* Constructing an optimal solution (also using a bottom-up method)

Although it may seem like any optimization problem can be solved using dynamic programming, the principle of optimality MUST apply to the problem for us to be able to use DP to solve it. **The Principle of Optimality** states that an optimal solution to an instance of a problem always contains optimal solutions to all sub-instances.

## Chained Matrix Multiplication
The Matrix Chain-Product: A = A<sub>1</sub> * A<sub>2</sub> * ... * A<sub>n</sub> such that A<sub>i</sub> has a dimension d = d<sub>i-1</sub> * d<sub>i</sub>.
> Example:
>> d of B = 3*100
>>
>> d of C = 100*5
>>
>> d of D = 5*5
>
> - (B*C)*D = 1575 operations
>
> - B*(C*D) = 4000 operations
>
> The goal is to develop the optimal order for multiplying “n“ matrices. So, it is better to start with (B*C)*D

### Matrix Chain Product Algorithm
#### Brute Force Approach
We try all possible ways to parenthesize A = A<sub>1</sub> * A<sub>2</sub> * ... * A<sub>n</sub> and calculate the number of operations required for each one. The order that results in the minimum number of operations is our final answer. **The running time** of this algorithm is _at least_ **exponential.** The principle of optimality applies to this problem, so we can use dynamic programming to find a solution.

### Optimized Approach
We use a sequence of 2-D arrays. 

## Optimal Binary Search Tree
## The Traveling Salesperson Problem
