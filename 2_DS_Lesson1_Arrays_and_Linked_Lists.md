# 2. Data Structures

## Lesson 1: Arrays and Linked Lists

**Why data structures?**

#### 1. Lists 

*Data Structures* are containers that organize and group data together in different ways. When you write code to solve a problem, there will always be data involved--and how you store or structure that data in the computer's memory can have a huge impact on what kinds of things you can do with it and how efficiently you can do those things. 

**Properties of collections**

* Don't have a particular order (so you can't say "give me the 3rd element in this collection")
* Don't have to have objects of the same type

There are many data structures that add rules to collections to be used in programming. 

___

#### 2. Lists

Have all of the properties of a collection. It havs a group of things but the objects have order. 

A shopping list has a lot of the same properties as the lists.

Different programming languages treat lists differently. 

**Properties of lists**

* Have an **order** (so you can say things like "give me the 3rd item in the list")

* Have **no fixed** length (you can add or remove elements)

___

#### 3. Arrays

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

#### 4. Strings Exercises

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

#### 5. Linked Lists Introduction

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

#### 6. Linked Lists Continued 

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


#### Implement a Linked List 

Practice implementing a basic linked list:

  2 --> 1 --> 4 --> 3 --> 5 --> None 

Head

___

**Key characteristics**

Let's review the overall abstract concepts for this data structure. 



#### 8. Types of Linked Lists

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



 