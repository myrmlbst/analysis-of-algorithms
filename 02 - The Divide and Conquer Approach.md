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

**Recurrence Equation for Binary Search:**
- The recurrence equation for binary search tree is ```T(n) = 2T(n/2) + n```
- According to the master theorem, the time complexity is O(n.log(n))
- If we follow the same steps mathematically, we get the same time complexity
