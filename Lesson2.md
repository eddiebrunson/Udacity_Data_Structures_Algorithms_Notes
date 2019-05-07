# Lesson 2: Python Refresher

___

* Examples are presented in psuedocode, but mainly will be using [Python 3](https://www.python.org/download/releases/3.0/). 

## 2. Control Stuctures 

Iteration with Loops

To iterate in Python, there are several options. A 'for' loop can be used to iterate through a list or dictionary. Instead of the traditional 'for' loop where we intialize a value 'i' and increase / decrease it till it reaches an end value, Python's 'for' loops are 'for-each' in nature. This means that when you are iterating using a 'for loop' over a list, you actually iterate over the items of that list. 

If you also need the index values from the list while iteratingm another possibility is to use 'enumerate', which is shown in an example below. 

An additional way to iterate in Python is with a 'while' loop. Just as in other programming languages, the 'while' loop will repeat while some conditinal statement is true. You will see more on conditional statements shortly, but first, here are examples of iteration with 'for' and 'while' loops. 

```Python
# Examples of iteration with for loops.

my_list = [0, 1, 2, 3, 4, 5]

# Print each value in my_list. Note you can use the "in" keyword to iterate over a list.
for item in my_list:
    print('The value of item is: ' + str(item))

# Print each index and value pair.
for i, value in enumerate(my_list):
    print('The index value is: ' + str(i) + '. The value at i is: ' + str(value))

# Print each number from 0 to 9 using a while loop.
i = 0
while(i < 10):
    print(i)
    i += 1

# Print each key and dictionary value. Note that you can use the "in" keyword 
# to iterate over dictionary keys.
my_dict = {'a': 'jill', 'b': 'tom', 'c': 'tim'}
for key in my_dict:
    print(key + ', ' + my_dict[key])
```

Remember that Python requires correct indentation for code blocks to be interpreted correctly. Indentation for a block is usually four spaces, or one tab length. 

## Quiz 1 question:

What would be the output of the following code?

```Python 
my_dict = {'a':[0, 1, 2, 3], 'b':[0, 1, 2, 3], 'c':[0, 1, 2, 3], 'd':[0, 1, 2, 3]}
i = 0
output = []
for key in my_dict:
    output.append(my_dict[key][i])
    i += 1
print(output)
```

:black_small_square: [0, 1, 2, 3, 0, 1, 2, 3, 0, 1, 2, 3, 0, 1, 2, 3]


:black_small_square: ['a', 'b', 'c', 'd']


:white_check_mark:  [0, 1, 2, 3]

___

### Conditional Statements

Conditional statements use bookean logic to help guide our decision process: the statement is true or false. These statements are structured using comparison operators: greater than ('>'), less than ('<'), and equal to ('==').

Using conditional statements for control flow is commplished in Python with the keywords:'if', 'else', and 'elif'. When doing multiple comparisons in Pyton, one after the other, the first comparison always uses 'if' and the last comparison generally uses 'else'. If additional control flow is needed, 'elif' statements can be used; 'elif' stands for "else if". 

```Pthon 
num = 5
if num < 5:
    print('The number is smaller than 5.')
elif num == 5:
    print('The number equals 5.')
else:
    print('The number is greater than 5.')
```
The code above would print: 'The number equals 5.'

___

### Control Stucture Practice 


