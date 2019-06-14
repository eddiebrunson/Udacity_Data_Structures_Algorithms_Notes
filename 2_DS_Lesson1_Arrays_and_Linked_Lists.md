# 2. Data Structures

## Lesson 1: Arrays and Linked Lists

**Why data structures?**

1. Lists 

*Data Structures* are containers that organize and group data together in different ways. When you write code to solve a problem, there will always be data involved--and how you store or structure that data in the computer's memory can have a huge impact on what kinds of things you can do with it and how efficiently you can do those things. 

**Properties of collections**

* Don't have a particular order (so you can't say "give me the 3rd element in this collection")
* Don't have to have objects of the same type

There are many data structures that add rules to collections to be used in programming. 

___

2. Lists

Have all of the properties of a collection. It havs a group of things but the objects have order. 

A shopping list has a lot of the same properties as the lists.

Different programming languages treat lists differently. 

**Properties of lists**

* Have an **order** (so you can say things like "give me the 3rd item in the list")

* Have **no fixed** length (you can add or remove elements)

___

3. Arrays

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

4. Strings Exercises

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

**Anagrams**


