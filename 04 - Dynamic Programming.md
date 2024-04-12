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

```int arr[n] = {0, 1, x, x, x, ..., n-1};```

We then iterate through the array without the base cases (positions 0 and 1)
```
for (int i=2; i<n; i++) {
  arr[i] = arr[i-1] + arr[i-2];
}
return arr[n-1];
```
This approach takes a linear time O(n) and space complexity o(n), making it a 
lot more efficient than
a recursive function.

## The Binomial Coefficient
## Floyd Warshall's Algorithm for Shortest Path
## Dynamic Programming and Optimization Problems
## Chained Matrix Multiplication
## OPtimal Binary Search Tree
## The Traveling Salesperson Problem
