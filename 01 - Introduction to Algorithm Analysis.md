# Chapter 01: Introduction to Algorithm Analysis

**Why study algorithms?** An algorithm is a set of instructions that aim to solve a problem. It is a finite, step-by-step sequence used to accomplish a task. 
It is important for us to study algorithms because it plays an important role in 
modern technological innovations, and allows us to improve existing algorithms to better their performance.

**Developing Efficient Algorithms is important** because no matter how advanced, fast, or large (in MEM) computers may get, a badly executed algorithm may hinder the performance.
That is why efficiency should always be taken into consideration when developing a program.

## Algorithm Analysis:
### Algorithm Efficiency:
It is the amount of time an algorithm needs to finish executing a certain input.
An algorithm is 'efficient' if its running time is a polynomial function.

### Growth rate function:
Given 2 functions f(n) and g(n), we say:
- f(n) = O g(n) _if and only if_ there exists a constant C and a positive integer n so that f(n) ≤ c.g(n)
- We say that f(n) = ∑ g(n), indicationg that g(n) is the minimum value that f(n) can be, therefore f(n) ≥ g(n)
- Assume we have 3 funcions f(n), g<sub>1</sub>(n), and g<sub>2</sub>(n). We say that f(n) = Ω g(n), indicating that f(n)
  lies between g<sub>1</sub>(n) and g<sub>2</sub>(n). THEREFORE:
  c<sub>1</sub>g<sub>1</sub> ≤ f(n) ≤ c<sub>2</sub>g<sub>2</sub>(n)

### Calculating the Time Complexity:
Given the above formulae, we can calculate the time complexity by computing n.
> Example: Assume that f(n) = 5n<sup>2</sup>+4. Calculate O(n).
>> Solution: g(n) = n<sup>2</sup>, since f(n) = O(n<sup>2</sup>)
>> f(n) ≤ c.g(n)
>> 
>> 5n<sup>2</sup>+4 ≤ c(n<sup>2</sup>)      let c=b
>> 
>> 5n<sup>2</sup>+4 ≤ b(n<sup>2</sup>)
>> 
>> n<sup>2</sup> ≥ 4, then n ≥ 2
>> 
>> So, for all n≥2 & c=b, f(n) = O(n<sup>2</sup>)

### Time Complexity for Different Loop Types:
1. Single For-Loop: the amount of times the sum of the statements inside the blocks are going to get executed
2. Nested For-Loop: running time for each loop multiplied by each other
3. If-else statement: sum of the condition statement & the block that has more LOC
