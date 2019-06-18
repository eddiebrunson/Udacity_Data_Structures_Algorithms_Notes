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

### 1. Create and initialize the `Stack` class

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

### 2. Add the `push` method

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


### 3. Handle full capacity 

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

### 4. Add the `size` and `is_empty` methods

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

### 5. Add the `pop` method

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