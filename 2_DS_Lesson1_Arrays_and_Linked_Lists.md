# 2. Data Structures

## Lesson 1: Arrays and Linked Lists

**Why data structures?**

### 1. Lists 

*Data Structures* are containers that organize and group data together in different ways. When you write code to solve a problem, there will always be data involved--and how you store or structure that data in the computer's memory can have a huge impact on what kinds of things you can do with it and how efficiently you can do those things. 

**Properties of collections**

* Don't have a particular order (so you can't say "give me the 3rd element in this collection")
* Don't have to have objects of the same type

There are many data structures that add rules to collections to be used in programming. 

___

### 2. Lists

Have all of the properties of a collection. It havs a group of things but the objects have order. 

A shopping list has a lot of the same properties as the lists.

Different programming languages treat lists differently. 

**Properties of lists**

* Have an **order** (so you can say things like "give me the 3rd item in the list")

* Have **no fixed** length (you can add or remove elements)

___

### 3. Arrays

**Arrays vs. lists vs. Python lists**

The distinction between arrays and lists can be a little confusing, especially because of how Python implements the data structure it calls a "list". 

**Arrays**

An array has some things in common with a list. In both cases:

* There is a collection of items 
* there items have an order to them

One of the key differences is that *arrays* have indexes, while lists do not. 

To understand this, it helps to know how arrays are stored in memory. When an arrays is created, it is always given some initial size--that is, the number of elements it should be able to hold (and how large each element is). The computer then finds a block of memory and sets aside the space for the array. 

Importantly, the space that gets set aside is one, continuous block. That is, all of the elements of the array are *contiguous*, meaning that they are all next to one another in memory>

Another key characteristic of an array is that all of the elements are the same size. 

When we represent an array visually, we often draw it as a series of boxes that are all the same size and all right next to one another:



Because all of the elements are 1) next to one another and 2) the same size, this means that if we know the location of the first element, we can calculate the location of any other element. 

For example, if the first element in the array is a memory location `00` and the elements are 24 bytes, then the next element would be at location 00 + 24 = `24`. An the one after that would be at 24 + 24 = `48`, and so on. 

Since we can easily calculate the location of any item in the array, we can assign each item an index and use that index to quickly and directly access the item. 

___

**Lists**

In contrast, the elements of a list may or may not be next to one another in mememory! For example, later on we will look at *linked lists*, where each list item points to the next list item--but where the items themselves may be scattered in different locations of memory. In this case, knowing the location of the first item in the list does not mean you can simply calculate the location of the other items. This means we cannot use indexes to directly access the list items as we would in an array.

___


**Python lists**
 
 In Python, we can create a list using square brackets `[]`. For example:

```Python
>>> my_list = ['a', 'b', 'c']
>>> my_list
['a', 'b', 'c']
```

And then we can access an item in the list by providing an index for that item:

```Python
>>> my_list[0]
'a'
>>> my_list[1]
'b'
>>> my_list[2]
'c'
```

But wait, didn't we just say that lists *don't* have indexes!? This seems to directly contradict that dinstinction. 

The reason for this confusion is simply one of terminology. THe earlier description we gave of lists is correct in *general* --that is, usually when you hear someone refer to something as a "list", that is what they mean. However, in Python the term is used differently. 

We will not get into all of the details, but the important thing you need to know is the following: If you were to look under the hood, you would find that a **Python list is essentially implemented like an array**(specifically, it behaves like a *dynamic array*) In particular, **the elements of a Python list are contiguous in memory, and they can be accessed using an index.**

In addition to the underlying array, a Python list also includes some additional behavior. For example, you can use things like`pop` and `append` methods on a Python list to add or remove items. using those methods, you can essentially utilize a Python list like a stack( which is another data structure).

In generally, we will try to avoid using things like `pop` and `append`, because these are high-level language features that may not be available to you in other languages. In most cases, we will ignore the extra functionality that comes with Python lists, and instead use them **as if they were simple arrays.** This allows us to see how the underlying data structures work, regardless of the language you are using to implement those structures. 

___

Arrays are the most common implementations of lists. 

In many programming languages arrays are built in as a core feature. 

In some langauges you can only have objects of the same type in the same array. And in some langauages your array can contain different types.

Insertions and deletions can be really messy with arrays. Inserting in the end is often easy but it can be hard if the arrays has a set size and you've alread filled it up. 

Insertion is difficult if you want to put an element in the middle of the array. If you want to do a normal insert you'll have to move everything after the inserted element back into different boxes with a different index. 

The operation as a whole is pretty inefficient since you need to move every element behind the one you're inserting back in the array. 

In the worst case this operation take *linear time or big O of n.*

Deletion causes a similar problem. If you delete an element you will have an empty box. 

You can't just look at the index and say that this is the fourth element anymore since there is an empty box before it. This can change based on the way a particular language implements an array but it's important to consider when talking abour arrays abstractly. 
___

In summary:

* Python lists are essentially arrays, but also include additional high-level functionality

* For this course, we will generally ignore this high-level functionality and treat Python lists as if they were simple arrays. 

### 4. Strings Exercises

**Intro**

Strings in Python are arrays of bytes representing unicode characaters. In this exercise we are going to practice our work with string manipulation. 

**Reverse Strings**

In the first exercise, the goal is to write a function that takes a string as input and then returns the reversed string. 

For example, if the input is the string `"water"`, then the output should be `"retaw"`.

While working on the function and trying to figure out how to manipulate the string, it may help to use the `print` statement so you can see the effects of whatever you are trying. 

```Python

def string_reverser(our_string):

	"""
	Reverse the input string 

	Args: 
	   our_string(string): String to be reversed 
	Returns: 
	   string: The reversed string
	"""

	# TODO: Write your solution here 

	pass

# Test Cases

print ("Pass" if ('retaw' == string_reverser('water')) else "Fail")
print ("Pass" if ('!noitalupinam gnirts gnicitcarP' == string_reverser('Practicing string manipulation!')) else "Fail")
print ("Pass" if ('3432 :si edoc esuoh ehT' == string_reverser('The house code is: 2343')) else "Fail")
```

<details><summary><b>Solution</b></summary>
<p>

```Python 

# TODO




```
</p>
</details>

___

**Anagrams**

THe goal of this exercise if to write code to determine if two strings are anagrams of each other. 

An anagram is a word (or phrase) that is formed by rearranging the letters of another word (or phrase).

For example:

* "rat" is an anagram of "art"
* "alert" is an anagram of "alter"
* "Solt machines" is an anagram of "Cash lost in me"

Your function should take two strings as input and return `True` if they are not.

You can assume the following about the input strings:

* No punctuation 
* No numbers
* No special characters

```Python 
def anagram_checker(str1, str2):

	"""
    Check if the input strings are anagrams of each other

    Args:
       str1(string),str2(string): Strings to be checked
    Returns:
       bool: Indicates whether strings are anagrams
    """
    
    # TODO: Write your solution here
    
    pass

# Test Cases

print ("Pass" if not (anagram_checker('water','waiter')) else "Fail")
print ("Pass" if anagram_checker('Dormitory','Dirty room') else "Fail")
print ("Pass" if anagram_checker('Slot machines', 'Cash lost in me') else "Fail")
print ("Pass" if not (anagram_checker('A gentleman','Elegant men')) else "Fail")
print ("Pass" if anagram_checker('Time and tide wait for no man','Notified madman into water') else "Fail")
```


<details><summary><b>Solution</b></summary>
<p>

```Python 

# TODO




```
</p>
</details>


___


**Reverse the words in sentence**

Given a sentence, reverse each word in the sentence while keeping the order the same!


```Python
def word_flipper(our_string):

   """
   Flip the individual words in a sentence 

   Args:
      our_string(string): String with words to flip
   Return: 
      string: String with words flipped
   """

   # TODO: Write your solution here 

   pass

# Test Cases

print ("Pass" if ('retaw' == word_flipper('water')) else "Fail")
print ("Pass" if ('sihT si na elpmaxe' == word_flipper('This is an example')) else "Fail")
print ("Pass" if ('sihT si eno llams pets rof ...' == word_flipper('This is one small step for ...')) else "Fail")
```

<details><summary><b>Solution</b></summary>
<p>

```Python 

# TODO




```
</p>
</details>

___

**Hamming Distance**

In information theory, the Hamming distance between two strings of equal lengths is the number of positions at which the corresponding symbols are different. Calculate the Hamming distance for the following test cases. 

```Python 

def hamming_distance(str1, str2):
	"""
	Calculate the hamming distance of the two strings 

	Args:
	   str1(string), str2(string): Strings to be used for finding the hamming distance 
	Returns:
	   int: Hamming Distance 
	"""

	# TODO: Write your solution here

	pass

# Test Cases 

print ("Pass" if (10 == hamming_distance('ACTTGACCGGG', 'GATCCGGTACA')) else "Fail")
print ("Pass" if (1 == hamming_distance('shove', 'stove')) else "Fail")
print ("Pass" if (None == hamming_distance('Slot machines', 'Cash lost in me')) else "Fail")
print ("Pass" if (9 == hamming_distance(('A gentleman', 'Elegant men')) else "Fail"))
print ("Pass" if (2 == hamming_distance(('01011010100011101', '0101010100010001')) else "Fail"))
```

<details><summary><b>Solution</b></summary>
<p>

```Python 

# TODO




```
</p>
</details>

___

### 5. Linked Lists Introduction

You can think of an array as a set of boxes where each has an address called an index. 

A paper chaing is like a similar construct called a linked list. 

A linked list is an extension of a list, but is definitely not an array. 

There are still some things that have order, but there are no indices. 

A linked list is characterized by its links. 

Each element has some notion of waht the next element is since it's connected to it, but not necessarily how long the list is or where it is in the list. 

An array is different. There is nothing in one element of the array that says here's your next element. You know what the next element is by what the next index is. 

Adding or removing an element on a array is difficult. Although, adding or removing elements from a linked list turns out to be so simple. 

You could just take one element out or add one in. 

___

### 6. Linked Lists Continued 

The main difference between *linked lists* and *arrays*, is that each element stores different information. 

* It's important to know the differences between the two data structures as it is asked in interviews often. 


* It both cases a single element can store a value 
* In an **array** we store a number as an index 
* You can get the next element by querying the array for the element at index one in this case. 

Where as in a **linked list**, we store a reference to the next element in the list. In many languages this will look like assigning the actual next element as a proerty of this element. Way down at the hardware level your element actually has some space dedicated for it in memory. 

It's pretty easy to insert and delete elements. 

Adding an element changes the next reference to point to the new object and done. 

**Important** if you delete the next reference and replace it with a new object. You'll lose your reference to this object, you should always assign your next pointer for this element before you assign your next pointer for this element, so you don't lose your reference to th is one down here. 

* Note that insertion takes constant time in this case, since you are just shifting around pointers and not iterating over every element in the list. 

Removing an element is going to look pretty similar.

There is also something called a **Doubly linked lists**, where you have pointers to the next element and the previous element.

You can traverse the list in both directions now. 

* Be careful not to lose references when adding or removing elements but it's easier than performing these operation on an array. 


___


### Implement a Linked List 

Practice implementing a basic linked list:

  2 --> 1 --> 4 --> 3 --> 5 --> None 

Head

___

**Key characteristics**

Let's review the overall abstract concepts for this data structure. 



### 8. Types of Linked Lists

There versions of linked-lists:

* Singly-linked lists
* Doubly-linked lists
* Circular lists

**Singly Linked Lists**

In this linked list, each node in the list is connected only to the next node in the list. 

                             **Singly Linked List**

                          2 --> 1 --> 4 --> 3 --> 5
The connection is typyically implemented by setting the `next` attribute on a node object itself. 

```Python
class Node:
	def __init__(self, value):
		self.value = value 
		self.next = None

# A small linked list:


head = Node(1)
head.next = Node(2)
```

Above shows a simple linked list with two elements `[1, 2]`. Usually you'll want to create a `LinkedList` class as a wrapper for the nodes themselves and to provide common methods that operate on the list. For example you can implement an `append` method that adds a value to the end of the list. 

Note, that if we're only tracking the head of the list, this *runs in linear time -**O(N)*** since you have to iterate through the entire list to get to the tail node. However, prepending (adding to the head of the list) can be done in constant **O(1)** time. 

```Python 
class LinkedList:
	def __init__(self):
		self.head = None 

	def append(self, value):
		if self.head = Node(value)
		return 

    # Move to the tail (the last node)
    node = self.head 
    while node.next:
    	node = node.next 

   node.next = Node(value)
   return


linked_list = LinkedList()
linked_list.append(1)
linked_list.append(2)
linked_list.append(4)

node = linked_list.head
while node:
	print(node.value)
	node = node.next
```
**Exercise:** Add a method `to_list()` to `LinkedList` that converts a linked list back into a Python list.

```Python 
class LinkedList: 
	def __init__(self):
		self.head = None 

	def append(self, value):
		if self.head is None:
			self.head = Node(value)
			return

		# Move to the tail (the last node)
		node = self.head
		while node.next:
			node = node.next

		node.next = Node(value)
		return

	def to_list (self):

		# TODO: Write function to turn Linked List into Python List

		pass 

		# Test your method here 
		linked_list = LinkedList()
		linked_list.append(3)
		linked_list.append(2)
		linked_list.append(-1)
		linked_list.append(0.2)

		print ("Pass" if (linked_list.to_list() == [3, 2, -1, 0.2]) else "Fail")
```

<details><summary><b>Solution</b></summary>
<p>

```Python 

# TODO




```
</p>
</details>

___

**Doubly Linked Lists**

This type of list has connnections backwards and forwards through the list. 

                                     Doubly Linked List

                                     2 --> 1 --> 4 --> 3 --> 5 
                                      <--    <--   <--  <--

```Python 
class DoubleNode:
	def __init__(self, value):
		self.value = value 
		self.next = None 
		self.previous = None 
```

Now that we have backwards connections it makes sense to track the tail of the linked list as well as the head. 

**Exercise:** Implement a doubly linked list that can append to the tail in constant time. Make sure to include forward and backwards connections when adding a new node to the list. 

```Python 
class DoublyLinkedList: 
   def __init__(self, value):
       self.head = None  
       self.tail = None 

   def append(self, value):

      # TODO: Implement this method to append to the tail of the list 

      pass 

      # Test your class here 

      linked_list = DoublyLinkedList()
      linked_list.append(1)
      linked_list.append(-2)
      linked_list.append(4)

      print ("Going forward through the list, should print 1, -2, 4")
      node = linked_list.head
      while node:
         print(node.value)
         node.ext 
      print ("\nGoing backward through the list, should print 4, -2, 1")
      node = linked_list.tail
      while node: 
         print(node.value)
         node = node.previous

```


<details><summary><b>Solution</b></summary>
<p>

```Python 

# TODO




```
</p>
</details>

___

**Circular Linked Lists**

Circular linked lists occur when the chain of nodes links back to itself somewhere. For example `NodeA -> NodeB -> NodeC -NodeD -> NodeB` is a circular list because `NodeD` points back to `NodeB` creating a loop `NodeB -> NodeC -> NodeD -> NodeB`.



A circular linked list is typically consider pathological because when you try to iterate throught it, you'll never find the end. Wer usually want to detect if there is a loop in our linked lists to aviod these problems.


___

### 9. Linked List Practice 

**Linked List Practice**

Implement a linked list class. Your class should be able to:

* Append data to the tail of the list and prepend to the head 
* Search the linked list for a value and return the node 
* Remove a node 
* Pop, which means to return the first node's value and delete the node from the list
* Insert data at some position in the list 
* Return the size (length) of the linked list

___

```Python 
class Node:

   def __init__(self, value):
   self.value = value
   self.next = None

class LinkedList:
   def __init__(self):
      self.head = None
      def prepend(self, value):
        """ Prepend a value to the beginning of the list. """
        
        # TODO: Write function to prepend here
        
        pass
    
    def append(self, value):
        """ Append a value to the end of the list. """
        
        # TODO: Write function to append here
        
        pass
    
    def search(self, value):
        """ Search the linked list for a node with the requested value and return the node. """
        
        # TODO: Write function to search here
        
        pass
    
    def remove(self, value):
        """ Remove first occurrence of value. """
        
        # TODO: Write function to remove here
        
        pass
    
    def pop(self):
        """ Return the first node's value and remove it from the list. """
        
        # TODO: Write function to pop here
        
        pass
    
    def insert(self, value, pos):
        """ Insert value at pos position in the list. If pos is larger than the
            length of the list, append to the end of the list. """
        
        # TODO: Write function to insert here
        
        pass
    
    def size(self):
        """ Return the size or length of the linked list. """
        
        
        # TODO: Write function to get size here
        
        pass
    
    def to_list(self):
        out = []
        node = self.head
        while node:
            out.append(node.value)
            node = node.next
        return out
## Test your implementation here

# Test prepend
linked_list = LinkedList()
linked_list.prepend(1)
assert linked_list.to_list() == [1], f"list contents: {linked_list.to_list()}"
linked_list.append(3)
linked_list.prepend(2)
assert linked_list.to_list() == [2, 1, 3], f"list contents: {linked_list.to_list()}"
    
# Test append
linked_list = LinkedList()
linked_list.append(1)
assert linked_list.to_list() == [1], f"list contents: {linked_list.to_list()}"
linked_list.append(3)
assert linked_list.to_list() == [1, 3], f"list contents: {linked_list.to_list()}"

# Test search
linked_list.prepend(2)
linked_list.prepend(1)
linked_list.append(4)
linked_list.append(3)
assert linked_list.search(1).value == 1, f"list contents: {linked_list.to_list()}"
assert linked_list.search(4).value == 4, f"list contents: {linked_list.to_list()}"

# Test remove
linked_list.remove(1)
assert linked_list.to_list() == [2, 1, 3, 4, 3], f"list contents: {linked_list.to_list()}"
linked_list.remove(3)
assert linked_list.to_list() == [2, 1, 4, 3], f"list contents: {linked_list.to_list()}"
linked_list.remove(3)
assert linked_list.to_list() == [2, 1, 4], f"list contents: {linked_list.to_list()}"

# Test pop
value = linked_list.pop()
assert value == 2, f"list contents: {linked_list.to_list()}"
assert linked_list.head.value == 1, f"list contents: {linked_list.to_list()}"

# Test insert 
linked_list.insert(5, 0)
assert linked_list.to_list() == [5, 1, 4], f"list contents: {linked_list.to_list()}"
linked_list.insert(2, 1)
assert linked_list.to_list() == [5, 2, 1, 4], f"list contents: {linked_list.to_list()}"
linked_list.insert(3, 6)
assert linked_list.to_list() == [5, 2, 1, 4, 3], f"list contents: {linked_list.to_list()}"

# Test size
assert linked_list.size() == 5, f"list contents: {linked_list.to_list()}"

```

___


<details><summary><b>Solution</b></summary>
<p>

```Python 

# Solution

class LinkedList:
    def __init__(self):
        self.head = None

    def prepend(self, value):
        """ Prepend a node to the beginning of the list """

        if self.head is None:
            self.head = Node(value)
            return

        new_head = Node(value)
        new_head.next = self.head
        self.head = new_head

    def append(self, value):
        """ Append a node to the end of the list """
        # Here I'm not keeping track of the tail. It's possible to store the tail
        # as well as the head, which makes appending like this an O(1) operation.
        # Otherwise, it's an O(N) operation as you have to iterate through the
        # entire list to add a new tail.

        if self.head is None:
            self.head = Node(value)
            return

        node = self.head
        while node.next:
            node = node.next

        node.next = Node(value)

    def search(self, value):
        """ Search the linked list for a node with the requested value and return the node. """
        if self.head is None:
            return None

        node = self.head
        while node:
            if node.value == value:
                return node
            node = node.next

        raise ValueError("Value not found in the list.")


    def remove(self, value):
        """ Delete the first node with the desired data. """
        if self.head is None:
            return

        if self.head.value == value:
            self.head = self.head.next
            return

        node = self.head
        while node.next:
            if node.next.value == value:
                node.next = node.next.next
                return
            node = node.next

        raise ValueError("Value not found in the list.")


    def pop(self):
        """ Return the first node's value and remove it from the list. """
        if self.head is None:
            return None

        node = self.head
        self.head = self.head.next

        return node.value

    def insert(self, value, pos):
        """ Insert value at pos position in the list. If pos is larger than the
            length of the list, append to the end of the list. """
        if pos == 0:
            self.prepend(value)
            return

        index = 0
        node = self.head
        while node.next and index <= pos:
            if (pos - 1) == index:
                new_node = Node(value)
                new_node.next = node.next
                node.next = new_node
                return

            index += 1
            node = node.next
        else:
            self.append(value)

    def size(self):
        """ Return the size or length of the linked list. """
        size = 0
        node = self.head
        while node:
            size += 1
            node = node.next

        return size

    def to_list(self):
        out = []
        node = self.head
        while node:
            out.append(node.value)
            node = node.next
        return out





```
</p>
</details>

___

### 10. Reverse a Linked List 

**Reversing a linked list exercise**

Given a singly linked list, return another linked list that is the reverse of the first. 

```Python 
# Helper Code

class Node:
    def __init__(self, value):
        self.value = value
        self.next = None

class LinkedList:
    def __init__(self):
        self.head = None
        
    def append(self, value):
        if self.head is None:
            self.head = Node(value)
            return
        
        node = self.head
        while node.next:
            node = node.next

        node.next = Node(value)
        
    def __iter__(self):
        node = self.head
        while node:
            yield node.value
            node = node.next
            
    def __repr__(self):
        return str([v for v in self])
```

```Python 

def reverse(linked_list):
    """
    Reverse the inputted linked list

    Args:
       linked_list(obj): Linked List to be reversed
    Returns:
       obj: Reveresed Linked List
    """
    
    # TODO: Write your function to reverse linked lists here
    
    pass
```

```Python 

llist = LinkedList()
for value in [4,2,5,1,-3,0]:
    llist.append(value)

flipped = reverse(llist)
is_correct = list(flipped) == list([0,-3,1,5,2,4]) and list(llist) == list(reverse(flipped))
print("Pass" if is_correct else "Fail")

```

___

<details><summary><b>Solution</b></summary>
<p>

```Python 

# Solution

# Solution

class Node:
    def __init__(self, value):
        self.value = value
        self.next = None

class LinkedList:
    def __init__(self):
        self.head = None
        
    def append(self, value):
        if self.head is None:
            self.head = Node(value)
            return
        
        node = self.head
        while node.next:
            node = node.next

        node.next = Node(value)
        
    def __iter__(self):
        node = self.head
        while node:
            yield node.value
            node = node.next
            
    def __repr__(self):
        return str([v for v in self])

# Time complexity O(N)
def reverse(linked_list):
        """
    Reverse the inputted linked list

    Args:
       linked_list(obj): Linked List to be reversed
    Returns:
       obj: Reveresed Linked List
    """
    new_list = LinkedList()
    node = linked_list.head
    prev_node = None

    # A bit of a complex operation here. We want to take the
    # node from the original linked list and prepend it to 
    # the new linked list
    for value in linked_list:
        new_node = Node(value)
        new_node.next = prev_node
        prev_node = new_node
    new_list.head = prev_node
    return new_list

llist = LinkedList()
for value in [4,2,5,1,-3,0]:
    llist.append(value)

flipped = reverse(llist)
is_correct = list(flipped) == list([0,-3,1,5,2,4]) and list(llist) == list(reverse(flipped))
print("Pass" if is_correct else "Fail")
```
</p>
</details>

___


### 11. Loop Detection 

**Detecting Loops in Linked Lists**

Here we'll implement a function that detects if a loop exists in a linked list. The way we'll do this is by having two pointers, called "runners", moving through the list at different rates. Typically we have a "slow" runner which moves at one node per step and a "fast" runner that moves at two nodes per step.

If a loop exists in the list, the fast runner will eventually move behind the slow runner as it moves to the beginning of the loop. Eventually it will catch up to the slow runner and both runners will be pointing to the same node at the same time. If this happens then you know there is a loop in the linked list. Below is an example where we have a slow runner (the green arrow) and a fast runner (the red arrow).





```Python

class Node:
    def __init__(self, value):
        self.value = value
        self.next = None
        
class LinkedList:
    def __init__(self, init_list=None):
        self.head = None
        if init_list:
            for value in init_list:
                self.append(value)
        
    def append(self, value):
        if self.head is None:
            self.head = Node(value)
            return
        
        # Move to the tail (the last node)
        node = self.head
        while node.next:
            node = node.next
        
        node.next = Node(value)
        return
```

```Python

list_with_loop = LinkedList([2, -1, 3, 0, 5])

# Creating a loop where the last node points back to the second node
loop_start = list_with_loop.head.next

node = list_with_loop.head
while node.next: 
    node = node.next   
node.next = loop_start

```

**Exercise:** Given a linked list, implement a function iscircular that returns True if a loop exists in the list and False otherwise.

```Python 
def iscircular(linked_list):
    """
    Determine wether the Linked List is circular or not

    Args:
       linked_list(obj): Linked List to be checked
    Returns:
       bool: Return True if the linked list is circular, return False otherwise
    """
    
    # TODO: Write function to check if linked list is circular
    
    pass
```

```Python 

# Test Cases

small_loop = LinkedList([0])
small_loop.head.next = small_loop.head
print ("Pass" if iscircular(list_with_loop) else "Fail")
print ("Pass" if not iscircular(LinkedList([-4, 7, 2, 5, -1])) else "Fail")
print ("Pass" if not iscircular(LinkedList([1])) else "Fail")
print ("Pass" if iscircular(small_loop) else "Fail")
print ("Pass" if not iscircular(LinkedList([])) else "Fail")

```

___

<details><summary><b>Solution</b></summary>
<p>

```Python 

# Soultion

# Solution

def iscircular(linked_list):
    """
    Determine wether the Linked List is circular or not

    Args:
       linked_list(obj): Linked List to be checked
    Returns:
       bool: Return True if the linked list is circular, return False otherwise
    """

    if linked_list.head is None:
        return False
    
    slow = linked_list.head
    fast = linked_list.head
    
    while fast and fast.next:
        # slow pointer moves one node
        slow = slow.next
        # fast pointer moves two nodes
        fast = fast.next.next
        
        if slow == fast:
            return True
    
    # If we get to a node where fast doesn't have a next node or doesn't exist itself, 
    # the list has an end and isn't circular
    return False

small_loop = LinkedList([0])
small_loop.head.next = small_loop.head
print ("Pass" if iscircular(list_with_loop) else "Fail")
print ("Pass" if not iscircular(LinkedList([-4, 7, 2, 5, -1])) else "Fail")
print ("Pass" if not iscircular(LinkedList([1])) else "Fail")
print ("Pass" if iscircular(small_loop) else "Fail")
print ("Pass" if not iscircular(LinkedList([])) else "Fail")
```
</p>
</details>
 

 ___


### 12. Flatten a Nested Linked List 

**Falttening a nested linked list**

Suppose you have a linked list where the value of each node is a sorted linked list (i.e., it is a nested list). Your task is to flatten this nested list—that is, to combine all nested lists into a single (sorted) linked list.

First, we'll need some code for generating nodes and a linked list:

```Python 
# Use this class as the nodes in your linked list
class Node:
    def __init__(self, value):
        self.value = value
        self.next = None
    
    def __repr__(self):
        return str(self.value)
    
class LinkedList:
    def __init__(self, head):
        self.head = head
        
    def append(self, value):
        if self.head is None:
            self.head = Node(value)
            return
        node = self.head
        while node.next is not None:
            node = node.next
        node.next = Node(value)
```

Now, in the cell below, see if you can solve the problem by implementing the flatten method.

>Hint: If you first create a merge method that merges two linked lists into a sorted linked list, then there is an elegant recursive solution.

```Python 
def merge(list1, list2):
    # TODO: Implement this function so that it merges the two linked lists in a single, sorted linked list.
    pass

class NestedLinkedList(LinkedList):
    def flatten(self):
        # TODO: Implement this method to flatten the linked list in ascending sorted order.
        pass
```

Here's some code that will generate a nested linked list that we can use to test the solution:

```Python
# First Test scenario
linked_list = LinkedList(Node(1))
linked_list.append(Node(3))
linked_list.append(Node(5))

nested_linked_list = NestedLinkedList(Node(linked_list))

second_linked_list = LinkedList(Node(2))
second_linked_list.append(4)

nested_linked_list.append(Node(second_linked_list))
```

___


**Stucture**

`nested_linked_list` should now have 2 nodes. The head node is a linked list containing `1, 3, 5`. The second node is a linked list containing `2, 4`.
Calling `flatten` should return a linked list containing `1, 2, 3, 4, 5`.

```Python 
solution = nested_linked_list.flatten()
assert solution == [1,2,3,4,5]
```

**Solution**

First, let's implement a `merge` function that takes in two linked lists and returns one sorted linked list. Note, this implementation expects both linked lists to be sorted.

```Python
def merge(list1, list2):
    merged = LinkedList(None)
    if list1 is None:
        return list2
    if list2 is None:
        return list1
    list1_elt = list1.head
    list2_elt = list2.head
    while list1_elt is not None or list2_elt is not None:
        if list1_elt is None:
            merged.append(list2_elt)
            list2_elt = list2_elt.next
        elif list2_elt is None:
            merged.append(list1_elt)
            list1_elt = list1_elt.next
        elif list1_elt.value <= list2_elt.value:
            merged.append(list1_elt)
            list1_elt = list1_elt.next
        else:
            merged.append(list2_elt)
            list2_elt = list2_elt.next
    return merged
```

 Let's make sure merge works how we expect:

```Python
 linked_list = LinkedList(Node(1))
linked_list.append(3)
linked_list.append(5)

second_linked_list = LinkedList(Node(2))
second_linked_list.append(4)

merged = merge(linked_list, second_linked_list)
node = merged.head
while node is not None:
    #This will print 1 2 3 4 5
    print(node.value)
    node = node.next
    
# Lets make sure it works with a None list
merged = merge(None, linked_list)
node = merged.head
while node is not None:
    #This will print 1 2 3 4 5
    print(node.value)
    node = node.next
```

Now let's implement `flatten` recursively using merge.

```Python
class NestedLinkedList(LinkedList):
    def flatten(self):
        return self._flatten(self.head)

    def _flatten(self, node):
        if node.next is None:
            return merge(node.value, None)
        return merge(node.value, self._flatten(node.next))
```

```Python
nested_linked_list = NestedLinkedList(Node(linked_list))
nested_linked_list.append(second_linked_list)
flattened = nested_linked_list.flatten()

node = flattened.head
while node is not None:
    #This will print 1 2 3 4 5
    print(node.value)
    node = node.next
```

___


**Computational Complexity**

Lets start with the computational complexity of `merge`. Merge takes in two lists. Let's say the lengths of the lists are  `𝑁1` and  `𝑁2`

Because we assume the inputs are sorted, `merge` is very efficient. It looks at the first element of each list and adds the smaller one to the returned list. Every time through the loop we are appending one element to the list, so it will take  `𝑁1+𝑁2`iterations until we have the whole list.

The complexity of flatten is a little more complicated to calculate. Suppose our `NestedLinkedList` has  `𝑁` linked lists and each list's length is represented by  `𝑀1,𝑀2,...,𝑀𝑁`

We can represent this recursion as:

`𝑚𝑒𝑟𝑔𝑒(𝑀1,𝑚𝑒𝑟𝑔𝑒(𝑀2,𝑚𝑒𝑟𝑔𝑒(...,𝑚𝑒𝑟𝑔𝑒(𝑀𝑁−1,𝑚𝑒𝑟𝑔𝑒(𝑀𝑁,𝑁𝑜𝑛𝑒)))))`

 
Let's start from the inside. The inner most merge returns the  `𝑛𝑡ℎ` linked list. The next merge does  `𝑀𝑁−1+𝑀𝑁` comparisons. The next merge does  `𝑀𝑁−2+𝑀𝑁−1+𝑀𝑁` comparisons.
Eventually we will do  `𝑁` comparisons on all of the  `𝑀𝑁` elements. We will do  `𝑁−1` comparisons on  `𝑀𝑁−1` elements.

This can be generalized as:
`∑𝑛𝑁𝑛∗𝑀𝑛`

 ___

### 13. Add One


**Problem Statement** 

Given a non-negative number in the form of list elements. For example, the number `123` would be provided as `arr = [1, 2, 3]`. Add one to the number and return the output in the form of a new list. 

**Example 1:**

* `input = [1, 2, 3]`
* `output = [1, 2,4]`

**Example 2:**

* `input = [9, 9, 9]`
* `output = [1,0,0,0]`

**Challenge:**

One way to solve this problem is to convert the input array into a number and then add one to it. For example, if we have `input = [1, 2, 3]`, you could solve this problem by creating the number `123` and then seperating the digits of the output number `124`. 

But can it be solved some other way?

```Python 
def add_one(arr):
	"""
	:param: arr - list of digits representing some number x 
	return a list with digits representing (x + 1)
	"""

	pass
```

<details><summary><b>Solution</b></summary>
<p>

```Python 
# Solution
def add_one(arr):
    output = 1;

    for i in range(len(arr), 0, -1):
        output = output + arr[i - 1]
        borrow = output//10
        if borrow == 0:
            arr[i - 1] = output
            break
        else:
            arr[i - 1] = output % 10
            output = borrow
    arr = [borrow] + arr
    index = 0
    while arr[index]==0:
        index += 1
    return arr[index:]

```
</p>
</details>

___


```Python
def test_function(test_case):
    arr = test_case[0]
    solution = test_case[1]
    
    output = add_one(arr)
    for index, element in enumerate(output):
        if element != solution[index]:
            print("Fail")
            return
    print("Pass")     
```
```Python
arr = [0]
solution = [1]
test_case = [arr, solution]
test_function(test_case)
```
Pass

```Python
arr = [1, 2, 3]
solution = [1, 2, 4]
test_case = [arr, solution]
test_function(test_case)
```
Pass

```Python
arr = [9, 9, 9]
solution = [1, 0, 0, 0]
test_case = [arr, solution]
test_function(test_case)
```

Pass


___

### 14. Duplicate Number


**Problem Statement**

Given an array of `length = n`. The array contains integers from `0` to `n-2`. Each number in the array is present exactly once except for one number which is present twice. Find and return this duplicate number in the array. 

**Example:** 

* `arr = [0, 2, 3, 1, 4, 5, 3]`
* `output = 3` (because `3` is present twice)

This expected time complexity for this problem is `O(n)` and the expected space-complexity is O(1).

```Python 
def duplicate_number(arr):
	"""

	:param - array containing numbers in the range [0, len(arr) -2]
	return - the number that is duplicate in the arr
	"""

	pass
```

<details><summary><b>Solution</b></summary>
<p>

```Python 
# Solution
def duplicate_number(arr):
    current_sum = 0
    expected_sum = 0
    
    for num in arr:
        current_sum += num
        
    for i in range(len(arr) - 1):
        expected_sum += i
    return current_sum - expected_sum
```
</p>
</details>

___

```Python
def test_function(test_case):
	arr = test_case[0]
	solution = test_case[1]
	output = duplicate_number(arr)
	if output == solution:
		print("Pass")
	else:
		print("Fail")
```

```Python 
arr = [0, 0]
solution = 0

test_case = [arr, solution]
test_function(test_case)
```
Pass

```Python 
arr = [0, 2, 3, 1, 4, 5, 3]
solution = 3

test_case = [arr, solution]
test_function(test_case)
```
Pass

```Python
arr = [0, 1, 5, 4, 3, 2, 0]
solution = 0

test_case = [arr, solution]
test_function(test_case)
```

Pass

```Python
arr = [0, 1, 5, 5, 3, 2, 4]
solution = 5

test_case = [arr, solution]
test_function(test_case)
```
Pass

___

### 15. Max Sum Subarray

**Problem Statement**

Given an array containing numbers. Find and return the largest sum in a contiguous subarray within the input array. 

**Example 1:**

* `arr= [1, 2, 3, -4, 6]`
* The largest sum is `8`, which is the sum of all elements of the array. 

**Example 2:**

* `arr = [1, 2, -5, -4, 1, 6]`
* The largest sum is `7`, which is the sum of the last two elements of the array. 

```Python

def max_sum_subarray(arr):
    """
    :param - arr - input array
    return - number - largest sum in contiguous subarry within arr
    """
    pass
```

<details><summary><b>Solution</b></summary>
<p>

```Python 
# Solution

def max_sum_subarray(arr):
    max_sum = arr[0]
    current_sum = arr[0]

    for num in arr[1:]:
        current_sum = max(current_sum + num, num)
        max_sum = max(current_sum, max_sum)
    return max_sum
```
</p>
</details>

___


```Python
def test_function(test_case):
    arr = test_case[0]
    solution = test_case[1]
    
    output = max_sum_subarray(arr)
    if output == solution:
        print("Pass")
    else:
        print("Fail")
```
```Python
arr= [1, 2, 3, -4, 6]
solution= 8 # sum of array

test_case = [arr, solution]
test_function(test_case)
```

Pass

```Python
arr = [1, 2, -5, -4, 1, 6]
solution = 7   # sum of last two elements

test_case = [arr, solution]
test_function(test_case)
```
Pass

```Python
arr = [-12, 15, -13, 14, -1, 2, 1, -5, 4]
solution = 18  # sum of subarray = [15, -13, 14, -1, 2, 1]

test_case = [arr, solution]
test_function(test_case)
```

Pass

___

### 16. Pascal's Triangle 

**Problem Statement**

Find and return the `nth` row of Pascal's triangle in the form of a list. `n` is 0-based. 

For example, if `n = 4`, then the `output = [1, 4, 6, 1]`. 

[To learn more about Pascal's triangle:](https://wwww.mathisfun.com/pascals-triangle.html)

```Python
def nth_row_pascal(n):
    """
    :param: - n - index (0 based)
    return - list() representing nth row of Pascal's triangle
    """
```

<details><summary><b>Solution</b></summary>
<p>

```Python 
# Solution

def nth_row_pascal(n):
    if n == 0:
        return [1]
    current_row = [1]
    for i in range(1, n + 1):
        previous_row = current_row
        current_row = [1]
        for j in range(1, i):
            next_number = previous_row[j] + previous_row[j - 1]
            current_row.append(next_number)
        current_row.append(1)
    return current_row
```
</p>
</details>

___

```Python 
def test_function(test_case):
    n = test_case[0]
    solution = test_case[1]
    output = nth_row_pascal(n)
    if solution == output:
        print("Pass")
    else:
        print("Fail")
```

```Python
n = 0
solution = [1]

test_case = [n, solution]
test_function(test_case)
```

Pass

```Python
n = 1
solution = [1, 1]

test_case = [n, solution]
test_function(test_case)
```

Pass

```Python
n = 2
solution = [1, 2, 1]

test_case = [n, solution]
test_function(test_case)
```

Pass

```Python
n = 3
solution = [1, 3, 3, 1]

test_case = [n, solution]
test_function(test_case)
```

Pass

```Python
n = 4
solution = [1, 4, 6, 4, 1]

test_case = [n, solution]
test_function(test_case)
```

___

### 17. Even after odd

**Problem Statement**

Give a linked list with integer data, arrange the elements in such a manner that all nodes with even numbers are placed after odd numbers. **Do not create any new nodes and avoid using any other data structure. The relative order of even and odd elements must not change.**

**Example:**

* `linked list = 1 2 3 4 5 6`
* `output = 1 3 5 2 4 6`

```Python
class Node:
	def __init__(self, data):
		self.data = data
		self.next = None
```

```Python 
def even_after_odd(head)
   """

   :param - head - head of linked list
   return - updated list with all even elements are odd elements
   """

   pass
```
<details><summary><b>Solution</b></summary>
<p>

```Python 
# Solution
def even_after_odd(head):
    
    if head is None:
        return head
    
    even = None
    odd = None
    even_tail = None
    head_tail = None
    
    while head:
        next_node = head.next
        
        if head.data % 2 == 0:
            if even is None:
                even = head
                even_tail = even
            else:
                even_tail.next = head
                even_tail = even_tail.next
        else:
            if odd is None:
                odd = head
                odd_tail = odd
            else:
                odd_tail.next = head
                odd_tail = odd_tail.next
        head.next = None
        head = next_node
    
    if odd is None:
        return even
    odd_tail.next = even
    return odd
```
</p>
</details>

___

```Python
# helper functions for testing purpose
def create_linked_list(arr):
    if len(arr)==0:
        return None
    head = Node(arr[0])
    tail = head
    for data in arr[1:]:
        tail.next = Node(data)
        tail = tail.next
    return head

def print_linked_list(head):
    while head:
        print(head.data, end=' ')
        head = head.next
    print()
```

```Python

def test_function(test_case):
    head = test_case[0]
    solution = test_case[1]
    
    node_tracker = dict({})
    node_tracker['nodes'] = list()
    temp = head
    while temp:
        node_tracker['nodes'].append(temp)
        temp = temp.next

    head = even_after_odd(head)    
    temp = head
    index = 0
    try:
        while temp:
            if temp.data != solution[index] or temp not in node_tracker['nodes']:
                print("Fail")
                return
            temp = temp.next
            index += 1
        print("Pass")            
    except Exception as e:
        print("Fail")
```

```Python
arr = [1, 2, 3, 4, 5, 6]
solution = [1, 3, 5, 2, 4, 6]

head = create_linked_list(arr)
test_case = [head, solution]
test_function(test_case)
```
Pass

```Python
arr = [1, 3, 5, 7]
solution = [1, 3, 5, 7]

head = create_linked_list(arr)
test_case = [head, solution]
test_function(test_case)
```
Pass

```Python
arr = [2, 4, 6, 8]
solution = [2, 4, 6, 8]
head = create_linked_list(arr)
test_case = [head, solution]
test_function(test_case)
```
Pass

___

### 18. Skip i, j

**Problem Statement**

Given the head of a linked list and two integers, `i` and `j`. You have to retain the first `i` nodes and then delete the next `j` nodes. Continue doing so unitl the end of the linked list. 

**Example:**

* `linked-list = 1 2 3 4 5 6 7 8 9 10 11 12`
* `i = 2`
* `j = 3` 
* `output = 1 2 6 7 11 12`

```Python 
# LinkedList Node class for your reference
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None
```

```Python
def skip_i_delete_j(head, i, j):
    """
    :param: head - head of linked list
    :param: i - first `i` nodes that are to be skipped
    :param: j - next `j` nodes that are to be deleted
    return - return the updated head of the linked list
    """
    pass
```
<details><summary><b>Solution</b></summary>
<p>

```Python 
# Solution
def skip_i_delete_j(head, i, j):
    if i == 0:
        return None
    
    if head is None or j < 0 or i < 0:
        return head
    
    current = head
    previous = None
    while current:
        # skip (i - 1) nodes
        for _ in range(i - 1):
            if current is None:
                return head
            current = current.next
        previous = current
        current = current.next
        
        # delete next j nodes
        for _ in range(j):
            if current is None:
                break
            next_node = current.next
            current = next_node
        previous.next = current
    return head
```
</p>
</details>

___

```Python
# helper functions for testing purpose
def create_linked_list(arr):
    if len(arr)==0:
        return None
    head = Node(arr[0])
    tail = head
    for data in arr[1:]:
        tail.next = Node(data)
        tail = tail.next
    return head

def print_linked_list(head):
    while head:
        print(head.data, end=' ')
        head = head.next
    print()
```

```Python
def test_function(test_case):
    head = test_case[0]
    i = test_case[1]
    j = test_case[2]
    solution = test_case[3]
        
    temp = skip_i_delete_j(head, i, j)
    index = 0
    try:
        while temp is not None:
            if temp.data != solution[index]:
                print("Fail")
                return
            index += 1
            temp = temp.next
        print("Pass")
    except Exception as e:
        print("Fail")
```

```Python
arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12]
i = 2
j = 2
head = create_linked_list(arr)
solution = [1, 2, 5, 6, 9, 10]
test_case = [head, i, j, solution]
test_function(test_case)
```
Pass 

```Python 
arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12]
i = 2
j = 3
head = create_linked_list(arr)
solution = [1, 2, 6, 7, 11, 12]
test_case = [head, i, j, solution]
test_function(test_case)
```
Pass

```Python 
arr = [1, 2, 3, 4, 5]
i = 2
j = 4
head = create_linked_list(arr)
solution = [1, 2]
test_case = [head, i, j, solution]
test_function(test_case)
```
Pass

___


### 19. Swap Nodes

**Problem Statement**

Given a linked list, swap the two nodes present at position `i` and `j`. The positions are based on 0-based indexing. 

**Note:** You have to swap the nodes and not just the values.

**Example:** 

* `linked_list = 3 4 5 2 6 1 9`
* `positions = 3 4`
* `output = 3 4 5 6 2 1 9`

**Explanation:** 

* The node at position 3 has the value `2`
* The node at position 4 has the value of `6`
* Swapping these nodes will result in a final order of nodes `3 4 5 6 2 1 9`

```Python 
class Node:
    """LinkedListNode class to be used for this problem"""
    def __init__(self, data):
        self.data = data
        self.next = None
```

```Python 
def swap_nodes(head, left_index, right_index):
    """
    :param: head- head of input linked list
    :param: left_index - indicates position
    :param: right_index - indicates position
    return: head of updated linked list with nodes swapped
    TODO: complete this function and swap nodes present at left_index and right_index
    Do not create a new linked list
    """
    pass
```
<details><summary><b>Solution</b></summary>
<p>
	
```Python 
# Solution

def swap_nodes(head, left_index, right_index):

    # if both the indices are same
    if left_index == right_index:
        return head
    
    
    left_previous = None
    left_current = None

    right_previous = None
    right_current = None

    count = 0
    temp = head
    new_head = None

    # find out previous and current node at both the indices
    while temp is not None:
        if count == left_index:
            left_current = temp
        elif count == right_index:
            right_current = temp
            break

        if left_current is None:
            left_previous = temp
        right_previous = temp
        temp = temp.next
        count += 1

    right_previous.next = left_current
    temp = left_current.next
    left_current.next = right_current.next

    # if both the indices are next to each other
    if left_index != right_index:
        right_current.next = temp

    # if the node at first index is head of the original linked list
    if left_previous is None:
        new_head = right_current
    else:
        left_previous.next = right_current
        new_head = head

    return new_head
```
</p>
</details>

___


```Python 
def test_function(test_case):
    head = test_case[0]
    left_index = test_case[1]
    right_index = test_case[2]
    
    left_node = None
    right_node = None
    
    temp = head
    index = 0
    try:
        while temp is not None:
            if index == left_index:
                left_node = temp
            if index == right_index:
                right_node = temp
                break
            index += 1
            temp = temp.next

        updated_head = swap_nodes(head, left_index, right_index)

        temp = updated_head
        index = 0
        pass_status = [False, False]

        while temp is not None:
            if index == left_index:
                pass_status[0] = temp is right_node
            if index == right_index:
                pass_status[1] = temp is left_node

            index += 1
            temp = temp.next

        if pass_status[0] and pass_status[1]:
            print("Pass")
        else:
            print("Fail")
        return updated_head
    except Exception as e:
        print("Fail")
```

```Python 
# helper functions for testing purpose
def create_linked_list(arr):
    if len(arr)==0:
        return None
    head = Node(arr[0])
    tail = head
    for data in arr[1:]:
        tail.next = Node(data)
        tail = tail.next
    return head

def print_linked_list(head):
    while head:
        print(head.data, end=" ")
        head = head.next
    print()
```

```Python 
arr = [3, 4, 5, 2, 6, 1, 9]
head = create_linked_list(arr)
left_index = 3
right_index = 4

test_case = [head, left_index, right_index]
updated_head = test_function(test_case)
```
Pass

```Python 
arr = [3, 4, 5, 2, 6, 1, 9]
left_index = 2 
right_index = 4
head = create_linked_list(arr)
test_case = [head, left_index, right_index]
updated_head = test_function(test_case)
```
Pass

```Python 
arr = [3, 4, 5, 2, 6, 1, 9]
left_index = 0
right_index = 1
head = create_linked_list(arr)
test_case = [head, left_index, right_index]
updated_head = test_function(test_case)
```

Pass

___




