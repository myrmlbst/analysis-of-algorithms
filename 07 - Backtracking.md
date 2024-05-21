# 07 - Backtracking

## Overview
Backtracking signifies going back and undoing a step after realizing that it leads to a dead end. It's like trying to find your way out in a maze. Signs that a path leads to a dead end help facilitate the process of backtracking and are thus used when figuring out the traversal that needs to be taken. 

An example of this would be the 0-1 Knapsack Problem, which we can solve via backtracking.
There are 2n subsets, which means that this brute-force method is feasible only for small values of "n".
However, if while generating the subsets, we can find signs that tell us that many of them do not need to be generated, we can often avoid unnecessary labor.
Backtracking algorithms for problems such as the 0-1 Knapsack problem are still exponential-time in the worst case.

Backtracking is useful because it is efficient for many large instances of a problem, NOT because it is efficient for all large instances.

## The Backtracking Technique
**Definition:** Backtracking is used to solve problems in which a sequence of objects is selected from a specified set so that the sequence satisfies some criterion.

**Example:** The n-queens problem

The goal of the n-queens problem is to position "n" queens on an n x n chessboard so that no two queens threaten each other,
i.e., No two queens can be in the same row, column, or diagonal.
The sequence is going to be the “n” position where we are going to position these “n” queens.
The set is going to be the n<sup>2</sup> possible position where we can place them.
The criterion is going to be no two queens can be in the same row, column, or diagonal.

Backtracking is a modified depth-first search of a rooted tree.
A preorder tree traversal is a depth-first search of a tree.
A depth-first search does not require that the children be visited in any particular order.
For the sake of consistency, we will visit the children of a node from left to right.
Notice that in a depth-first search, a path is followed as deeply as possible until a dead end is reached.
At a dead end, we back up until we reach a node with an unvisited child, and then we again proceed to go as deep as possible.

**Simple Recursive Algorithm for DFS:**
```
void depth_First_Tree_Search (node v)
{
   node u;
   visit v;
		
   for (each child u of v)
   // revisit “u” using a depth first search
   depth_First_Tree_Search ( u );	
}
```

To return to the n-Queens problem: when n = 4,
our task is to position four queens on a 4 x 4 chessboard so that no two queens threaten each other.
We already know that no two queens can be in the same row.
The instance can be solved by assigning each queen a different row and checking which column combinations yield solutions.
In this case there are: ```4 ∗ 4 ∗ 4 ∗ 4 = 256 candidate solutions```
If we have an n x n chessboard, what is the number of candidate solutions?
- n<sup>n</sup> which is supper exponential, i.e. worse than factorial

We can create the candidate solutions by constructing a tree in which the column choices for the first queen (in row 1) are stored in level-1 nodes in the tree.
The column choices for the second queen are in level-2 nodes, and so on...
If we have a path from the root to the leaf, then it is a candidate solution.
This tree is called a state space tree

**Note:** for a 4 x 4 chessboard we are going to have 5 levels in the state space tree. The root is at level 0, level 1 represents where we place Q1, level 2 represents where we place Q2, and so on...

A simple depth-first search of a state space tree is like following every path in a maze until you reach a dead end. It does not take advantage of any signs along the way.

**We can make the depth-first search more efficient:**

_No two queens can be in the same column,_ meaning that there is no point in constructing and checking any paths in the entire branch where the othe queen already is.

_No two queens can be in the same diagonal,_ meaning that the same rules as before apply.

We call a node non-promising if we can determine that it cannot possibly lead to a solution.
If there is a potential that a solution might be found, we call the node promising.

So, tos um it up, backtracking consists of doing a depth-first search of a state space tree by 
1. Checking whether each node is promising
2. If it is non-promising, backtrack to the node’s parent (this process is called "pruning". A subtree consisting of the visited nodes is called the pruned state space tree)

**General Algorithm for Backtracking:**
```
void checkNode (node v) {
   node u;

   if (promising(v)) {
      if (there is a solution at v) {
         write the solution;
      }
      else {
         for (each child u of v) {
            checkNode(u);
         }
      }
   }
}
```

The root of the state space tree is passed to “checknode“ at the top level.
A visit to a node consists of first checking whether or not it is promising.
If it is promising and there is a solution at the node, then the solution is printed.
If there is not a solution at a promising node, the children of the node are visited.
The function promising is different in each application of backtracking:
For the n-Queens problem, it must return false if a node and any of the node’s ancestors place queens in the same column or diagonal.
Unlike the n-Queens problem algorithm, in some backtracking algorithms a solution can be found before reaching a leaf in the state space tree.

_Notice that a backtracking algorithm does not need to actually create a tree. We say that the state space tree exists implicitly in the algorithm because it is not actually constructed._

**You may have observed that there is some inefficiency in our general algorithm for backtracking (procedure "checknode”).**
That is, we check whether a node is promising after passing it to the procedure.
This means that activation records for non-promising nodes are unnecessarily placed on the stack of activation records.
We could avoid this by checking whether a node is promising before passing it by comparing the first algorithm with the new one.
We use the aforementioned version to explain the **majority** of backtracking algorithms due to its simplicity.

**New Algorithm:**
```
void expand (node v) {
   node u;

   for (each child u of v) {
      if (promising(u)) {
         if (there is a solution at u) {
            write the solution;
         }
         else expand(u);
      }
   }
}
```
Next, we will develop backtracking algorithms for several problems, starting with the n-Queens problem.
In all these problems, the state space tree contains an exponentially large number of nodes.
**Backtracking is used to avoid unnecessary checking of nodes.**
Given two instances with the same value of "n", a backtracking algorithm may check very few nodes for one of them but the entire state space tree for the other.
This means that we will not obtain efficient time complexities for our backtracking algorithms as we did for the algorithms in the preceding chapters

## The n-Queens Problem
The promising function must check whether or not two queens are in the same column or diagonal.
Let col(i) = x, then x is the column where the queen in the i<sup>th</sup> row is located.
Then, to check whether the queen in the kth row is in the same column as the queen int the ith row, we need to check whether col(i) = col(k)

### Backtracking Algorithm For the n-Queen Problem:
- Problem: Position n Queens on a chessboard so that no two queens are in the same _row_, _column_, or _diagonal_.
- Input: positive integer n
- Output: All possible ways n Queens can be placed on nxn chessboard so that no two Queens threaten each other.

Each output consists of a 1-D array of integers “col” indexed from 1 to n where col[i] is the column where the Queen in the i<sup>th</sup> row is placed.

```
void queens (index i) {
   index j;

   if (promising(i)) {
      if (i == n) {
         print "col[1] through col[n]";
      }
      else {
         for (j=1; j<=n; j++) {
            col[i+1] = j;
            queens(i+1);
         }
      }
   }
}


bool promising (index i) {
   index k = 1;

   bool SWITCH = true;

   while (k<i && SWITCH) {
      if (col[i] == col[k] || abs(col[i]-col[k]) == i-k) {
         SWITCH = false;
      }
      k++;
   }

   return SWITCH;
}
```

The top-level call to queens would be: queens(0).
It is difficult to analyze the algorithm theoretically
To do this, we have to determine the number of nodes checked as a function of “n”, the number of queens.
We can get an upper bound on the number of nodes in the pruned state space tree by counting the number of nodes in the entire state space tree. The total number of nodes is:

1 + n + n<sup>2</sup> + n<sup>3</sup> + ... + n<sup>n</sup> = (n<sup>n+1</sup> - 1) / (n-1)

This analysis is of limited value because the whole purpose of backtracking is to avoid checking many of these nodes.

Another analysis we could try is to obtain an upper bound on the number of promising nodes. To compute such a bound, we can use the fact that no two queens can ever be placed in the same column. The number of promising nodes is bounded above by:

1 + n + n(n-1) + n(n-1)(n-2) + ... = n! promisisng nodes

This analysis does not give us a very good idea as to the efficiency of the algorithm for the following reasons:
- First, it does not take into account the diagonal check in function promising. Therefore, there could be far less promising nodes than this upper bound.
- Second, the total number of nodes checked includes both promising and non-promising nodes. The number of non-promising nodes can be substantially greater than the number of promising nodes.
