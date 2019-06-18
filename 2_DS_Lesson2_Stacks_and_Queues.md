# 2. Data Structures

## Lesson 2: Stacks and Queues

___

### 1. Stacks Introduction 

Stacks are also a list-based data structure, so they are slightly different than arrays and linked lists. 

The main idea is a stack is like a stack of objects in real life. 

You keep putting elements on top and you have easy access to remove or look at the top element. 

___

### 2. Stacks Details

Stacks can be really useful when you only care about the most recent elements or the order in which you see and save elements actually matters. 

There are specific terminology associated with stacks. 

When you add an element to a stack, the operation is called a **Push** instead of insert.

When you take an element off of the stack, the operation is called a **Pop** instead of remove.

Remember all you need is to look at the top element of the stack. So the operation should be constant time **O(n)** for both Push and Pop operations. 

The notation L.I.F.O. associated with stakcs, which means **Last In, First Out**.

Which means that the last element you put on the stack when you use push, is always the first one you get out when you use pop. 

___

### 3. Implement a Stack Using an Array

One way to implement an stack.


**Walkthrough**

With stacks you can only access the last element added to the stack. 

Whereas, with an **array** you can access elements at the beginning, middle, or end of the array. 

For example, imagine *stacks* as a Prinkles can, where you can only remove or add from the top. Therefore, a stack is a **last in, first out** data structure. 

So if you want to remove elements under the element on top, you will first have to remove the elements on top to reach the selected element below. 

To implement a stack using an array, you would define `stack` class and give it the necessary behaviors to determine what objects in that class can do. 


___


**Functionality**

The goal is to implement a `Stack` class that has the following behaviors:

1. `push` - adds an item to the top of the stack
2. `pop` - removes an item from the top of the stack (and returns the value of that item)
3. `size` - returns the size of the stack
4. `top` - returns the value of the item at the top of the stack (without removing that item)
5. `is_empty` - returns `True` if the stack is empty and `False` otherwise

##### 1. Create and initialize the `Stack` class

```Python
class Stack:
    
    def __init__(self, initial_size = 10):
        self.arr = [0 for _ in range(initial_size)]
        self.next_index = 0
        self.num_elements = 0
```
Next:

* Define a class named `Stack` and add the `__init__` method
* Initialize the `arr` attribute with an array containing 10 elements, like this: `[0, 0, 0, 0, 0, 0, 0, 0, 0, 0]`
* Initialize the `next_index` attribute
* Initialize the `num_elements` attribute

To check if the array is being initalized correctly. You can create a `Stack` object and access the `arr` attribute, and we should see the ten-element array:

```Python
foo = Stack()
print(foo.arr)
print("Pass" if foo.arr == [0, 0, 0, 0, 0, 0, 0, 0, 0, 0] else "Fail")
```

<details><summary><b>Solution</b></summary>
<p>

```Python 
class Stack:
    
    def __init__(self, initial_size = 10):
        self.arr = [0 for _ in range(initial_size)] 
        self.next_index = 0
        self.num_elements = 0
```
</p>
</details>

___

##### 2. Add the `push` method

Next, we define our `push` method, so that we have a way of adding elements to the top of the stack.

**Walkthrough**


___

The key things to include: 

* The method will need to have a parameter for the value that you want to push 
* Remember that `next_index` will have the index for where the value should be added
* Once you've added the value, you'll want to increament both `next_index` and `num_elements`

```Python
class Stack:
    
    def __init__(self, initial_size = 10):
        self.arr = [0 for _ in range(initial_size)]
        self.next_index = 0
        self.num_elements = 0
        
    # TODO Add the push method
```
Test it by creating a stack oject and pushing an item onto the stack:

```Python 
foo = Stack()
foo.push("Test!")
print(foo.arr)
print("Pass" if foo.arr[0] == "Test!" else "Fail")

>>> ['Test!', 0, 0, 0, 0, 0, 0, 0, 0, 0]
Pass
```

<details><summary><b>Solution</b></summary>
<p>

```Python 
class Stack:
    
    def __init__(self, initial_size = 10):
        self.arr = [0 for _ in range(initial_size)] 
        self.next_index = 0
        self.num_elements = 0
```
</p>
</details>

___


##### 3. Handle full capacity 

If you keep pushing items onto the stack, eventually you will run out of room in the array. Currently, that will cause an `Index out of range` error. In order to avoid a stack overflow, we need to check the capacity of the array before pushing an item to the stack. And if the array is full, we need to increase the array size before pushing the new element. 


**Walktthrough**


___

First, define the `_handle_stack_capacity_full` method:

* Define an `old_arr` variable and assign it the current (full) array
* Create a new  (larger) array and assign it to `arr`
* Iterate over the values in the old array and copy them to the new array

Then, in the `push` method:

* Add a conditional to check if the array is full; if it is , call the `_handle_stack_capacity_full`


```Python 
class Stack:
    
    def __init__(self, initial_size = 10):
        self.arr = [0 for _ in range(initial_size)]
        self.next_index = 0
        self.num_elements = 0
        
    def push(self, data):
        # TODO: Add a conditional to check for full capacity
        
        self.arr[self.next_index] = data
        self.next_index += 1
        self.num_elements += 1
        
    # TODO: Add the _handle_stack_capacity_full method
```
We can test this by pushing items onto the stack until we exceed the original capacity. Let's see if we get an error, or if the array size gets increased like we want it to.

```Python 
foo = Stack()
foo.push(1)
foo.push(2)
foo.push(3)
foo.push(4)
foo.push(5)
foo.push(6)
foo.push(7)
foo.push(8)
foo.push(9)
foo.push(10) # The array is now at capacity!
foo.push(11) # This one should cause the array to increase in size
print(foo.arr) # Let's see what the array looks like now!
print("Pass" if len(foo.arr) == 20 else "Fail") # If we successfully doubled the array size, it should now be 20.

>>> Out of space! Increasing array capacity ...
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 0, 0, 0, 0, 0, 0, 0, 0, 0]
Pass
```
<details><summary><b>Solution</b></summary>
<p>

```Python 
class Stack:
    
    def __init__(self, initial_size = 10):
        self.arr = [0 for _ in range(initial_size)]
        self.next_index = 0
        self.num_elements = 0
        
    def push(self, data):
        if self.next_index == len(self.arr):
            print("Out of space! Increasing array capacity ...")
            self._handle_stack_capacity_full()
        
        self.arr[self.next_index] = data
        self.next_index += 1
        self.num_elements += 1

    def _handle_stack_capacity_full(self):
        old_arr = self.arr

        self.arr = [0 for _ in range( 2* len(old_arr))]
        for index, element in enumerate(old_arr):
            self.arr[index] = element
```
</p>
</details>

___

##### 4. Add the `size` and `is_empty` methods

Next, we need to add a couple of simple methods:

* Add a `size` method that returns the current size of the stack
* Add an `is_empty` method that returns `True` if the stack is empty and `False` otherwise

<details><summary><b>Solution</b></summary>
<p>

```Python
class Stack:
    
    def __init__(self, initial_size = 10):
        self.arr = [0 for _ in range(initial_size)]
        self.next_index = 0
        self.num_elements = 0
        
    def push(self, data):
        if self.next_index == len(self.arr):
            print("Out of space! Increasing array capacity ...")
            self._handle_stack_capacity_full()
        
        self.arr[self.next_index] = data
        self.next_index += 1
        self.num_elements += 1
        
    # TODO: Add the size method
    
    # TODO: Add the is_empty method

    def _handle_stack_capacity_full(self):
        old_arr = self.arr

        self.arr = [0 for _ in range( 2* len(old_arr))]
        for index, value in enumerate(old_arr):
            self.arr[index] = value
```

</p>
</details>


___

Test the new methods:

```Python 
foo = Stack()
print(foo.size()) # Should return 0
print(foo.is_empty()) # Should return True
foo.push("Test") # Let's push an item onto the stack and check again
print(foo.size()) # Should return 1
print(foo.is_empty()) # Should return False
```

<details><summary><b>Solution</b></summary>
<p>

```Python
class Stack:
    
    def __init__(self, initial_size = 10):
        self.arr = [0 for _ in range(initial_size)]
        self.next_index = 0
        self.num_elements = 0
        
    def push(self, data):
        if self.next_index == len(self.arr):
            print("Out of space! Increasing array capacity ...")
            self._handle_stack_capacity_full()
        
        self.arr[self.next_index] = data
        self.next_index += 1
        self.num_elements += 1

    def size(self):
        return self.num_elements

    def is_empty(self):
        return self.num_elements == 0
    
    def _handle_stack_capacity_full(self):
        old_arr = self.arr

        self.arr = [0 for _ in range( 2* len(old_arr))]
        for index, element in enumerate(old_arr):
            self.arr[index] = element
```

</p>
</details>

___

##### 5. Add the `pop` method

The last thing we need to do is add the `pop` method.

The method needs to:

* Check if the stack is empty and, if it is, return `None`
* Decrement `next_index` and num_elements
* Return the item that is being "popped"

```Python 
class Stack:
    
    def __init__(self, initial_size = 10):
        self.arr = [0 for _ in range(initial_size)]
        self.next_index = 0
        self.num_elements = 0
        
    def push(self, data):
        if self.next_index == len(self.arr):
            print("Out of space! Increasing array capacity ...")
            self._handle_stack_capacity_full()
        
        self.arr[self.next_index] = data
        self.next_index += 1
        self.num_elements += 1
        
    # TODO: Add the pop method

    def size(self):
        return self.num_elements

    def is_empty(self):
        return self.num_elements == 0
    
    def _handle_stack_capacity_full(self):
        old_arr = self.arr

        self.arr = [0 for _ in range( 2* len(old_arr))]
        for index, value in enumerate(old_arr):
            self.arr[index] = value
```
Let's rest the `pop` method:

```Python 
foo = Stack()
foo.push("Test") # We first have to push an item so that we'll have something to pop
print(foo.pop()) # Should return the popped item, which is "Test"
print(foo.pop()) # Should return None, since there's nothing left in the stack

>>> Test
None
```

</p>
</details>


___

<details><summary><b>Solution</b></summary>
<p>

```Python
class Stack:
    
    def __init__(self, initial_size = 10):
        self.arr = [0 for _ in range(initial_size)]
        self.next_index = 0
        self.num_elements = 0
        
    def push(self, data):
        if self.next_index == len(self.arr):
            print("Out of space! Increasing array capacity ...")
            self._handle_stack_capacity_full()
        
        self.arr[self.next_index] = data
        self.next_index += 1
        self.num_elements += 1
        
    def pop(self):
        if self.is_empty():
            self.next_index = 0
            return None
        self.next_index -= 1
        self.num_elements -= 1
        return self.arr[self.next_index]

    def size(self):
        return self.num_elements

    def is_empty(self):
        return self.num_elements == 0
    
    def _handle_stack_capacity_full(self):
        old_arr = self.arr

        self.arr = [0 for _ in range( 2* len(old_arr))]
        for index, element in enumerate(old_arr):
            self.arr[index] = element
```

</p>
</details>

___

### 4. Implement a Stack Using a Linked List

Implementing a stack using an array works, but introduces concerns with time complexity. For example, if we exceed the capacity of the array, we have to go through the laborious process of creating a new array and moving over all the elements from the old array. 

What if we instead implement the stack using a linked list? Can this improve our time complexity? Let's give it a try.

##### 1. Define a `Node` class 

Since we'll be implementing a linked list for this, we know that we'll need a `Node` class like we used earlier. 

> Note: Practice implementing this from memory as each concept builds upon one another. So try to remember, then check the solution, then hide the solution and try to remember again! 

```Python 
# Add the Node class here from memory 

```
<details><summary><b>Solution</b></summary>
<p>

```Python
class Node:
    def __init__(self, value):
        self.value = value
        self.next = None
```

</p>
</details>

___

##### 2. Create the `Stack` Class and its `__init__` method

In the below, see if you can write the `__init__` method for our `Stack` class. It will need two attributes:

* A `head` attribute to keep track of the first node in the linked list
* A `num_elements` attribute to keep track of how many items are in the stack

```Python 
class Stack:
    
    # TODO: Add the __init__ method

```
<details><summary><b>Solution</b></summary>
<p>

```Python
class Stack:
    
    def __init__(self):
        self.head = None # No items in the stack, so head should be None
        self.num_elements = 0 # No items in the stack, so num_elements should be 0
```

</p>
</details>

___

##### 3. Add the `push` method 

Next, we need to define our `push` method, so that we have a way of adding elements to the top of the stack. 

**Walkthrough**

First we take a look at the first method, we take the value that we are passing in to create a new node.

```Python 
def push (self, value):
	new_node = Node(value)
```


But, first we need to check if there are any new nodes. 

If the value of the head is None, then we know that we haven't added anything yet and that the stack is empty. 
```Python 
# if stsack is empty

if self. head is None:
	self.head = new_node
``` 
Then the question is where do we attach this node? In a stack we can only add to the top, but which end of the list should be the top, the tail or the head?

First, 

```Python
else: 
	current_node = head 
	while current_node.next:
		current_node = current_node.next
	current_node.next = new_node
```
Start at the head of the list, then we iterate over the of the nodes. We use the while loop to traverse the list until we find the end of the list. Wherever a node points to None, rather than next element. We attach that element to new node. This approach will work but it isn't very efficient! 

Because, everytime we want to pop or push an item we have to traverse the whole linked lists to get to the top of the stack. By defining the tail as the top of the stack, we are using the head as the entry point and we have the issue where we have to traverse the to reach the top of the stack. 

So we flip that around and want to define the head as the top of the stack.

```Python 
else:
	new_node.next = self.head 
	self.head = new_node
self.num_elements += 1
```

So we are attaching the new node in front of the head and making it the new head of list. 

Now we need to keep track of where the top of the stack is, by updating what head refers to. 
___


Now give it a try yourself. Add the `push` method.

* The method will need to have a parameter for the `value` that you want to push 
* You'll then need to create a new `Node` object with this value and link it to the list
* Rememebr that we want to add new items at the head of the stack, not the tail!
* Once the new node is added, you increment `num_elements`


```Python 
class Stack:
    
    def __init__(self):
        self.head = None
        self.num_elements = 0
        
    # TODO: Add the push method
        
```
<details><summary><b>Solution</b></summary>
<p>

```Python 
class Stack:
    
    def __init__(self):
        self.head = None
        self.num_elements = 0
        
    def push(self, value):
        new_node = Node(value)        
        # if stack is empty
        if self.head is None:
            self.head = new_node
        else:
            new_node.next = self.head    # place the new node at the head of the linked list (top)
            self.head = new_node

        self.num_elements += 1
```
</p>
</details>

___

##### 4. Add the `size` and `is_empty` methods

When we implemented a stack using an array, we had these same methods. They will work the same here--they aren't affected by the use of a linked list versus an array. 

* Add a `size` method that returns the current size of the stack 
* Add an `is_empty` method that returns `True` if the stack is empty and `False` otherwise. 

```Python 
class Stack:
    
    def __init__(self):
        self.head = None
        self.num_elements = 0
        
    def push(self, value):
        new_node = Node(value)
        # if stack is empty
        if self.head is None:
            self.head = new_node
        else:
            new_node.next = self.head # place the new node at the head (top) of the linked list
            self.head = new_node

        self.num_elements += 1
        
    # TODO: Add the size method
    
    # TODO: Add the is_empty method
```
 <details><summary><b>Solution</b></summary>
<p>


```Python
class Stack:
    
    def __init__(self):
        self.head = None
        self.num_elements = 0
        
    def push(self, value):
        new_node = Node(value)
        # if stack is empty
        if self.head is None:
            self.head = new_node
        else:
            new_node.next = self.head # place the new node at the head (top) of the linked list
            self.head = new_node

        self.num_elements += 1
    
    def size(self):
        return self.num_elements
    
    def is_empty(self):
        return self.num_elements == 0
```
</p>
</details>

___

##### 5. Add the `pop` method

THe last thing we want to do is add the `pop` method. 

**Walkthrough**


___


THe method needs to:

* Check if the stack is empty and , if it is, return `None`
* Get the value from the `head` node and put it in a local variable
* Move the `head` so that it refers to the next item in the list
* Return the value we got earlier 

```Python 
class Stack:
    
    def __init__(self):
        self.head = None
        self.num_elements = 0
        
    def push(self, value):
        new_node = Node(value)
        # if stack is empty
        if self.head is None:
            self.head = new_node
        else:
            new_node.next = self.head # place the new node at the head (top) of the linked list
            self.head = new_node

        self.num_elements += 1
        
    # TODO: Add the pop method
    
    def size(self):
        return self.num_elements
    
    def is_empty(self):
        return self.num_elements == 0
```
<details><summary><b>Solution</b></summary>
<p>


```Python
class Stack:
    
    def __init__(self):
        self.head = None
        self.num_elements = 0
        
    def push(self, value):
        new_node = Node(value)
        # if stack is empty
        if self.head is None:
            self.head = new_node
        else:
            new_node.next = self.head # place the new node at the head (top) of the linked list
            self.head = new_node

        self.num_elements += 1
        
    def pop(self):
        if self.is_empty():
            return
        
        value = self.head.value # copy data to a local variable
        self.head = self.head.next # move head pointer to point to next node (top is removed by doing so)
        self.num_elements -= 1
        return value
    
    def size(self):
        return self.num_elements
    
    def is_empty(self):
        return self.num_elements == 0
```
</p>
</details>

___

**Test it!** 

Now that the `Stack` class is completed, let's test it to make sure it all works as expected. 

```Python 
# Setup
stack = Stack()
stack.push(10)
stack.push(20)
stack.push(30)
stack.push(40)
stack.push(50)

# Test size
print ("Pass" if (stack.size() == 5) else "Fail")

# Test pop
print ("Pass" if (stack.pop() == 50) else "Fail")

# Test push
stack.push(60)
print ("Pass" if (stack.pop() == 60) else "Fail")
print ("Pass" if (stack.pop() == 40) else "Fail")
print ("Pass" if (stack.pop() == 30) else "Fail")
stack.push(50)
print ("Pass" if (stack.size() == 3) else "Fail")
```

Pass 
Pass
Pass 
Pass 
Pass 
Pass

**Time complexity of stacks using linked lists**

___

Notice that if we pop or push an element with this stack, there's no traveral. We simply add or remove the item from the head of the linked list, and update the `head` reference. So with out linked list implementation, `pop` and `push` have time complexity of O(1). 

Also notice that using a linked list avoids the issue we ran into when we implemented our stack using an array. In that case, adding an item to the stack was fine--until we ran out of space. Then we would have to create an entirely new (larger) array and copy over all of the references from the old array. 

That happened because, with an array, we had to specify some inital size (in other words, we had to set aside a contiguous block of memory in advance). But with a linked list, the nodes do not need to be contiguous. They can be scattered in different locations of memory, an d that works just fine. This means that with a linked list, we can simply append as many nodes as we like. Using that as the underlying data structure for our stack means that we never run out of capacity, so pushing and popping items will always have a *time complexity* of **O(1)**

___

### 5. Build a Stack

**Building a Stack in Python**

Before we start let us reiterate they key components of a stack. A stack is a data structure that consists of two main operations: push and pop. A push is when you add an element to the **top of the stack** and a pop is when you remove an element from the **top of the stack**. Python 3.x conviently allows us to demonstate this functionality with a list. When you have a list such as [2,4,5,6] you can decide which end of the list is the bottom and the top of the stack respectivley. Once you decide that, you can use the append, pop or insert function to simulate a stack. We will choose the first element to be the bottom of our stack and therefore be using the append and pop functions to simulate it. Give it a try by implementing the function below!

```Python 
class Stack:
    def __init__(self):
         # TODO: Initialize the Stack
    
    def size(self):
         # TODO: Check the size of the Stack
    
    def push(self, item):
         # TODO: Push item onto Stack

    def pop(self):
         # TODO: Pop item off of the Stack
```
Test the Stack

```Python
MyStack = Stack()

MyStack.push("Web Page 1")
MyStack.push("Web Page 2")
MyStack.push("Web Page 3")

print (MyStack.items)

MyStack.pop()
MyStack.pop()

print ("Pass" if (MyStack.items[0] == 'Web Page 1') else "Fail")

MyStack.pop()

print ("Pass" if (MyStack.pop() == None) else "Fail") 
```

---------------------------------------------------------------------------
NameError                                 Traceback (most recent call last)
<ipython-input-1-161b6dd35e6f> in <module>()
----> 1 MyStack = Stack()
      2 
      3 MyStack.push("Web Page 1")
      4 MyStack.push("Web Page 2")
      5 MyStack.push("Web Page 3")

NameError: name 'Stack' is not defined

___

<details><summary><b>Solution</b></summary>
<p>


```Python
# Solution

class Stack:
    def __init__(self):
        self.items = []
    
    def size(self):
        return len(self.items)
    
    def push(self, item):
        self.items.append(item)

    def pop(self):
        if self.size()==0:
            return None
        else:
            return self.items.pop()
        
MyStack = Stack()

MyStack.push("Web Page 1")
MyStack.push("Web Page 2")
MyStack.push("Web Page 3")

print (MyStack.items)

MyStack.pop()
MyStack.pop()

print ("Pass" if (MyStack.items[0] == 'Web Page 1') else "Fail")

MyStack.pop()

print ("Pass" if (MyStack.pop() == None) else "Fail")# Solution

class Stack:
    def __init__(self):
        self.items = []
    
    def size(self):
        return len(self.items)
    
    def push(self, item):
        self.items.append(item)

    def pop(self):
        if self.size()==0:
            return None
        else:
            return self.items.pop()
        
MyStack = Stack()

MyStack.push("Web Page 1")
MyStack.push("Web Page 2")
MyStack.push("Web Page 3")

print (MyStack.items)

MyStack.pop()
MyStack.pop()

print ("Pass" if (MyStack.items[0] == 'Web Page 1') else "Fail")

MyStack.pop()

print ("Pass" if (MyStack.pop() == None) else "Fail")# Solution

class Stack:
    def __init__(self):
        self.items = []
    
    def size(self):
        return len(self.items)
    
    def push(self, item):
        self.items.append(item)

    def pop(self):
        if self.size()==0:
            return None
        else:
            return self.items.pop()
        
MyStack = Stack()

MyStack.push("Web Page 1")
MyStack.push("Web Page 2")
MyStack.push("Web Page 3")

print (MyStack.items)

MyStack.pop()
MyStack.pop()

print ("Pass" if (MyStack.items[0] == 'Web Page 1') else "Fail")

MyStack.pop()

print ("Pass" if (MyStack.pop() == None) else "Fail")
```
</p>
</details>

___

### 6. Practice: Balanced Parentheses 

Exercise:

In this exercise you are going to apply what you learned about stacks with a real world problem. We will be using stacks to make sure the parentheses are balanced in mathematical expressions such as:  `((32+8)∗(5/2))/(2+6)`.  In real life you can see this extend to many things such as text editor plugins and interactive development environments for all sorts of bracket completion checks.

Take a string as an input and return True if it's parentheses are balanced or `False` if it is not.

Try to code up a solution and pass the test cases.

**Code**

```Python
# Our Stack Class - Brought from previous concept
# No need to modify this
class Stack:
    def __init__(self):
        self.items = []
    
    def size(self):
        return len(self.items)
    
    def push(self, item):
        self.items.append(item)

    def pop(self):
        if self.size()==0:
            return None
        else:
            return self.items.pop()

def equation_checker(equation):
    """
    Check equation for balanced parentheses

    Args:
       equation(string): String form of equation
    Returns:
       bool: Return if parentheses are balanced or not
    """
    
    
    # TODO: Intiate stack object
    
    # TODO: Interate through equation checking parentheses
    
    # TODO: Return True if balanced and False if not
    
    pass
```

**Test Cases**

```Python 
print ("Pass" if (equation_checker('((3^2 + 8)*(5/2))/(2+6)')) else "Fail")
print ("Pass" if not (equation_checker('((3^2 + 8)*(5/2))/(2+6))')) else "Fail")
```

<details><summary><b>Solution</b></summary>
<p>


```Python
# Solution

# Our Stack Class
class Stack:
    def __init__(self):
        self.items = []

    def size(self):
        return len(self.items)

    def push(self, item):
        self.items.append(item)

    def pop(self):
        if self.size()==0:
            return None
        else:
            return self.items.pop()


def equation_checker(equation):
    """
    Check equation for balanced parentheses

    Args:
       equation(string): String form of equation
    Returns:
       bool: Return if parentheses are balanced or not
    """
    
    stack = Stack()

    for char in equation:
        if char == "(":
            stack.push(char)
        elif char == ")":
            if stack.pop() == None:
                return False

    if stack.size() == 0:
        return True
    else:
        return False


print ("Pass" if (equation_checker('((3^2 + 8)*(5/2))/(2+6)')) else "Fail")
print ("Pass" if not (equation_checker('((3^2 + 8)*(5/2))/(2+6))')) else "Fail")
```
</p>
</details>

___

### 7. Reverse Polish Notation 

**Reverse Polish notation**, also referred to as **Polish postfix notation** is a way of laying out operators and operands.

When making mathematical expressions, we typically put arithmetic operators (like `+`, `-`, `*`, and `/`) between operands. For example: `5 + 7 - 3 * 8`

However, in Reverse Polish Notation, the operators come after the operands. For example: `3 1 + 4 *`

The above expression would be evaluated as `(3 + 1) * 4 = 16`

The goal of this exercise is to create a function that does the following:

Given a postfix expression as input, evaluate and return the correct final answer.

>**Note:** In Python 3, the division operator / is used to perform float division. So for this problem, you should use int() after every division to convert the answer to an integer.

```Python 
class LinkedListNode:

    def __init__(self, data):
        self.data = data
        self.next = None

class Stack:

    def __init__(self):
        self.num_elements = 0
        self.head = None

    def push(self, data):
        new_node = LinkedListNode(data)
        if self.head is None:
            self.head = new_node
        else:
            new_node.next = self.head
            self.head = new_node
        self.num_elements += 1

    def pop(self):
        if self.is_empty():
            return None
        temp = self.head.data
        self.head = self.head.next
        self.num_elements -= 1
        return temp

    def top(self):
        if self.head is None:
            return None
        return self.head.data

    def size(self):
        return self.num_elements

    def is_empty(self):
        return self.num_elements == 0
```

```Python
def evaluate_post_fix(input_list):
    """
    Evaluate the postfix expression to find the answer

    Args:
       input_list(list): List containing the postfix expression
    Returns:
       int: Postfix expression solution
    """
    # TODO: Iterate over elements 
    
    # TODO: Use stacks to control the element positions
    
    pass
```

```Python
 def test_function(test_case):
    output = evaluate_post_fix(test_case[0])
    print(output)
    if output == test_case[1]:
        print("Pass")
    else:
        print("Fail")
```

```Python
 test_case_1 = [["3", "1", "+", "4", "*"], 16]

test_function(test_case_1)
```

```Python
 test_case_2 = [["4", "13", "5", "/", "+"], 6]
test_function(test_case_2)
```

```Python
 test_case_3 = [["10", "6", "9", "3", "+", "-11", "*", "/", "*", "17", "+", "5", "+"], 22]
test_function(test_case_3)
```

<details><summary><b>Solution</b></summary>
<p>


```Python
def evaluate_post_fix(input_list):
    stack = Stack()
    for element in input_list:
        if element == '*':
            second = stack.pop()
            first = stack.pop()
            output = first * second
            stack.push(output)
        elif element == '/':
            second = stack.pop()
            first = stack.pop()
            output = int(first / second)
            stack.push(output)
        elif element == '+':
            second = stack.pop()
            first = stack.pop()
            output = first + second
            stack.push(output)
        elif element == '-':
            second = stack.pop()
            first = stack.pop()
            output = first - second
            stack.push(output)
        else:
            stack.push(int(element))
    return stack.pop()
```
</p>
</details>

___

### 8. Reverse a Stack

**Problem Statement**

Reverse a stack. If your stack initially has `1, 2, 3, 4` (4 at the top and 1 at the bottom), after reversing the order must be `4, 3, 2, 1`(4 at the bottom and 1 at the top).

```Python 
class LinkedListNode:

    def __init__(self, data):
        self.data = data
        self.next = None

class Stack:

    def __init__(self):
        self.num_elements = 0
        self.head = None

    def push(self, data):
        new_node = LinkedListNode(data)
        if self.head is None:
            self.head = new_node
        else:
            new_node.next = self.head
            self.head = new_node
        self.num_elements += 1

    def pop(self):
        if self.is_empty():
            return None
        temp = self.head.data
        self.head = self.head.next
        self.num_elements -= 1
        return temp

    def top(self):
        if self.head is None:
            return None
        return self.head.data

    def size(self):
        return self.num_elements

    def is_empty(self):
        return self.num_elements == 0
```

```Python 
def reverse_stack(stack):
    """
    Reverse a given input stack

    Args:
       stack(stack): Input stack to be reversed
    Returns:
       stack: Reversed Stack
    """
    
    # TODO: Write the reverse stack function
      
    pass
```

```Python 
def test_function(test_case):
    stack = Stack()
    for num in test_case:
        stack.push(num)
    
    reverse_stack(stack)
    index = 0
    while not stack.is_empty():
        popped = stack.pop()
        if popped != test_case[index]:
            print("Fail")
            return
        else:
            index += 1
    print("Pass")
   
```
```Python 
test_case_1 = [1, 2, 3, 4]
test_function(test_case_1)
```

```Python 
test_case_2 = [1]
test_function(test_case_2)
```

<details><summary><b>Solution</b></summary>
<p>


```Python
def reverse_stack(stack):
    holder_stack = Stack()
    while not stack.is_empty():
        popped_element = stack.pop()
        holder_stack.push(popped_element)
    _reverse_stack_recursion(stack, holder_stack)


def _reverse_stack_recursion(stack, holder_stack):
    if holder_stack.is_empty():
        return
    popped_element = holder_stack.pop()
    _reverse_stack_recursion(stack, holder_stack)
    stack.push(popped_element)
```
</p>
</details>


___

### 9. Minimum Bracket Reversals

**Problem Statment**

Given an input string consisting of only `{` and `}`, figure out the minimum number of reversals required to make the brackets balanced.

For example:

For `input_string = "}}}}`, the number of reversals required is `2`.
For `input_string = "}{}}`, the number of reversals required is `1`.
If the brackets cannot be balanced, return `-1` to indicate that it is not possible to balance them.

```Python 
class LinkedListNode:

    def __init__(self, data):
        self.data = data
        self.next = None

class Stack:

    def __init__(self):
        self.num_elements = 0
        self.head = None

    def push(self, data):
        new_node = LinkedListNode(data)
        if self.head is None:
            self.head = new_node
        else:
            new_node.next = self.head
            self.head = new_node
        self.num_elements += 1

    def pop(self):
        if self.is_empty():
            return None
        temp = self.head.data
        self.head = self.head.next
        self.num_elements -= 1
        return temp

    def top(self):
        if self.head is None:
            return None
        return self.head.data

    def size(self):
        return self.num_elements

    def is_empty(self):
        return self.num_elements == 0
```

```Python 
def minimum_bracket_reversals(input_string):
	"""
	Calculate the number of reversals to fix the brackets

	Args: 
	   input_string(string): Strings to be used for bracket reversal calculation
	Returns: 
	   int: Number of bracket reversals needed
	"""
	# TODO: Write function here
	 pass

```

```Python 
def test_function(test_case):
    input_string = test_case[0]
    expected_output = test_case[1]
    output = minimum_bracket_reversals(input_string)
    
    if output == expected_output:
        print("Pass")
    else:
        print("Fail")
```
```Python 
test_case_1 = ["}}}}", 2]
test_function(test_case_1)
```
```Python 
test_case_2 = ["}}{{", 2]          
test_function(test_case_2)
```
```Python 
test_case_2 = ["}}{{", 2]          
test_function(test_case_2)
```
```Python 
test_case_3 = ["{{{{{{{{{{{{{{{{{{{{{{{{{{{{{{{}}}}}", 13]

test_function(test_case_1)
```

```Python 
test_case_4= ["}{}{}{}{}{}{}{}{}{}{}{}{}{}{}{", 2]
test_function(test_case_2)
```

```Python
test_case_5 = ["}}{}{}{}{}{}{}{}{}{}{}{}{}{}{}", 1]

test_function(test_case_3)
```

<details><summary><b>Solution</b></summary>
<p>


```Python
def minimum_bracket_reversals(input_string):
    if len(input_string) % 2 == 1:
        return -1

    stack = Stack()
    count = 0
    for bracket in input_string:
        if stack.is_empty():
            stack.push(bracket)
        else:
            top = stack.top()
            if top != bracket:
                if top == '{':
                    stack.pop()
                    continue
            stack.push(bracket)

    ls = list()
    while not stack.is_empty():
        first = stack.pop()
        second = stack.pop()
        ls.append(first)
        ls.append(second)
        if first == '}' and second == '}':
            count += 1
        elif first == '{' and second == '}':
            count += 2
        elif first == '{' and second == '{':
            count += 1
    return count
```
</p>
</details>

___


### 10. Queues

First in, First out data structure a.k.a. a **Queue**

It's kind of an oppoiste of a stack. In a stack the most recently added element comes out first, but here in Queues the oldest element comes out first. 

The first or oldest element in a Queue, is called the **head**.

The last element in the queue or the newest element in the queue, is called the **tail**

When you add an element to the tail the operation is called an **enqueue**.

When you remove the head element, the operation is called **dequeue**.

There is also an operation called **peek**, where you look at the head element, but you don't actually remove it. 

You can implement this data structure with a linked list, where you also save references to the head and tail so you can look them both up in **constant time**

There are actually tow special types of queues that show up a lot. 

A **deck/deque(pronounced deck)** or **double-ended queue** is a queue that goes both ways. 

You can enqueue or dequeue from either end. 

A deck is a generalized version of both stacks and queues. 

Since, you can represent either of them with it, you could treak it like a stack and add and remove elements from the same end, or you could treat it like a queue and add elements on one end and remove them from the other. 

In a **Priority Queue**, you assign each element a numerical priority when you insert it into the queue. When you dequeue, you remove the element with the highest priority. 

If the elements have the same priority then the oldest element is the one that gets dequeued first. 

### 11. Implement a queue using an array

One way to implement a queue by using an array. 

**Walkthrough**


____


<-------  0,              0,               ,0       <------

Dequeue  Head                             Tail     Enqueue 
        (Front)                          (Back)


**Functionality**

Once implemented, our queue will need to have the following functionality:

1. `enqueue` - adds data to the back of the queue
2. `dequeue` - removes data from the front of the queue
3. `front` - returns the element at the front of the queue
4. `size` - returns the number of elements present in the queue
5. `is_empty` - returns True if there are no elements in the queue, and False otherwise
6. `_handle_full_capacity` - increases the capacity of the array, for cases in which the queue would otherwise overflow

Also, if the queue is empty, `dequeue` and `front` operations should return `None`.

##### 1. Create the `queue` class and its `__init__` method

<details><summary><b>Solution</b></summary>
<p>

```Python
class Queue:

    def __init__(self, initial_size=10):
        self.arr = [0 for _ in range(initial_size)]
        self.next_index = 0
        self.front_index = -1
        self.queue_size = 0
```
</p>
</details>

Let's check that the array is being initialized correctly. We can create a `Queue` object and access the `arr` attribute, and we should see our ten-element array:


```Python
q = Queue()
print(q.arr)
print("Pass" if q.arr == [0, 0, 0, 0, 0, 0, 0, 0, 0, 0] else "Fail")
```
q = Queue()
print(q.arr)
print("Pass" if q.arr == [0, 0, 0, 0, 0, 0, 0, 0, 0, 0] else "Fail")


##### 2. Add the `enqueue` method

The method should:

* Take a value as input and assign this value to the next free slot in the array
* Increment `queue_size`
* Increment `next_index` (this is where you'll need to use the modulo operator `%`)
* If the front index is `-1` (because the queue was empty), it should set the front index to `0`

```Python 
class Queue:

    def __init__(self, initial_size=10):
        self.arr = [0 for _ in range(initial_size)]
        self.next_index = 0
        self.front_index = -1
        self.queue_size = 0

    # TODO: Add the enqueue method
```
<details><summary><b>Solution</b></summary>
<p>

```Python
class Queue:

    def __init__(self, initial_size=10):
        self.arr = [0 for _ in range(initial_size)]
        self.next_index = 0
        self.front_index = -1
        self.queue_size = 0

    def enqueue(self, value):
        # enqueue new element
        self.arr[self.next_index] = value
        self.queue_size += 1
        self.next_index = (self.next_index + 1) % len(self.arr)
        if self.front_index == -1:
            self.front_index = 0
```
</p>
</details>

___

##### 3. Add the `size`, `is_empty` and `front` methods

Just like with stacks, we need methods to keep track of the size of the queue and whether it is empty. We can also add a `front` method that returns the value of the front element.

* Add a `size method` that returns the current size of the queue
* Add an `is_empty` method that returns `True` if the queue is empty and `False` otherwise
* Add a `front` method that returns the value for the front element (whatever item is located at the `front_index` position). If the queue is empty, the `front` method should return None.

```Python
class Queue:

    def __init__(self, initial_size=10):
        self.arr = [0 for _ in range(initial_size)]
        self.next_index = 0
        self.front_index = -1
        self.queue_size = 0

    def enqueue(self, value):
        # enqueue new element
        self.arr[self.next_index] = value
        self.queue_size += 1
        self.next_index = (self.next_index + 1) % len(self.arr)
        if self.front_index == -1:
            self.front_index = 0
            
    # TODO: Add the size method
    
    # TODO: Add the is_empty method

    # TODO: Add the front method
```
<details><summary><b>Solution</b></summary>
<p>

```Python
class Queue:

    def __init__(self, initial_size=10):
        self.arr = [0 for _ in range(initial_size)]
        self.next_index = 0
        self.front_index = -1
        self.queue_size = 0

    def enqueue(self, value):
        # enqueue new element
        self.arr[self.next_index] = value
        self.queue_size += 1
        self.next_index = (self.next_index + 1) % len(self.arr)
        if self.front_index == -1:
            self.front_index = 0

    def size(self):
        return self.queue_size

    def is_empty(self):
        return self.size() == 0
    
    def front(self):
        # check if queue is empty
        if self.is_empty():
            return None
        return self.arr[self.front_index]
```
</p>
</details>

___

##### 4. Add the `dequeue` method

Here's what it should do:

* If the queue is empty, reset the `front_index` and `next_index` and then simply return `None`. Otherwise...
* Get the value from the front of the queue and store this in a local variable (to return later)
* Shift the `head` over so that it refers to the next index
* Update the `queue_size` attribute
* Return the value that was dequeued

```Python
class Queue:

    def __init__(self, initial_size=10):
        self.arr = [0 for _ in range(initial_size)]
        self.next_index = 0
        self.front_index = -1
        self.queue_size = 0

    def enqueue(self, value):
        # enqueue new element
        self.arr[self.next_index] = value
        self.queue_size += 1
        self.next_index = (self.next_index + 1) % len(self.arr)
        if self.front_index == -1:
            self.front_index = 0
            
    # TODO: Add the dequeue method

    def size(self):
        return self.queue_size

    def is_empty(self):
        return self.size() == 0
    
    def front(self):
        # check if queue is empty
        if self.is_empty():
            return None
        return self.arr[self.front_index]
```

<details><summary><b>Solution</b></summary>
<p>

```Python
class Queue:

    def __init__(self, initial_size=10):
        self.arr = [0 for _ in range(initial_size)]
        self.next_index = 0
        self.front_index = -1
        self.queue_size = 0

    def enqueue(self, value):
        # enqueue new element
        self.arr[self.next_index] = value
        self.queue_size += 1
        self.next_index = (self.next_index + 1) % len(self.arr)
        if self.front_index == -1:
            self.front_index = 0
            
    def dequeue(self):
        # check if queue is empty
        if self.is_empty():
            self.front_index = -1   # resetting pointers
            self.next_index = 0
            return None

        # dequeue front element
        value = self.arr[self.front_index]
        self.front_index = (self.front_index + 1) % len(self.arr)
        self.queue_size -= 1
        return value

    def size(self):
        return self.queue_size

    def is_empty(self):
        return self.size() == 0
    
    def front(self):
        # check if queue is empty
        if self.is_empty():
            return None
        return self.arr[self.front_index]
```
</p>
</details>

___

##### 5. Add the `_handle_queue_capacity_full` method

First, define the `_handle_queue_capacity_full` method:

* Define an `old_arr` variable and assign the the current (full) array so that we have a copy of it
* Create a new (larger) array and assign it to `arr`.
* Iterate over the values in the old array and copy them to the new array. Remember that you'll need two for loops for this.

Then, in the `enqueue` method:

* Add a conditional to check if the queue is full; if it is, call  `_handle_queue_capacity_full`

```Python 
class Queue:

    def __init__(self, initial_size=10):
        self.arr = [0 for _ in range(initial_size)]
        self.next_index = 0
        self.front_index = -1
        self.queue_size = 0

    def enqueue(self, value):
        # TODO: Check if the queue is full; if it is, call the _handle_queue_capacity_full method

        # enqueue new element
        self.arr[self.next_index] = value
        self.queue_size += 1
        self.next_index = (self.next_index + 1) % len(self.arr)
        if self.front_index == -1:
            self.front_index = 0

    def dequeue(self):
        # check if queue is empty
        if self.is_empty():
            self.front_index = -1   # resetting pointers
            self.next_index = 0
            return None

        # dequeue front element
        value = self.arr[self.front_index]
        self.front_index = (self.front_index + 1) % len(self.arr)
        self.queue_size -= 1
        return value

    def size(self):
        return self.queue_size

    def is_empty(self):
        return self.size() == 0
    
    def front(self):
        # check if queue is empty
        if self.is_empty():
            return None
        return self.arr[self.front_index]

    # TODO: Add the _handle_queue_capacity_full method
```
<details><summary><b>Solution</b></summary>
<p>

```Python
class Queue:

    def __init__(self, initial_size=10):
        self.arr = [0 for _ in range(initial_size)]
        self.next_index = 0
        self.front_index = -1
        self.queue_size = 0

    def enqueue(self, value):
        # if queue is already full --> increase capacity
        if self.queue_size == len(self.arr):
            self._handle_queue_capacity_full()

        # enqueue new element
        self.arr[self.next_index] = value
        self.queue_size += 1
        self.next_index = (self.next_index + 1) % len(self.arr)
        if self.front_index == -1:
            self.front_index = 0

    def dequeue(self):
        # check if queue is empty
        if self.is_empty():
            self.front_index = -1   # resetting pointers
            self.next_index = 0
            return None

        # dequeue front element
        value = self.arr[self.front_index]
        self.front_index = (self.front_index + 1) % len(self.arr)
        self.queue_size -= 1
        return value

    def size(self):
        return self.queue_size

    def is_empty(self):
        return self.size() == 0
    
    def front(self):
        # check if queue is empty
        if self.is_empty():
            return None
        return self.arr[self.front_index]

    def _handle_queue_capacity_full(self):
        old_arr = self.arr
        self.arr = [0 for _ in range(2 * len(old_arr))]

        index = 0

        # copy all elements from front of queue (front-index) until end
        for i in range(self.front_index, len(old_arr)):
            self.arr[index] = old_arr[i]
            index += 1

        # case: when front-index is ahead of next index
        for i in range(0, self.front_index):
            self.arr[index] = old_arr[i]
            index += 1

        # reset pointers
        self.front_index = 0
        self.next_index = index
```
</p>
</details>

___

**Test your queue**

```Python 
# Setup
q = Queue()
q.enqueue(1)
q.enqueue(2)
q.enqueue(3)

# Test size
print ("Pass" if (q.size() == 3) else "Fail")

# Test dequeue
print ("Pass" if (q.dequeue() == 1) else "Fail")

# Test enqueue
q.enqueue(4)
print ("Pass" if (q.dequeue() == 2) else "Fail")
print ("Pass" if (q.dequeue() == 3) else "Fail")
print ("Pass" if (q.dequeue() == 4) else "Fail")
q.enqueue(5)
print ("Pass" if (q.size() == 1) else "Fail")
```
Pass
Pass
Pass
Pass
Pass
Pass

___

### 12. Build a queue using a linked list

By now, you may be noticing a pattern. Earlier, we had you implement a stack using an array and a linked list. Here, we're doing the same thing with queues: In the previous notebook, you implemented a queue using an array, and in this notebook we'll implement one using a linked list.

It's good to try implementing the same data structures in multiple ways. This helps you to better understand the abstract concepts behind the data structure, separate from the details of their implementation—and it also helps you develop a habit of comparing pros and cons of different implementations.

With both stack and queues, we saw that trying to use arrays introduced some concerns regarding the time complexity, particularly when the initial array size isn't large enough and we need to expand the array in order to add more items.

With our stack implementation, we saw that linked lists provided a way around this issue—and exactly the same thing is true with queues.

##### 1. Define a `Node` class 

Since we'll be implementing a linked list for this, we know that we'll need a `Node` class like we used earlier in this lesson. 

<details><summary><b>Solution</b></summary>
<p>

```Python
class Node:
    
    def __init__(self, value):
        self.value = value
        self.next = None
```
</p>
</details>

___

##### 2. Create the `Queue` class and it's `__init__` method

It will need three attributes:

* A `head` attribute to keep track of the first node in the linked list
* A `tail` attribute to keep track of the last node in the linked list
* A `num_elements` attribute to keep track of how many items are in the stack

<details><summary><b>Solution</b></summary>
<p>

```Python
class Queue:
    
    def __init__(self):
        self.head = None
        self.tail = None
        self.num_elements = 0
```
</p>
</details>

___

##### 3. Add the `enqueue` method 

In the cell below, see if you can figure out how to write the `enqueue` method.

Remember, the purpose of this method is to add a new item to the back of the queue. Since we're using a linked list, this is equivalent to creating a new node and adding it to the tail of the list.

Some things to keep in mind:

* If the queue is empty, then both the `head` and `tail` should refer to the new node (because when there's only one node, this node is both the head and the tail)
* Otherwise (if the queue has items), add the new node to the tail (i.e., to the end of the queue)
* Be sure to shift the `tail` reference so that it refers to the new node (because it is the new tail)

```Python
class Queue:
    
    def __init__(self):
        self.head = None
        self.tail = None
        self.num_elements = 0
        
    # TODO: Add the enqueue method
```

<details><summary><b>Solution</b></summary>
<p>

```Python
class Queue:
    
    def __init__(self):
        self.head = None
        self.tail = None
        self.num_elements = 0
        
    def enqueue(self, value):
        new_node = Node(value)
        if self.head is None:
            self.head = new_node
            self.tail = self.head
        else:
            self.tail.next = new_node    # add data to the next attribute of the tail (i.e. the end of the queue)
            self.tail = self.tail.next   # shift the tail (i.e., the back of the queue)
        self.num_elements += 1
```
</p>
</details>

___

##### 4. Add the `size` and `is_empty` methods

* Add a `size` method that returns the current size of the stack
* Add an `is_empty` method that returns `True` if the stack is empty and `False` otherwise

We'll make use of these methods in a moment when we write the `dequeue` method.

```Python
class Queue:
    
    def __init__(self):
        self.head = None
        self.tail = None
        self.num_elements = 0
        
    def enqueue(self, value):
        new_node = Node(value)
        if self.head is None:
            self.head = new_node
            self.tail = self.head
        else:
            self.tail.next = new_node    # add data to the next attribute of the tail (i.e. the end of the queue)
            self.tail = self.tail.next   # shift the tail (i.e., the back of the queue)
        self.num_elements += 1
    
    # TODO: Add the size method
    
    # TODO: Add the is_empty method
```

<details><summary><b>Solution</b></summary>
<p>

```Python
class Queue:
    
    def __init__(self):
        self.head = None
        self.tail = None
        self.num_elements = 0
        
    def enqueue(self, value):
        new_node = Node(value)
        if self.head is None:
            self.head = new_node
            self.tail = self.head
        else:
            self.tail.next = new_node    # add data to the next attribute of the tail (i.e. the end of the queue)
            self.tail = self.tail.next   # shift the tail (i.e., the back of the queue)
        self.num_elements += 1
    
    def size(self):
        return self.num_elements
    
    def is_empty(self):
        return self.num_elements == 0
```
</p>
</details>

___

##### 5. Add the `dequeue` method

* If the queue is empty, it should simply return `None`. Otherwise...
* Get the value from the front of the queue (i.e., the head of the linked list)
* Shift the `head` over so that it refers to the next node
* Update the `num_elements` attribute
* Return the value that was dequeued

```Python
class Queue:
    
    def __init__(self):
        self.head = None
        self.tail = None
        self.num_elements = 0
        
    def enqueue(self, value):
        new_node = Node(value)
        if self.head is None:
            self.head = new_node
            self.tail = self.head
        else:
            self.tail.next = new_node    # add data to the next attribute of the tail (i.e. the end of the queue)
            self.tail = self.tail.next   # shift the tail (i.e., the back of the queue)
        self.num_elements += 1
            
    # Add the dequeue method
    
    def size(self):
        return self.num_elements
    
    def is_empty(self):
        return self.num_elements == 0
        
```

<details><summary><b>Solution</b></summary>
<p>

```Python
class Queue:
    
    def __init__(self):
        self.head = None
        self.tail = None
        self.num_elements = 0
        
    def enqueue(self, value):
        new_node = Node(value)
        if self.head is None:
            self.head = new_node
            self.tail = self.head
        else:
            self.tail.next = new_node    # add data to the next attribute of the tail (i.e. the end of the queue)
            self.tail = self.tail.next   # shift the tail (i.e., the back of the queue)
        self.num_elements += 1
            
    def dequeue(self):
        if self.is_empty():
            return None
        value = self.head.value          # copy the value to a local variable
        self.head = self.head.next       # shift the head (i.e., the front of the queue)
        self.num_elements -= 1
        return value
    
    def size(self):
        return self.num_elements
    
    def is_empty(self):
        return self.num_elements == 0
```
</p>
</details>

___

**Test it!**

Code to check if the implementation works:

```Python

# Setup
q = Queue()
q.enqueue(1)
q.enqueue(2)
q.enqueue(3)

# Test size
print ("Pass" if (q.size() == 3) else "Fail")

# Test dequeue
print ("Pass" if (q.dequeue() == 1) else "Fail")

# Test enqueue
q.enqueue(4)
print ("Pass" if (q.dequeue() == 2) else "Fail")
print ("Pass" if (q.dequeue() == 3) else "Fail")
print ("Pass" if (q.dequeue() == 4) else "Fail")
q.enqueue(5)
print ("Pass" if (q.size() == 1) else "Fail")
```

**Time Complexity**

So what's the time complexity of adding or removing things from our queue here?

Well, when we use `enqueue`, we simply create a new node and add it to the tail of the list. And when we `dequeue` an item, we simply get the value from the head of the list and then shift the `head` variable so that it refers to the next node over.

Both of these operations happen in constant time—that is, they have a *time-complexity* of **O(1)**.





