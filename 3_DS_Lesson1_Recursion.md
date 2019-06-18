# 2. Data Structures

## Lesson 3: Recursion 

---

### 1. Recursion introduction

Recursion is a technique for solving problems where the solution to a particular problem depends on the solution to a smaller instance of the same problem. 

Consider the problem of calculating $\mathtt{2^5}$. Let's assume to calculate this, you need to do one multiplication after another. That's $2 * 2 * 2 * 2 * 2$. We know that $2^5 = 2 * 2^4$. If we know the value of $2^4$, we can easily calculate $2^5$.

We can use recursion to solve this problem, since the solution to the original problem ($2^n$) depends on the solution to a smaller instance ($2^{n-1}$) of the same problem. The recursive solution is to calculate $2 * 2^{n-1}$ for all n that is greater than 0. If n is 0, return 1. We'll ignore all negative numbers.

Let's look at what the recursive steps would be for calculating $2^5$.

$2^5 = 2 * 2^4$

$2^5 = 2 * 2 * 2^3$

$2^5 = 2 * 2 * 2 * 2^2$

$2^5 = 2 * 2 * 2 * 2 * 2^1$

$2^5 = 2 * 2 * 2 * 2 * 2 * 2^0$

$2^5 = 2 * 2 * 2 * 2 * 2 * 1$

Let's look at the recursive function `power_of_2`, which calculates $2^n$. 

```Python
def power_of_2(n):
    if n == 0:
        return 1
    
    return 2 * power_of_2(n - 1)

print(power_of_2(5))
```
As you can see, the function calls itself to calculate the smaller instance of the solution. Let's break down the `power_of_2` function, starting with the first two lines.
```
if n == 0:
    return 1
```
These lines contain the base case. This is where you catch edge cases that don't fit the problem ($2 * 2^{n-1}$). Since we aren't considering any $n < 0$ valid, $2 * 2^{n-1}$ can't be used when $n$ is $0$. This section of the code returns the solution to $2^0$ without using $2 * 2^{n-1}$.
```
return 2 * power_of_2(n - 1)
```
This code is where it breaks the problem down into smaller instances. Using the formula $2^{n} = 2 * 2^{n-1}$, the `power_of_2` function calls itself to calculate $2^{n-1}$. To better understand what is happening, let's look at the call stack with an example.

