# Chapter 02 - The Divide and Conquer Approach

## Introduction
As the name suggests, the divide and conquer approach is a **top-down** method used to solve problems by dividing it into smaller parts and tackling each sub-problem seperately.
The algorithms used in this approach are: binary search, merge sort, and quick sort.

## Calculating Time Complexity
To analyze the running time of the divide and conquer algorithm, we need to solve the recurrence equation. The recurrence equation describes a function in terms of its input.
Since we're using this recurrence for the divide and conquer approach, we use the **master theorem.**

### The Master Theorem:
**General Form:** ```T(n) = aT(n/b) + f(n)``` where variable a is the number of sub-problems, n/b is the size of each problem, and f(n) is the cost of the work that has to be done outsode of the recursive calls.

**Example of case 1:** ```T(n) = 2T(n/2) + n``` a=2, b=2, f(n)=n. Calculate n.log<sub>b</sub>a => n.log<sub>2</sub>(2), then n=f(n). We conclude that the cost is everything distributed throughout the tree.
T(n) = O(log<sub>b</sub>(n).log(n)) = O(n.log(n)).

**Example of case 2:** ```T(n) = 9T(n/3) + n``` a=9, b=3, f(n)=n. Calculates nlog<sub>b</sub>(a) => n.log<sub>3</sub>(9) = n<sup>2</sup>, then n<sup>2</sup> > f(n). We conclude that the cost is dominated by the cost of the leaves.
T(n) = O(n.log<sub>b</sub>(a)) = O(n<sup>2</sup>).

**Example of case 3:** ```T(n) = 3T(n/4) + nlogn(n)``` a=3, b=4, f(n)=n.logn. Calculate n.log<sub>b</sub>(a) = n.log<sub>4</sub>(3) = n<sup>0.789</sup>, then n<sup>0.789</sup> < n.log(n).
We conclude that the cost is dominated by the cost at the root. Nowe we need to calculate the regularity to see if it holds. This is done by checking a.f(n/b) ≤ c.f(n) where c<1.
> 3(n/4).log(n/4) < c.f(n)
>
> 3/4(log(3/4)) < c.f(n) => for c=2/4, it holds
>> T(n) = O(f(n)) = O(n.log(n))

## Binary Search
The binary search algorithm tries to locate a key x in an array where the array must be sorted in an incremental order.

**How it works:**
- Step 1: Find the middle item of an array
- Step 2: Check if the middle element is equal to the key (if yes, the objective is done. if not, we divide said array into 2 parts)
- Step 3: Check if x is less or greater than the middle element (if x<mid, go to the left. if x>mid, go to the right part)
- Step 4: Repeat the previous step until key x is found

**Recurrence Equation for Binary Search:**
- The recurrence equation for binary search tree is ```T(n) = T(n/2) + 1```
- According to the master theorem, the time complexity is O(logn)
- Another method to calculate its time complexity is:
  
  > EQ1: T(n) = T(n/2) + 1
  > 
  > EQ2: T(n/2) = T(n/4) + 1 => we substitute n in the above equation with n/2
  > 
  > T(n) = [T(n/4)+1] + 1 = T(n/2<sup>2</sup>)+2 => substitute equation 2 in 1
  > 
  > Repeat both substitutions. Eventually, we'll have T(n) = T(n/2<sup>i</sup>) + i
- Since the run time of having 1 element in an array is 1, then T(1)=1
- No matter our input, it's going to keep diminishing until it reaches 1 => let n/2<sup>i</sup>=1 => n=2<sup>i<sup>
- To find the value of i, we do:
  > n=2<sup>i</sup> => log<sub>2</sub>(n) = log<sub>2</sub>(2<sup>i</sup>) = i.log<sub>2</sub>2
  >
  > i = log(n)/log<sub>2</sub>2 = log<sub>2</sub>(n)/1
- Now if we substitute n and i, we get O(log(n))

## Merge Sort
Merge sort is an algorithm that uses the divide and conquer approach to sort an array. Note that it is NOT an in-place algorithm.

**How it works:**
- Step 1: Divide the array into 2 equal parts
- Step 2: Keep dividing each part of the array until each one of them only contains 2 elements
- Step 3: Sort the elements of each of these parts
- Step 4: Combine them while sorting them until we end up with a sorted array

**Recurrence Equation for Merge Sort:**
- The recurrence equation for binary search tree is ```T(n) = 2T(n/2) + n```
- According to the master theorem, the time complexity is O(n.log(n))
- If we follow the same steps mathematically, we get the same time complexity

## Counting Inversions
Counting inversions is an algorithm applied on arrays that returns number of pairs in an array that obey these rules:
1. left element > right element
2. index of left element < index of right element

```Example: [1,3,5,2,4,6] => (3,2);(5,2);(5,4) => this array has 3 inversions```

If an array is sorted, it has 0 inversions

**Number of Inversions:** To figure out how many inversions an array can have, regardless of the value of its elements, we use ```n(n-1) / 2``` where n = length. 
For example, in an array of 6 elements, ```6(6-1)/2 = 15 inversions```

**How it works:**
We could simply use a nested for-loop with a running time of O(n<sub>2</sub>), but that is a brute force algorithm.
It is preferable for us to use the divide and conquer approach Merge Sort.
- Split the array into 2 and apply counting inversion on each side


Run time for this algorithm is ```O(n.log(n))```

## Quick Sort
Quick sort is the most efficient sorting algorithm that falls under the 'divide and conquer' methodology.

**How it works:**
- Step 1: Choose a pivot element. This element coukd be any element in the array
- Step 2: Split the array into 2 parts:
  - Left has all the elements smaller than the pivot
  - Right has all the elements larger tha the pivot
- Step 3: Steps are repeated until each part has only 1 element

**Note:** By default, when each part only has 1 element, the array would become sorted.

**Recurrence Equation for Quick Sort:**
- If an array is split in the middle:
  ```T(n) = 2T(n/2) + O(n)``` where n/2 is the cost of dividing, and O(n) is the cost of positioning

  Time Complexity = O(n.log(n))
- If an array is presorted:
  ```T(n) = T(n-1) + O(n)```

  Time Complexity = O(n<sup>2</sup>)
- If pivot is chosen randomly => Time Complexity = O(n.log(n))

## Maximum Subsequence Sum Problem
If we are given an array of integers that could include negative values, how would we find a sequence in this array that would return to us the largest sum among all other sequences? We use the divide and conquer approach to find the maximum subsequence sum.

**How it works:**
- Step 1: Split array into 2 halves
- Step 2: Find the maximum subsequence in the left half, then the right half
- Step 3: Find the maximum subsequence of the entire array

Imagine we have an array [2,3,-1,-8,4,11,5,-2,7,1,-3]. The maximum subsequence sum would be [4,11,5,-2,7,1].

**Recurrence Equation for Maximum Subsequence Sum:**
- T(n) = 2T(n/2) + O(n)
- Time Complexity = O(nlog(n))

## Strassen's Algorithm for Matrix Multiplication
Strassen's Matrix Multiplication is an algorithm used to calculate 2 square matrices. Each matrix is of size nxn, so they can be represented by a 2D array.

**How Matrix Multiplication works:**
- Step 1: Ensure that both matrices are of the same dimensions
- Step 2: Multiply the row in Matrix 1 by the column in Matrix 2, then add up these two products
- Step 3: Repeat for all rows in the matrices
```
A1 A2  *  B1 B2  =  A1B1  A2B2

A3 A4  *  B3 B4     A3B3  A4B4
```
Example:
```
A = 2 1 3    B = 5 6 2    AB = 23 23 17
    3 4 2        7 8 4         47 52 28
    1 2 0        2 1 3         19 22 10
```

**How Strassen's Algorithm for Matrix Multiplication works:**
- _Divide and conquer approach:_ each matrix is divided into multiple submatrices until they're simplified to the point where we can solve them using simple formulae
```
Example:
Let A = 1 3    B = 6 8
        7 5        4 2

=> M1 = (A1,1 + A2,2)(B1,2 + B2,2) = (1+5)(6+2) = 48
=> M2 = (A2,1 + A2,2)(B1,1) = (7+5)(16) = 72
=> M3 = (A1,1)(B1,2 - B2,2) = (1)(8-2) = 6
=> M4 = (A2,2)(B2,2 - B2,1) = (5)(4-6) = 10

Then, we use the following formula to find the results:
C1,1 = M1+M4-M5+M7        C1,2 = M3+M5
C2,1 = M2+M4              C1,2 = M2+M3-M2+M4
...
18  14
62  66
```
**Recurrence Equation:**
- T(n) = 7T(n/2) + cn<sup>2</sup>

## Arithmetic with Large Integers
Large integers are numbers that are so big they exceed the hardware's capabilities of representing them. There are two ways to represent them:
1- Straightforward method (using an array of int where each array represents a digit)
2- Divide and Conquer method:
  - Split the integer into 2 (one with ceiling, one with floor)
  - Divide the integers until they're easy to multiply
  - Formula: U = x.10<sup>n</sup>.y, where x=n/2 ceiling digits, y=n/2 floor digits, n=n/2 floor digits
    Using this formula, we find the equation for each large integer.
    ```
    Example: 567,832 x 9,423,723
    => 567,823 = 567 x 10^3 + 832
    => 9,423,723 = 9423 x 10^3 + 723
    => Therefore, (567 x 10^3 + 832) x (9423 x 10^3 + 723)
    ```

**Recurrence Equation:**
- T(n) = 4T(n/2) + Cn
- Time Complexity = O(n<sup>2</sup>)
**Finding the Recurrence Equation from Code:**
The general formula is ```T(n) = aT(n/b) + f(n)``` where n is the size of the input, a is the number of times the function calls itself, n/b is the size of each subproblem, and f(n) is the cost of what has to be done outside the subproblem (for example, during dividing and merging). Knowing that, we can now conclude the recurrence equation when reading code.

Note that we should **not** use the divide and conquer approach when dealing with large integers if after dividing an instance of size n, the sizes of the sub-instances remain almost the same size OR when we have too many sub-instances.
