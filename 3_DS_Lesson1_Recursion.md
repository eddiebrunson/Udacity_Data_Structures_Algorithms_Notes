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

**Call Stack** 

Let's follow the call stack when calling `power_of_2(5)`:

First `power_of_2(5)` is called `power_of_2(4)`

Then `power_of_2(5)` calls `power_of_2(3)`

Then `power_of_2(4)` calls `power_of_2(3)`

...

Then `power_of_2(1)` calls `power_of_2(0)`

At this point, the call stack will look something like this:

   ...
   
   File "<ipython-input-27-9e8459c7465f>", line 5, in power_of_2
    return 2 * power_of_2(n - 1)
  File "<ipython-input-27-9e8459c7465f>", line 5, in power_of_2
    return 2 * power_of_2(n - 1)
  File "<ipython-input-27-9e8459c7465f>", line 5, in power_of_2
    return 2 * power_of_2(n - 1)
  File "<ipython-input-27-9e8459c7465f>", line 5, in power_of_2
    return 2 * power_of_2(n - 1)
  File "<ipython-input-27-9e8459c7465f>", line 3, in power_of_2
    return 1
Let's look at a cleaner view of the stack:

...
    -> power_of_2(5)
        -> power_of_2(4)
            -> power_of_2(3)
                -> power_of_2(2)
                    -> power_of_2(1)
                        -> power_of_2(0)
Each function is waiting on the function it called to complete. So, `power_of_2(5)` is waiting for `power_of_2(4)`, power_of_2(4) is waiting for `power_of_2(3)`, etc..

The function `power_of_2(0)` will return  1 
Using the 1 returned from `power_of_2(0)`, `power_of_2(1)` will return  2∗1 
Using the 2 returned from `power_of_2(1)`, `power_of_2(2)` will return  2∗2 
...

Using the 16 returned from `power_of_2(4)`, `power_of_2(5)` will return  2∗16 

Finally, the result of  25  is returned!  25=2∗24=2∗16=32

**Practice Problem**

___

Implement `sum_integers(n)` to calculate the sum of all integers from 1 to n using recursion. For example, `sum_integers(3)` should return 6(1 + 2 +3).

```Python 
def sum_integers(n):
    pass
```

<details><summary><b>Solution</b></summary>
<p>

```Python 
def sum_integers(n):
    if n == 1:
        return 1
    
    return n + sum_integers(n -1)

print(sum_integers(3))
```
</p>
</details>

___

**Gotchas**

When using recursion, there are a few things to look out for that you don't have to worry about when running a loop (iteratively). Let's go over a few of those items. 

**Call Stack**

We went over an example of the call stack when calling `power_of_2(5)` above. In this section, we'll cover the limitations of recursion on a call stack. The following code below when run will create a really large stack. It should raise the error `RecursionError: maximun recursion depth exceeded in comparison.`

```Python 
print(power_of_2(10000))
```
Python has a limit on the depth of recursion to prevent a [stack overflow](https://en.wikipedia.org/wiki/Stack_overflow). However, some compliers will turn [tail-recursive functions]( https://en.wikipedia.org/wiki/Recursion_(computer_science)#Tail-recursive_functions) into an iterative loop to prevent recursion from using up the stack. Since Python's complier doesn't do this, you'll will have to watch out for this limit. 

**Slicing**

Let's look at recursion on arrays and how you can run into the problem of slicing the array. If you haven't heard the term slicing, it's the operation of taking a sunset of some data. For example, the list `a` can be sliced using the following operation: `a[start:stop]`. This will return a new list from index `start` (inclusive) to index `stop` (exclusive).

Let's look at an example of a recursive function that takes the sum of all numbers in an array. For example, the array of `[5, 2, 9, 11]` would sum to 27 (5 + 9 + 11).

```Python
def sum_array(array):
    # Base Case
    if len(array) == 1:
        return array[0]
    
    return array[0] + sum_array(array[1:])

arr = [1, 2, 3, 4]
print(sum_array(arr))
```

Looking at this, you might think it has a running time of O(n), but that isn't correct due to the slice operation `array[1:]`. This operation will take **O(k)** time to run where k is the number of elements to copy. So, this function is actually **O(k * n)** running time complexity and **O(k * n)** space complexity.

To visualize this, let's plot the time it takes to slice. 

```Python
import matplotlib.pyplot as plt
import statistics
import time
%matplotlib inline

n_steps = 10
step_size = 1000000
array_sizes = list(range(step_size, n_steps*step_size, step_size))
big_array = list(range(n_steps*step_size))
times = []

# Calculate the time it takes for the slice function to run with different sizes of k
for array_size in array_sizes:
    start_time = time.time()
    big_array[:array_size]
    times.append(time.time() - start_time)

# Graph the results
plt.scatter(x=array_sizes, y=times)
plt.ylim(top=max(times), bottom=min(times))
plt.xlabel('Array Size')
plt.ylabel('Time (seconds)')
plt.plot()
```
As you can see, it's **linear time** to slice. 

Instead of slicing, we can pass the index for the element that we want to use for addition. That will give us the following function:

```Python 
def sum_array_index(array, index):
    # Base Cases
    if len(array) - 1 == index:
        return array[index]
    
    return array[index] + sum_array_index(array, index + 1)

arr = [1, 2, 3, 4]
print(sum_array_index(arr, 0))
```
That eliminates the need to do slicing. With the two different functions implemented, let's compare the running times. 

```Python
import matplotlib.pyplot as plt
import statistics
import time

n_steps = 10
step_size = 200
array_sizes = list(range(step_size, n_steps*step_size, step_size))
big_array = list(range(n_steps*step_size))
sum_array_times = []
sum_array_index_times = []

for array_size in array_sizes:
    subset_array = big_array[:array_size]
    
    start_time = time.time()
    sum_array(subset_array)
    sum_array_times.append(time.time() - start_time)
    
    start_time = time.time()
    sum_array_index(subset_array, 0)
    sum_array_index_times.append(time.time() - start_time)
    
    
plt.scatter(x=array_sizes, y=sum_array_times, label='sum_array')
plt.scatter(x=array_sizes, y=sum_array_index_times, label='sum_array_index')
plt.ylim(
    top=max(sum_array_times + sum_array_index_times),
    bottom=min(sum_array_times + sum_array_index_times))
plt.legend()
plt.xlabel('Array Size')
plt.ylabel('Time (seconds)')
plt.plot()
```

As you can see, the function `sum_array` is a polynomial and `sum_array_index` is linear as we predicted. 

However, in our pursuit to use recursion we actually made things worse. Let's look at an iterative solution to this problem:

```Python 
def sum_array_iter(array):
	result = 0 

	for x in array:
		result += x

	return result 

arr = [1, 2, 3, 4]
print(sum_array_iter(arr))
```

The `sum_array_iter` function is a lot more straightforward than the two recursive functions, which is importatn. Second, to help ensure an answer that is correct and bug free, you generally want to pick the solution that is more readable. In some cases recursion is more readable and in some cases iteration is more readable. As you gain experience reading other people's code, you get an intuition for code readability. 

___

### Factorial Fuction 

**Factorial using recursion**

The **factorial** function is a matematical function that multiplies a give number, n, and all of the whole numners from n down to 1. 

For example, if  𝑛  is  4  then we will get:

4∗3∗2∗1=24 

This is often notated using an exclamation point, as in  4!  (which would be read as "four factorial").

So  4!=4∗3∗2∗1=24 

More generally, we can say that for any input  𝑛 :

𝑛!=𝑛∗(𝑛−1)∗(𝑛−2)...1 

If you look at this more closely, you will find that the factorial of any number is the product of that number and the factorial of the next smallest number. In other words:

𝑛!=𝑛∗(𝑛−1)! 

Notice that this is recursive, meaning that we can solve for the factorial of any given number by first solving for the factorial of the next smallest number, and the next smallest number, and the next smallest number, and so on, until we reach 1.

If you were to write a Python function called `factorial` to calculate the factorial of a number, then we could restate what we said above as follows:

`factorial(n) = n * factorial(n-1)`

So that is the goal of this exercise: To use recursion to write a function that will take a number and return the factorial of that number.

For example, you should be able to call your function with `factorial(4)` and get back `24`.

**Note:** By definition,  0!=1

```Python 
# Code

def factorial(n):
    """
    Calculate n!
    
    Args:
       n(int): factorial to be computed
    Returns:
       n!
    """
    
    # TODO: Write your recursive factorial function here
    
    pass
```

```Python
# Test Cases

print ("Pass" if (1 == factorial(0)) else "Fail")
print ("Pass" if  (1 == factorial(1)) else "Fail")
print ("Pass" if  (120 == factorial(5)) else "Fail")
```

___

<details><summary><b>Solution</b></summary>
<p>

```Python 
# Solution

def factorial(n):
    """
    Calculate n!

    Args:
       n(int): factorial to be computed
    Returns:
       n!
    """

	if n == 0:
        return 1  # by definition of 0!
    return n * factorial(n-1)

print ("Pass" if (1 == factorial(0)) else "Fail")
print ("Pass" if  (1 == factorial(1)) else "Fail")
print ("Pass" if  (120 == factorial(5)) else "Fail")
```
</p>
</details>

### Reversing a String 

The goal if to get practice with a problem that is frequently solved by recursionL Resering a string.

Note that Python has a built-in function that you could use for this, but the goal here is to avoid that and understand how it can be done using recursion instead. 

```Python
# Code

def reverse_string(input):
    """
    Return reversed input string
    
    Examples:
       reverse_string("abc") returns "cba"
    
    Args:
      input(str): string to be reversed
    
    Returns:
      a string that is the reverse of input
    """
    
    # TODO: Write your recursive string reverser solution here
    
    pass
```
```Python
# Test Cases
    
print ("Pass" if  ("" == reverse_string("")) else "Fail")
print ("Pass" if  ("cba" == reverse_string("abc")) else "Fail")
```

<details><summary><b>Solution</b></summary>
<p>

```Python 
# Solution

def reverse_string(input):
    """
    Return reversed input string
    
    Examples:
       reverse_string("abc") returns "cba"
    
    Args:
      input(str): string to be reversed
    
    Returns:
      a string that us reversed of input
    """
    if len(input) == 0:
        return ""
    else:
        first_char = input[0]
        the_rest = slice(1, None)
        sub_string = input[the_rest]
        reversed_substring = reverse_string(sub_string)
        return reversed_substring + first_char

print ("Pass" if  ("" == reverse_string("")) else "Fail")
print ("Pass" if  ("cba" == reverse_string("abc")) else "Fail")
```
</p>
</details>

___


### 5. Palindrome 

A **palindrome** is a word that is the reverse of itself --that is, it is the same word when read forwards and backwards.

For example:

* "madam" is a palindrome
* "abba" is a palindrome 
* "cat" is not 
* "a" is a trivial case of a palindrome 

The goal of this exercise is to use recursion to write a function `is_palindrome` that take a string as input and checks whether that string is a palindrome. (Note that this problem can also be solved with a non-recursive solution, but that's not the point of this exercise.)

```Python
def is_palindrome(input):
    """
    Return True if input is palindrome, False otherwise.
    
    Args:
       input(str): input to be checked if it is palindrome
    """
    
    # TODO: Write your recursive palindrome checker here
    
    pass
```

```Python
# Test Cases

print ("Pass" if  (is_palindrome("")) else "Fail")
print ("Pass" if  (is_palindrome("a")) else "Fail")
print ("Pass" if  (is_palindrome("madam")) else "Fail")
print ("Pass" if  (is_palindrome("abba")) else "Fail")
print ("Pass" if not (is_palindrome("Udacity")) else "Fail")
```

<details><summary><b>Solution</b></summary>
<p>

```Python 
# Solution

def is_palindrome(input):
    """
    Return True if input is palindrome, False otherwise.

    Args:
       input(str): input to be checked if it is palindrome
    """
    if len(input) <= 1:
        return True
    else:
        first_char = input[0]
        last_char = input[-1]

        # sub_input is input with first and last char removed
        sub_input = input[1:-1]

        return (first_char == last_char) and is_palindrome(sub_input)

print ("Pass" if  (is_palindrome("")) else "Fail")
print ("Pass" if  (is_palindrome("a")) else "Fail")
print ("Pass" if  (is_palindrome("madam")) else "Fail")
print ("Pass" if  (is_palindrome("abba")) else "Fail")
print ("Pass" if not (is_palindrome("Udacity")) else "Fail")
```
</p>
</details>

___

### 6. Permutation

Let's use recursion to help use solve this permutation problem: 

Given a list of items, the goal is to find all of the permutations of that list. For example, if given a list like: `["apple", "water"]`, you could create two permuations from it. One in the form of the original input and one in the reversed order like so: `["water", "apple"]`

```Python 
# Code

import copy

def permute(l):
    """
    Return a list of permutations
    
    Examples:
       permute([0, 1]) returns [ [0, 1], [1, 0] ]
    
    Args:
      l(list): list of items to be permuted
    
    Returns:
      list of permutation with each permuted item being represented by a list
    """
    pass
```
```Python 
# Test Cases 

# Helper Function
def check_output(output, expected_output):
    """
    Return True if output and expected_output
    contains the same lists, False otherwise.
    
    Note that the ordering of the list is not important.
    
    Examples:
        check_output([ [0, 1], [1, 0] ] ], [ [1, 0], [0, 1] ]) returns True

    Args:
        output(list): list of list
        expected_output(list): list of list
    
    Returns:
        bool
    """
    o = copy.deepcopy(output)  # so that we don't mutate input
    e = copy.deepcopy(expected_output)  # so that we don't mutate input
    
    o.sort()
    e.sort()
    return o == e

print ("Pass" if  (check_output(permute([]), [[]])) else "Fail")
print ("Pass" if  (check_output(permute([0]), [[0]])) else "Fail")
print ("Pass" if  (check_output(permute([0, 1]), [[0, 1], [1, 0]])) else "Fail")
print ("Pass" if  (check_output(permute([0, 1, 2]), [[0, 1, 2], [0, 2, 1], [1, 0, 2], [1, 2, 0], [2, 0, 1], [2, 1, 0]])) else "Fail")
```

<details><summary><b>Solution</b></summary>
<p>

```Python 
# Solution 


import copy

def permute(l):
    """
    Return a list of permutations

    Examples:
       permute([0, 1]) returns [ [0, 1], [1, 0] ]

    Args:
      l(list): list of items to be permuted

    Returns:
      list of permutation with each permuted item be represented by a list
    """
    perm = []
    if len(l) == 0:
        perm.append([])
    else:
        first_element = l[0]
        after_first = slice(1, None)
        sub_permutes = permute(l[after_first])
        for p in sub_permutes:
            for j in range(0, len(p) + 1):
                r = copy.deepcopy(p)
                r.insert(j, first_element)
                perm.append(r)
    return perm

def check_output(output, expected_output):
    """
    Return True if output and expected_output
    contains the same lists, False otherwise.
    
    Note that the ordering of the list is not important.
    
    Examples:
        check_output([ [0, 1], [1, 0] ] ], [ [1, 0], [0, 1] ]) returns True

    Args:
        output(list): list of list
        expected_output(list): list of list
    
    Returns:
        bool
    """
    o = copy.deepcopy(output)  # so that we don't mutate input
    e = copy.deepcopy(expected_output)  # so that we don't mutate input
    
    o.sort()
    e.sort()
    return o == e

print ("Pass" if  (check_output(permute([]), [[]])) else "Fail")
print ("Pass" if  (check_output(permute([0]), [[0]])) else "Fail")
print ("Pass" if  (check_output(permute([0, 1]), [[0, 1], [1, 0]])) else "Fail")
print ("Pass" if  (check_output(permute([0, 1, 2]), [[0, 1, 2], [0, 2, 1], [1, 0, 2], [1, 2, 0], [2, 0, 1], [2, 1, 0]])) else "Fail")

```
</p>
</details>

___

### 7. String Permutations

**Problem Statement**

Given an input string, return all permutations of the string in an array. 

**Example 1:**

* `string = 'ab'`
* `output = ['ab', 'ba']`

**Example 2:**

* `string = 'abc'`
* `output = ['abc', 'bac', 'bca', 'acb', 'cab' 'cba']`

```Python 
def permutations(string):
    """
    :param: input string
    Return - list of all permutations of the input string
    TODO: complete this function to return a list of all permutations of the string
    """
    pass
```
<details><summary><b>Solution</b></summary>
<p>

```Python 
# Solution
def permutations(string):
    return return_permutations(string, 0)
    
def return_permutations(string, index):
    # Base Case
    if index >= len(string):
        return [""]
    
    small_output = return_permutations(string, index + 1)
    
    output = list()
    current_char = string[index]
    
    # iterate over each permutation string received thus far
    # and place the current character at between different indices of the string
    for permutation in small_output:
        for index in range(len(small_output[0]) + 1):
            new_permutation = permutation[0: index] + current_char + permutation[index:]
            output.append(new_permutation)
    return output
```
</p>
</details>


```Python
def test_function(test_case):
    string = test_case[0]
    solution = test_case[1]
    output = permutations(string)
    
    output.sort()
    solution.sort()
    
    if output == solution:
        print("Pass")
    else:
        print("Fail")
```
```Python
string = 'ab'
solution = ['ab', 'ba']
test_case = [string, solution]
test_function(test_case)
```
Pass

```Python
string = 'abc'
output = ['abc', 'bac', 'bca', 'acb', 'cab', 'cba']
test_case = [string, output]
test_function(test_case)
```
Pass

```Python
string = 'abcd'
output = ['abcd', 'bacd', 'bcad', 'bcda', 'acbd', 'cabd', 'cbad', 'cbda', 'acdb', 'cadb', 'cdab', 'cdba', 'abdc', 'badc', 'bdac', 'bdca', 'adbc', 'dabc', 'dbac', 'dbca', 'adcb', 'dacb', 'dcab', 'dcba']
test_case = [string, output]
test_function(test_case)
```
Pass

___

### 8. Keypad Combintations

**Keypad Combinations**

A keypad on a cellphone has alphabets for all numbers between 2 and 9.

You can make different combinations of alphabets by pressing the numbers.

For example, if you press 23, the following combinations are possible:

`ad, ae, af, bd, be, bf, cd, ce, cf`

Note that because 2 is pressed before 3, the first letter is always an alphabet on the number 2. Likewise, if the user types 32, the order would be

`da, db, dc, ea, eb, ec, fa, fb, fc`

Given an integer `num`, find out all the possible strings that can be made using digits of input `num`. Return these strings in a list. The order of strings in the list does not matter. However, as stated earlier, the order of letters in a particular string matters.


```Python
def get_characters(num):
    if num == 2:
        return "abc"
    elif num == 3:
        return "def"
    elif num == 4:
        return "ghi"
    elif num == 5:
        return "jkl"
    elif num == 6:
        return "mno"
    elif num == 7:
        return "pqrs"
    elif num == 8:
        return "tuv"
    elif num == 9:
        return "wxyz"
    else:
        return ""


def keypad(num):
    
    # TODO: Write your keypad solution here!
    
    pass
```

```Python
def test_keypad(input, expected_output):
    if sorted(keypad(input)) == expected_output:
        print("Yay. We got it right.")
    else:
        print("Oops! That was incorrect.")
```

```Python
# Base case: list with empty string
input = 0
expected_output = [""]
test_keypad(input, expected_output)
```

```Python
# Example case
input = 23
expected_output = sorted(["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"])
test_keypad(input, expected_output)
```

```Python
# Example case
input = 32
expected_output = sorted(["da", "db", "dc", "ea", "eb", "ec", "fa", "fb", "fc"])
test_keypad(input, expected_output)
```

```Python
# Example case
input = 8
expected_output = sorted(["t", "u", "v"])
test_keypad(input, expected_output)
```
```Python
input = 354
expected_output = sorted(["djg", "ejg", "fjg", "dkg", "ekg", "fkg", "dlg", "elg", "flg", "djh", "ejh", "fjh", "dkh", "ekh", "fkh", "dlh", "elh", "flh", "dji", "eji", "fji", "dki", "eki", "fki", "dli", "eli", "fli"])
test_keypad(input, expected_output)
```
<details><summary><b>Solution</b></summary>
<p>

```Python 
def keypad(num):
    if num <= 1:
        return [""]
    elif 1 < num <= 9:
        return list(get_characters(num))

    last_digit = num % 10
    small_output = keypad(num//10)
    keypad_string = get_characters(last_digit)
    output = list()
    for character in keypad_string:
        for item in small_output:
            new_item = item + character
            output.append(new_item)
    return output
```
</p>
</details>

___

### 9. Deep Reverse

**Problem Statement**

Define a procedure, `deep_reverse`, that takes as input a list, and returns a new list that is the deep reverse of the input list.
This means it reverses all the elements in the list, and if any of those elements are lists themselves, reverses all the elements in the inner list, all the way down.

>Note: The procedure must not change the input list itself.

```Python 
def deep_reverse(arr):
    pass
```

