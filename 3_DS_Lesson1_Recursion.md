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

<details><summary><b>Solution</b></summary>
<p>

```Python 
def is_list(element):
    """
    Check if element is a Python list
    """
    return isinstance(element, list)

def deep_reverse(arr):
    """
    Function to deep_reverse an input list
    """
    return deep_reverse_func(arr, 0)

def deep_reverse_func(arr, index):
    """
    Recursive function to deep_reverse the input list
    """
    # Base Case
    if index == len(arr):
        return list()
    
    output = deep_reverse_func(arr, index + 1)
    
    # if element is a list --> deep_reverse the list
    if is_list(arr[index]):
        to_append = deep_reverse(arr[index])
    else:
        to_append = arr[index]
        
    output.append(to_append)
    return output
```
</p>
</details>

___

```Python 
def test_function(test_case):
    arr = test_case[0]
    solution = test_case[1]
    
    output = deep_reverse(arr)
    if output == solution:
        print("Pass")
    else:
        print("False")
```

```Python
arr = [1, 2, 3, 4, 5]
solution = [5, 4, 3, 2, 1]
test_case = [arr, solution]
test_function(test_case)
```
```Python
arr = [1, 2, [3, 4, 5], 4, 5]
solution = [5, 4, [5, 4, 3], 2, 1]
test_case = [arr, solution]
test_function(test_case)
```
```Python
arr = [1, [2, 3, [4, [5, 6]]]]
solution = [[[[6, 5], 4], 3, 2], 1]
test_case = [arr, solution]
test_function(test_case)
```
```Python
arr =  [1, [2,3], 4, [5,6]]
solution = [ [6,5], 4, [3, 2], 1]
test_case = [arr, solution]
test_function(test_case)
```

___

### The Call Stack and Recursion

**What is a call stack?**

When we use functions in our code, the computer makes use of a data structure called a **call stack**. As the name suggests, a call stack is a type of stack—meaning that it is a Last-In, First-Out (LIFO) data structure.

So it's a type of stack—but a stack of what, exactly?

Essentially, a call stack is a stack of frames that are used for the functions that we are calling. When we call a function, say `print_integers(5)`, a frame is created in memory. All the variables local to the function are created in this memory frame. And as soon as this frame is created, it's pushed onto the call stack.

The frame that lies at the top of the call stack is executed first. And as soon as the function finishes executing, this frame is discarded from the call stack.

**An example**

Let's consider the following function, which simply takes two integers and returns their sum

```Python
def add(num_one, num_two):
    output = num_one + num_two
    return output
```

```Python
result = add(5, 7)
print(result)
```
Before understanding what happens when a function is executed, it is important to remind ourselves that whenever an expression such as `product = 5 * 7` is evaluated, the right hand side of the `=` sign is evaluted first. When the right-hand side is completely evaluated, the result is stored in the variable name mentioned in the left-hand side.

When Python executes line 1 in the previous cell (`result = add(5, 7)`), the following things happen in memory:

* A frame is created for the `add` function. This frame is then pushed onto the *call stack*. We do not have to worry about this because Python takes care of this for us.

* Next, the parameters `num_one` and `num_two` get the values `5` and `7`, respectively

If we run this code in [Python tutor website](http://pythontutor.com/), we can get a nice visualization of what's happening "behind the scenes" in memory:

* Python then moves on to the first line of the function. The first line of the function is
    
        output = num_one + num_two
      
    Here an expression is being evaluated and the result is stored in a new variable. The expression here is sum of two numbers the result of which is stored in the variable `output`. We know that whenever an expression is evaluated, the right-hand side of the `= sign` is evaluated first. So, the numbers `5 and 7` will be added first.
     
     
* Once the right-hand side is completely evaluated, then the assignment operation happens i.e. now the result of `5 + 7` will be stored in the variable `output`.

* In the next line, we are returning this value. 

        return output
        
   Python acknowledged this return statement. 
   <img src='./stack-frame-resources/03.png'>
   
   
* Now the last line of the function has been executed. Therefore, this function can now be discarded from the stack frame. Also, the right-hand side of the expression `result = add(5, 7)` has finished evaluation. Now, the result of this evaluation will be stored in the variable `result`.

   <img src='./stack-frame-resources/04.png'>

___

Now the next question is how does this behave like a stack? The answer is pretty simple. We know that a stack is a Last-In First-Out (LIFO) structure, meaning the latest element inserted in the stack is the first to be removed.

**Another example**

Here's another example. Let's say we have a function add() which adds two integers and then prints a custom message for us using the custom_print() function.

```Python
def add(num_one, num_two):
    output = num_one + num_two
    custom_print(output, num_one, num_two)
    return output

def custom_print(output, num_one, num_two):
    print("The sum of {} and {} is: {}".format(num_one, num_two, output))
    
result = add(5, 7)    
```

What happens "behind-the-scenes" when `add()` is called, as in `result = add(5, 7)`?

Feel free to play with this on the Python tutor website. Here are a few points which might help aid the understanding.

* We know that when add function is called using `result = add(5, 7)`, a frame is created in the memory for the add() function. This frame is then pushed onto the call stack.

* Next, the two numbers are added and their result is stored in the variable `output`.

* On the next line we have a new function call - `custom_print(output, num_one, num_two)`. It's obvious that a new frame should be created for this function call as well. You must have realized that this new frame is now pushed into the call stack.

* We also know that the function which is at the top of the call stack is the one which Python executes. So, our `custom_print(output, num_one, num_two)`will now be executed.

* Python executes this function and as soon as it is finished with execution, the frame for `custom_print(output, num_one, num_two)` is discarded. If you recall, this is the LIFO behavior that we have discussed while studying stacks.

* Now, again the frame for `add()` function is at the top. Python resumes operation just after the line where it had left and returns the `output`.
___

**Call Stack and Recursion**

Problem Statement
Consider the following problem:

Given a positive integer n, write a function, `print_integers`, that uses recursion to print all numbers from `n` to `1`.

For example, if `n` is `4`, the function should print `4 3 2 1`.

If we use iteration, the solution to the problem is simple. We can simply start at `4` and use a loop to print all numbers till `1`. However, instead of using an interative approach, our goal is to solve this problem using recursion.

```Python
def print_integers(n):
    # TODO: Complete the function so that it uses recursion to print all integers from n to 1
    pass
```
<details><summary><b>Solution</b></summary>
<p>

```Python 
#TODO

```
</p>
</details>

___

```Python
print_integers(5)
``` 

Now let's consider what happens in the call stack when `print_integers(5)` is called. 

* As expected, a frame will be created for the `print_integers()` function and pushed onto the call stack. 


* Next, the parameter `n` gets the value `5`. 


* Following this, the function starts executing. The base condition is checked. For `n = 5`, the base case is `False`, so we move forward and print the value of `n`.


* In the next line, `print_integers()` is called again. This time it is called with the argument `n - 1`. The value of `n` in the current frame is `5`. So this new function call takes place with value `4`. Again, a new frame is created. **Note that for every new call a new frame will be created.** This frame is pushed onto the top of the stack. 


* Python now starts executing this frame. Again the base case is checked. It's `False` for `n = 4`. Following this, the `n` is printed and then `print_integers()` is called with argument `n - 1 = 3`. 


* The process keep on like this until we hit the base case. When `n <= 0`, we return from the frame without calling the function `print_integers()` again. Because we have returned from the function call, the frame is discarded from the call stack and the next frame resumes execution right after the line where we left off. 

___

### 11. Recurrence Relations 

**Problem Statement**

Previously, we considered the following problem:

>Given a positive integer `n`, write a function, `print_integers`, that uses recursion to print all numbers from `n` to `1`. 
>
>For example, if `n` is `4`, the function shuld print `4 3 2 1`. 

Our solution was:

```Python
def print_integers(n):
    if n <= 0:
        return
    print(n)
    print_integers(n - 1)
```

```Python
print_integers(5)
```
5
4
3
2
1

We have already discussed that every time a function is called, a new frame is created in memory, which is then pushed onto the *call stack*. For the current function, `print_integers`, the call stack with all the frames would look like this:

<img src='./recurrence-relation-resources/01.png'>

___

Note that in Python, the stack is displayed in an "upside down" manner. This can be seen in the illustration above—the last frame (i.e. the frame with `n = 0)` lies at the top of the stack (but is displayed last here) and the first frame (i.e., the frame with n = 5) lies at the bottom of the stack (but is displayed first).

But don't let this confuse you. The frame with `n = 0`is indeed the top of the stack, so it will be discarded first. And the frame with n = 5 is indeed at the bottom of the stack, so it will be discarded last.

We define time complexity as a measure of amount of time it takes to run an algorithm. Similarly, the time complexity of our function `print_integers(5)`, would indicate the amount of time taken to exceute our function print_integers. But notice how when we call `print_integers()` with a particular value of `n`, it recursively calls itself multiple times.

In other words, when we call `print_integers(n)`, it does operations (like checking for base case, printing number) and then calls `print_integers(n - 1)`.

Therefore, the overall time taken by print_integers(n) to execute would be equal to the time taken to execute its own simple operations and the time taken to execute `print_integers(n - 1)`.

Let the time taken to execute the function `print_integers(n)` be 𝑇(𝑛). And let the time taken to exceute the function's own simple operations be represented by some constant, 𝑘.

In that case, we can say that

𝑇(𝑛)=𝑇(𝑛−1)+𝑘

where 𝑇(𝑛−1) represents the time taken to execute the function `print_integers(n - 1)`.

Similarly, we can represent 𝑇(𝑛−1) as

𝑇(𝑛−1)=𝑇(𝑛−2)+𝑘

We can see that a pattern is being formed here:

𝑇(𝑛)       =𝑇(𝑛−1)+𝑘
𝑇(𝑛−1)=𝑇(𝑛−2)+𝑘
𝑇(𝑛−2)=𝑇(𝑛−3)+𝑘
𝑇(𝑛−3)=𝑇(𝑛−4)+𝑘 .
.
.
.
.
.
𝑇(2)=𝑇(1)+𝑘
𝑇(1)=𝑇(0)+𝑘
𝑇(0)=𝑘1
Notice that when n = 0 we are only checking the base case and then returning. This time can be represented by some other constant, 𝑘1.

If we add the respective left-hand sides and right-hand sides of all these equations, we get:

𝑇(𝑛)=𝑛𝑘+𝑘1

We know that while calculating time complexity, we tend to ignore these added constants because for large input sizes on the order of 105, these constants become irrelevant.

Thus, we can simplify the above to:

𝑇(𝑛)=𝑛𝑘

We can see that the time complexity of our function `print_integers(n)` is a linear function of 𝑛. Hence, we can say that the time complexity of the function is 𝑂(𝑛).

___


**Binary Search**
Let's look at the time complexity of one more recursive algorithm.

Note: The binary search function can also be written iteratively. But for the sake of understanding recurrence relations, we will have a look at the recursive algorithm.

Here's the binary search algorithm, coded using recursion:

```Python
def binary_search(arr, target):
    return binary_search_func(arr, 0, len(arr) - 1, target)

def binary_search_func(arr, start_index, end_index, target):
    if start_index > end_index:
        return -1
    
    mid_index = (start_index + end_index)//2
    
    if arr[mid_index] == target:
        return mid_index
    elif arr[mid_index] > target:
        return binary_search_func(arr, start_index, mid_index - 1, target)
    else:
        return binary_search_func(arr, mid_index + 1, end_index, target)
```

```Python
arr = [0, 1, 2, 3, 4, 5, 6, 7, 8]
print(binary_search(arr, 5))
```
Let's try to analyze the time complexity of the recursive algorithm for binary search by finding out the recurrence relation.

Our `binary_search()` function calls the `binary_search_func()` function. So the time complexity of the function is entirely dependent on the time complexity of the `binary_search_func()`.

The input here is an array, so our time complexity will be determined in terms of the size of the array.

Like we did earlier, let's say the time complexity of `binary_search_func()` is a function of the input size, n. In other words, the time complexity is  𝑇(𝑛) .

Also keep in mind that we are usually concerned with the worst-case time complexity, and that is what we will calculate here. In the worst case, the `target` value will not be present in the array.

In the `binary_search_func()` function, we first check for the base case. If the base case does not return `True`, we calculate the `mid_index` and then compare the element at this `mid_index` with the `target` values. All the operations are independent of the size of the array. Therefore, we can consider all these independent operations as taking a combined time,  𝑘 .

Apart from these constant time operations, we do just one other task. We either make a call on the left-half of the array, or on the right half of the array. By doing so, we are reducing the input size by  𝑛/2 .

Note: Remember that we usually consider large input sizes while calculating time complexity; there is no significant difference between  105 and ( 105+1 ).

Thus, our new function call is only called with half the input size. We said that  𝑇(𝑛)  was the time complexity of our original function. The time complexity of the function when called with half the input size will be  𝑇(𝑛/2) .

Therefore:

𝑇(𝑛)=𝑇(𝑛/2)+𝑘
 
Similarly, in the next step, the time complexity of the function called with half the input size would be:

𝑇(𝑛/2)=𝑇(𝑛/4)+𝑘
 
We can now form similar equations as we did for the last problem:

𝑇(𝑛)   =𝑇(𝑛/2)+𝑘 
𝑇(𝑛/2)=𝑇(𝑛/4)+𝑘 
𝑇(𝑛/4)=𝑇(𝑛/8)+𝑘 
𝑇(𝑛/8)=𝑇(𝑛/16)+𝑘  .
.
.
.
.
.
𝑇(4)=𝑇(2)+𝑘 
𝑇(2)=𝑇(1)+𝑘 
𝑇(1)=𝑇(0)+𝑘1   (1) 
𝑇(0)=𝑘1 
(1)  If we have only one element, we go to 0 elements next

From our binary search section, we know that it takes  𝑙𝑜𝑔(𝑛)  steps to go from  𝑇(𝑛)  to  1 . Therefore, when we add the corresponding left-hand sides and right-hand sides, we can safely say that:

𝑇(𝑛)=𝑙𝑜𝑔(𝑛)∗𝑘+𝑘1
 
As always, we can ignore the constant. Therefore:

𝑇(𝑛)=𝑙𝑜𝑔(𝑛)∗𝑘
 
Thus we see that the time complexity of the function is a logarithmic function of the input,  𝑛 . Hence, the time complexity of the recursive algorithm for binary search is  𝑙𝑜𝑔(𝑛) .

___

### 12. Tower of Hanoi

**Problem Statement**

The Tower of Hanoi is a puzzle where we have three rods and n disks. The three rods are:

1. source
2. destination
3. auxiliary

Initally, all the n disks are present on the source rod. The final objective of the puzzle is to move all disks from the source rod to the destination rod using the auxiliary rod. However, there are some rules according to which this has to be done:

1. Only one disk can be moved at a time.
2. A disk can be moved only if it is on the top of a rod.
3. No disk can be placed on the top of a smaller disk.

You will be given the number of disks num_disks as the input parameter.

For example, if you have num_disks = 3, then the disks should be moved as follows:

    1. move disk from source to auxiliary
    2. move disk from source to destination
    3. move disk from auxiliary to destination
You must print these steps as follows:

    S A
    S D
    A D
Where S = source, D = destination, A = auxiliary

```Python 
def tower_of_Hanoi(num_disks):
    """
    :param: num_disks - number of disks
    TODO: print the steps required to move all disks from source to destination
    """
    pass
```

<details><summary><b>Solution</b></summary>
<p>

```Python 
# Solution
def tower_of_Hanoi_soln(num_disks, source, auxiliary, destination):
    
    if num_disks == 0:
        return
    
    if num_disks == 1:
        print("{} {}".format(source, destination))
        return
    
    tower_of_Hanoi_soln(num_disks - 1, source, destination, auxiliary)
    print("{} {}".format(source, destination))
    tower_of_Hanoi_soln(num_disks - 1, auxiliary, source, destination)
    
def tower_of_Hanoi(num_disks):
    tower_of_Hanoi_soln(num_disks, 'S', 'A', 'D')
```
</p>
</details>

___

```Python
Compare your results with the following test cases
num_disks = 2

  solution 
          S A
          S D
          A D
num_disks = 3

  solution 
          S D
          S A
          D A
          S D
          A S
          A D
          S D
num_disks = 4

  solution
          S A
          S D
          A D
          S A
          D S
          D A
          S A
          S D
          A D
          A S
          D S
          A D
          S A
          S D
          A D
```

___

### 13. Return Codes

**Problem statement**

In an encryption system where ASCII lower case letters represent numbers in the pattern `a=1, b=2, c=3...` and so on, find out all the codes that are possible for a given input number. 

**Example 1**

* `number = 123`
* `codes_possible = ["aw", "abc", "lc"]`

Explanation: The codes are for the following number:
         
* 1 . 23     = "aw"
* 1 . 2 . 3  = "abc"
* 12 . 3     = "lc"
    

**Example 2**  

* `number = 145`
* `codes_possible = ["ade", "ne"]`

Return the codes in a list. The order of codes in the list is not important.

*Note: you can assume that the input number will not contain any 0s*

```Python 
def all_codes(number):
    """
    :param: number - input integer
    Return - list() of all codes possible for this number
    TODO: complete this method and return a list with all possible codes for the input number
    """
    pass
```
<details><summary><b>Solution</b></summary>
<p>

```Python 
# Solution

def get_alphabet(number):
    """
    Helper function to figure out alphabet of a particular number
    Remember: 
        * ASCII for lower case 'a' = 97
        * chr(num) returns ASCII character for a number e.g. chr(65) ==> 'A'
    """
    return chr(number + 96)

def all_codes(number):
    if number == 0:
        return [""]
    
    # calculation for two right-most digits e.g. if number = 1123, this calculation is meant for 23
    remainder = number % 100
    output_100 = list()
    if remainder <= 26 and number > 9 :
        
        # get all codes for the remaining number
        output_100 = all_codes(number // 100)
        alphabet = get_alphabet(remainder)
        
        for index, element in enumerate(output_100):
            output_100[index] = element + alphabet
    
    # calculation for right-most digit e.g. if number = 1123, this calculation is meant for 3
    remainder = number % 10
    
    # get all codes for the remaining number
    output_10 = all_codes(number // 10)
    alphabet = get_alphabet(remainder)
    
    for index, element in enumerate(output_10):
        output_10[index] = element + alphabet
        
    output = list()
    output.extend(output_100)
    output.extend(output_10)
    
    return output
```
</p>
</details>

___

```Python
number = 123
solution = ['abc', 'aw', 'lc']
test_case = [number, solution]
test_function(test_case)
```
Pass

```Python 
number = 145
solution =  ['ade', 'ne']
test_case = [number, solution]
test_function(test_case)
```
Pass

```Python 
number = 1145
solution =  ['aade', 'ane', 'kde']
test_case = [number, solution]
test_function(test_case)
```
Pass

```Python
number = 4545
solution = ['dede']
test_case = [number, solution]
test_function(test_case)
```

___


### 14. Return Subsets

**Problem Statement**

Given an integer array, find and return all the subsets of the array. The order of subsets in the output array is not important. However the order of elements in a particular subset should remain the same as in the input array.

Note: An empty set will be represented by an empty list

```Python
Example 1

arr = [9]

output = [[]
          [9]]
Example 2

arr = [9, 12, 15]

output =  [[],
           [15],
           [12],
           [12, 15],
           [9],
           [9, 15],
           [9, 12],
           [9, 12, 15]]
```

```Python
def subsets(arr):
    """
    :param: arr - input integer array
    Return - list of lists (two dimensional array) where each list represents a subset
    TODO: complete this method to return subsets of an array
    """
    pass
```

<details><summary><b>Solution</b></summary>
<p>

```Python 
# Solution
def subsets(arr):
    return return_subsets(arr, 0)

def return_subsets(arr, index):
    if index >= len(arr):
        return [[]]

    small_output = return_subsets(arr, index + 1)

    output = list()
    # append existing subsets
    for element in small_output:
        output.append(element)

    # add current elements to existing subsets and add them to the output
    for element in small_output:
        current = list()
        current.append(arr[index])
        current.extend(element)
        output.append(current)
    return output
```
</p>
</details>

___

```Python
def test_function(test_case):
    arr = test_case[0]
    solution = test_case[1]
    
    output = subsets(arr)
        
    output.sort()
    solution.sort()
    
    if output == solution:
        print("Pass")
    else:
        print("Fail")    
```

```Python
arr = [9]
solution = [[], [9]]

test_case = [arr, solution]
test_function(test_case)
```
Pass

```Python
arr = [5, 7]
solution = [[], [7], [5], [5, 7]]
test_case = [arr, solution]
test_function(test_case)
```
Pass

```Python
arr = [9, 12, 15]
solution = [[], [15], [12], [12, 15], [9], [9, 15], [9, 12], [9, 12, 15]]

test_case = [arr, solution]
test_function(test_case)
```
Pass

```Python
arr = [9, 8, 9, 8]
solution = [[],
[8],
[9],
[9, 8],
[8],
[8, 8],
[8, 9],
[8, 9, 8],
[9],
[9, 8],
[9, 9],
[9, 9, 8],
[9, 8],
[9, 8, 8],
[9, 8, 9],
[9, 8, 9, 8]]

test_case = [arr, solution]
test_function(test_case)
```
Pass

___

### 15. Staircase

### Problem Statement

Suppose there is a staircase that you can climb in either 1 step, 2 steps, or 3 steps. In how many possible ways can you climb the staircase if the staircase has `n` steps? Write a recursive function to solve the problem.

**Example:**

* `n = 3`
* `output = 4`
    
The output is `4` because there are four ways we can climb the staircase:
    
    1. 1 step +  1 step + 1 step
    2. 1 step + 2 steps 
    3. 2 steps + 1 step
    4. 3 steps

    
