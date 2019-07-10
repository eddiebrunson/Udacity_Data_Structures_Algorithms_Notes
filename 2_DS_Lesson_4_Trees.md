# 2. Data Structures

## Lesson 4: Trees

___

Trees start at the root and you add data to it through branches. 

Trees are really an extension of a linked list. 

___

### 2. Tree Basics

Trees are really just an extension of a linked list. The first element is called the root, and instead of having one element a tree can have several. 

Linked-list is often drawn horizontally, but a tree is normally drawn vertically. 

Just like a linked- list, each element on a tree contains some data. The individual elements in a tree that contain values are often called nodes. 

A tree must be completely connected. If you are starting form the root there must be some way to reach every node in the tree. 

There must not be any cycles in the tree. Cycles occur when there's a way for you to encounter the same node twice or connection back to the root. 

> ignore the arrows and you can still get back to the main node, that's not a tree as well. 





### 3. Tree Terminology 

* Levels- How many connections it takes to reach the root plus 1. 

* Root- is level 1, and nodes directly connected to it are on level 2. 

Nodes in a tree are often decribed as having a parent-child relationship. 

Children are only allowed to have one parent. If a parent has multiple children, those children are consided siblings of each other. 

A node a a lower level could be considered the ancestor, and the nodes at the higher level could be considered as the descendants. 


Nodes at the ned that don't have any children are called **leaves**, or **external nodes**. 

While, a **parent node** is called an **internal node**. 

Connections can be called **edges**, and a group of connections taken together as an **path**

The **Height** of an node is the number of edges between it and the furthest leaf on the tree. 

A leaf has a height of zero, but the parent of a leaf has a height of one. 

The height of a tree overall is just the height of the root node. 

On the flip side, the depth of a node is the number of edges to the root. 

Height and depth should move inversely. 

If a node is closer to a leaf then it's further from the root. 


___

### 4. Tree Traversal

In linked list traversal- we just needed ot make sure we looked at every element. Trees aren't linear, so there's no clear way to traverse through everything. 

There are two different broad approachers to treat traversal:

* DFS- depth-first search, where if there are children nodes to explore, exploring them is the priority. 

* BFS- breadth-first search, the priority is visiting every node on the same level wer're currently on before visiting child nodes. 

For Trees a level order traversal is a **BFS** with a more exact algorithm to implement. 
                        
                        **BFS Level Order Traversal**
                                   D
                                  / \
                                 B   E
                                / \   \
                               A   C   F
                            D, B, E, A, C, F 


A level order traveral is exactly what it sounds like. Start at the root then visit it's children on the second level then all of their children on the third level until you've visited every single leaf. 

By convention, we start on the left most side of the level and move right. 

___

### 5. Depth-First Traversals 

There are several different approaches to DFS and trees. 

1. First there is **Pre-Order** traversals, check off a node as you see it before you traverse any furthere in the tree.

```
                        **Pre-Order Traversal**
                                   D
                                  / \
                                 B   E
                                / \   \
                               A   C   F

                            D, B, A, C, E F
```
Check the root node, then by convention go down the next node on the left and continue traversing down the left most nodes until we hit a leaf. 

Then we check off the leaf and from there go back up to the parent. Then traverse to the right child and check it off too. 

Next, go back up to the the next child and do the exact same steps until we have seen everything. 

2. **In-Order** traversal- means moving through the nodes in the same order, only check off a node when we seen it's left child and come back to it. 

```
                         **In-Order Traversal**
                                   D
                                  / \ 
                                 B   E
                                / \   \
                               A   C   F
                            A, B, C, D, E, F
```

Start at the root and go down the left child until we hit a leaf, we check off the leaf and move up to the parent. We can check off the left parent since we have seen it now. Then move on to the right node, which has no children, so we can check it off too. Go back up to the root and repeat all of this on the right side until we are done. 

3. Lastly, we have the **post-order** traversal. We won't be able to to check off a node unitl we've seen all of it's descendants or we visited both of it's children and returned. 

Simliar steps, we begin at the root, don't check it off, but continue down to a leaf. We check off the leaf and move to the parent. This time we don't check off the parent though, we just move on to the right node. Once we check off the right node we can go back up to the parent and finally check it off too. 

Again, we'll skip over the root node and just move all the way down to the right. 

                          **Post-Order Traversal**
                                     D
                                   /  \
                                 B     E
                                / \     \
                               A   C     F
                           
                            A, C, B, F, E, D


___

### 6. Search and Delete

Binary trees, are trees where parents have at most two children. 

This means nodes can have 0, 1, or 2 children. The children might even be null, but that's okay. 

___

*Search* in a Binary Tree- We can start off by using any of the traversal algorithms to go through the tree. Because there is no real order to the elements, you have to go through every single element in the tree if the value I'm looking for doesn't exist. 

This is a linear time search. 

A *delete* operation often starts out with a search since you need to find the node you want to delete. If you are deleting a leaf, you can simply delete it and move on. 

If you delete an internal node, you'll suddenly have a gap in the tree. If the node you deleted only has one child, you can actually just take it out, move the child up and attach it to the old node's parent. 

If you are trying to get rid of a node that has two children, you have a few options. 

You could promote the child up just like before. 

--> What if both children also have two children?

In the worst case you will need to keep traversing down the sub tree until you hit a leaf. Since there is no real order requirement here, you can just put the leaf where your deleted node was without a problem. 

Since there is a search involved and some additional work to shift around the elements after deletion, *the run time is linear*. 

___

### 7. Insert

Inserting an element into our tree whenit has no order is relatively easy. You just tuck our node onto another node. 

Maybe it's a leaf or maybe it's a parent with only one child. 

We only need to make sure that we're obeying the two children rule. 

We are given the root at the beginning and we will need to keep moving down the tree until we find a open spot. 

-->How long will it take to find an open spot?

The *worst case* is that we travel down the longest path until we find the farthest leaf. 

In that case, we travel through the number of nodes equal to the height of the tree. 

--> But, what is the height of a binary tree?

Like we did with the sorting algorithms, let's look at some examples and reason through it. 

Here are two different trees:

         O                       O 
        / \                    /   \
       O   O                  O     O
                             / \   / \
                            O   O  O  O
* 3 Nodes                  * 7 Nodes 
* 2 Levels                 * 3 levels

These are called **Perfect trees** since every node except the leafs on the last level has two children. 

As the tree grows bigger, each new level has the capacity to hold a number of nodes equivalent to a power of two
```
Level 1     2^0
Level 2     2^1
Level 3     2^3
```

Each node can have two children, so each new level can have twice as many nodes as the one before it. 

Since we have gone back to talking about powers of two, our minds should jump back to log(n). 

--> Does log(n) apply here?

At every level we are adding roughly twice as many elements.

Everytime we need to add a new level or in a binary search divider array an other term, its bc we're giving ourselves the space to allow for about twice as many elements. 

n=3

```

new row...

n + (n + 1)

y
2n + 1 = 7 

elements
```

Remember that we're adding a power of two at each level, so when we count up the nodes overall, it won't be exactly a power of two. 

```
3 levels                                      log(1)=0
                                              log(2)=1
   |                                          log(4)=2 
   V                                          log(8)=3
7 nodes

log(7)=/(not exactly sign)3


```
Having three levels doesn't mean an overall node count of eight, but it does mean that the fourth level itself will have eight elements in it. 

---

### 9. Binary Search Tree

Ordering of elements are different amount different types of trees.

There is a specific type of binary tree called a **binary search tree(BST)**

Every parent node has at most two children. 

BSTs are sorted so every valu on the left of a particular node is smaller than it and every value on the right of a particular node is larger than it. 

Because BSTs have this structure, we can do operations like search, insert, and delete pretty quickly. 

The run time of a search on a BST is just the height of the tree, which we proved was log(n) when we learned about inserting. 

Inserting in a binary tree is pretty much the same process. 

You start at the top and you can make quick decisions about where to look at.


___

### 10. BST Complications

                            Unbalanced BST
                                 5
                                  \ 
                                   10
                                     \
                                      15
                                        \
                                         20


If everything on the right is bigger and no children then we call it an **unbalanced binary tree**, since the distribution of nodes is skewed to the right side. 

Which could also look like a worst case scenario for a BST. 

When a tree looks like this search, insert, and delete all actually take linear time in the worst case. 

The average case for these operations is Big O of log n, and the worst case for all of them is Big O of n. 

___

### 11. Practice overview

Tree data Structures show up a lot in real life and specifically used in software engineering. 

Trees 

* Faster to retrieve data

* Trees how up in Tree-based machine learning models (decision trees)



**Coding Practice Objectives**

* Create a binaray tree

* Traverse a tree
   * Depth first 
   * Breadth first

* Binary Search Tree
   * Insert 
   * Search
   * Delete

* Average Time Complexity 
   * Tree --> log(n)

> An easy way to remember the average time complexity of trees is to remember **"TREES HAVE LOGS"** thus log(n)

___

### 12. Code: Create a Binary Tree

**Task 01: build a node**

on a piece of paper, draw a tree.

* Define a node, what are the three things you'd expect in a node?
* Define class called Node, and define a constructor that takes no arguments, and sets the three instance variables to None.
* Note: coding from a blank cell (or blank piece of paper) is good practice for interviews!

```Python 
## Define a node

node0 = Node()
print(f"""
value: {node0.value}
left: {node0.left}
right: {node0.right}
""")
```
value: None
left: None
right None

___

**Task 02: add a constructor that takes the value as a parameter** 

Copy what you just made, and modify the constructor so that it takes in an optional value, which it assigns as the node's value. Otherwise, it sets the node's value to None.

```Python
## Check

node0 = Node()
print(f"""
value: {node0.value}
left: {node0.left}
right: {node0.right}
""")

node0 = Node("apple")
print(f"""
value: {node0.value}
left: {node0.left}
right: {node0.right}
""")
```
value: None 
Left: None
right: None

value: apple
left: None
right: None

___

**Task 03: add functions to set and get the value of the node**

Add functions `get_value` and `set_value`

```
# add set_value and get_value functions
```

___

**Task 04: add functions that assign a left child, or right child**

Define a function `set_left_child` and a function `set_right_child`. Each function takes in a node that it assigns as the left or right child, respectively. Note that we can assume that this will replace any existing node if it's already assigned as a left or right child.

Also, define `get_left_child` and `get_right_child` functions.

```Python
## check

node0 = Node("apple")
node1 = Node("banana")
node2 = Node("orange")
node0.set_left_child(node1)
node0.set_right_child(node2)

print(f"""
node 0: {node0.value}
node 0 left child: {node0.left.value}
node 0 right child: {node0.right.value}
""")
```

node 0: apple
node 0 left child: banana 
node 0 right child: orange 

___

**Task 05: check if left or right child exists**

Define functions `has_left_child`, `has_right_child`, so that they return true if the node has left child, or right child respectively.

```Python
## check

node0 = Node("apple")
node1 = Node("banana")
node2 = Node("orange")

print(f"has left child? {node0.has_left_child()}")
print(f"has right child? {node0.has_right_child()}")

print("adding left and right children")
node0.set_left_child(node1)
node0.set_right_child(node2)

print(f"has left child? {node0.has_left_child()}")
print(f"has right child? {node0.has_right_child()}")
```

has left child? False
has right child? False
adding left and right children
has left child? True
has right child? True

___

**Task 06: Create a binary tree**

Create a class called `Tree` that has a "root" instance variable of type `Node`.

Also define a `get_root` method that returns the root node.

```Python 
# define a Tree class here
```

___

**Task 07: setting root node in constructor**

Let's modify the `Tree` constructor so that it takes an input that initializes the root node. Choose between one of two options: 1) the constructor takes a `Node` object
2) the constructor takes a value, then creates a new `Node` object using that value.

Which do you think is better?

```Python
# choose option 1 or 2 (you can try both), and explain why you made this choice
```

<details><summary><b>Solution</b></summary>
<p>

```Python 
class Tree(object):
   def __init__(self, node):
      self.root = node 
   def get_root(self):
     return self.root
```
Recommended writing it the second way:

```Python
class Tree(object):
   def __init__(self, vlaue):
      self.root  = node 

   def get_root(self):
      return self.root
```
</p>
</details>

___

### 13. Code: DFS

**Depth First Search Intro**

> **Traversing a Tree** -means we are walking through it in some way so that we are visiting all the nodes once. 

* Traversing is used for searching, inserting, and deleting nodes. 

Two types:

* Depth First Search (DFS) 
* Breadth First Search (BFS)

Depth First Search:

* Pre-order
* In-order
* Post-order

In **Pre-Order DFS Traversal** we start at the root and we visit it and we check if there's a left child, if so we go down to the left child so now we're in B, we visit it and then we check if there is a left child, if there is we visit it and now we will visit D, and then check if there is a left child node, there isn't, then we check if there is a right child node, there isn't so we go back up check B, for a right child node, there isn't so we go up to A, check if there is a right child, there is, so we now visit C, again check if there is a left child node, there isn't so we check if there is a right child node. 

                                      A 
                                    /   \
                                   B     C
                                  /
                                 D 

Visit order: 

A, B, D, C


___

**Traverse a tree (depth first search)**

Traversing a tree means "visiting" all the nodes in the tree once. Unlike an array or linked list, there's more than one way to walk through a tree, starting from the root node.

Traversing a tree is helpful for printing out all the values stored in the tree, as well as searching for a value in a tree, inserting into or deleting values from the tree. There's depth first search and breadth first search.

Depth first search has 3 types: pre-order, in-order, and post-order.

Let's walk through pre-order traversal by hand first, and then try it out in code.

Create a sample tree:


                                  apple
                                /       \
                            banana      cherry
                            /              
                        dates

```Python
# this code makes the tree that we'll traverse

class Node(object):
        
    def __init__(self,value = None):
        self.value = value
        self.left = None
        self.right = None
        
    def set_value(self,value):
        self.value = value
        
    def get_value(self):
        return self.value
        
    def set_left_child(self,left):
        self.left = left
        
    def set_right_child(self, right):
        self.right = right
        
    def get_left_child(self):
        return self.left
    
    def get_right_child(self):
        return self.right

    def has_left_child(self):
        return self.left != None
    
    def has_right_child(self):
        return self.right != None
    
    # define __repr_ to decide what a print statement displays for a Node object
    def __repr__(self):
        return f"Node({self.get_value()})"
    
    def __str__(self):
        return f"Node({self.get_value()})"
    
    
class Tree():
    def __init__(self, value=None):
        self.root = Node(value)
        
    def get_root(self):
        return self.root
```
```Python
# create a tree and add some nodes
tree = Tree("apple")
tree.get_root().set_left_child(Node("banana"))
tree.get_root().set_right_child(Node("cherry"))
tree.get_root().get_left_child().set_left_child(Node("dates"))
```

___

**Depth first, pre-order traversal with a stack**

visited in this order:

apple, banana, dates, cherry

**Stack**

Notice how we're retracing our steps. It's like we are hiking on a trail, and trying to retrace our steps on the way back. This is an indication that we should use a stack.

```Python 
# Let's define a stack to help keep track of the tree nodes
class Stack():
    def __init__(self):
        self.list = list()
        
    def push(self,value):
        self.list.append(value)
        
    def pop(self):
        return self.list.pop()
        
    def top(self):
        if len(self.list) > 0:
            return self.list[-1]
        else:
            return None
        
    def is_empty(self):
        return len(self.list) == 0
    
    def __repr__(self):
        if len(self.list) > 0:
            s = "<top of stack>\n_________________\n"
            s += "\n_________________\n".join([str(item) for item in self.list[::-1]])
            s += "\n_________________\n<bottom of stack>"
            return s
        
        else:
            return "<stack is empty>"
```
```Python
# check Stack
stack = Stack()
stack.push("apple")
stack.push("banana")
stack.push("cherry")
stack.push("dates")
print(stack.pop())
print("\n")
print(stack)
```
**Walk through the steps with code**

We're going to translate what we're doing by hand into code, one step at a time. This will help us check if our code is doing what we expect it to do.

```Python
visit_order = list()
stack = Stack()

# start at the root node, visit it and then add it to the stack
node = tree.get_root()
stack.push(node)

print(f"""
visit_order {visit_order} 
stack:
{stack}
""")
```

```Python
# visit apple
visit_order.append(node.get_value())
print(f"""visit order {visit_order}
{stack}
""")
```

```Python
# check if apple has a left child
print(f"{node} has left child? {node.has_left_child()}")

# since apple has a left child (banana)
# we'll visit banana and add it to the stack
if node.has_left_child():
    node = node.get_left_child()
    stack.push(node)

print(f"""
visit_order {visit_order} 
stack:
{stack}
""")
```

```Python
# visit banana
print(f"visit {node}")
visit_order.append(node.get_value())
print(f"""visit_order {visit_order}""")
```

```Python
# check if banana has a left child
print(f"{node} has left child? {node.has_left_child()}")

# since banana has a left child "dates"
# we'll visit "dates" and add it to the stack
if node.has_left_child():
    node = node.get_left_child()    
    stack.push(node)
    
print(f"""
visit_order {visit_order} 
stack:
{stack}
""")
```

```Python
# visit dates
visit_order.append(node.get_value())
print(f"visit order {visit_order}")
```
```Python
# check if "dates" has a left child
print(f"{node} has left child? {node.has_left_child()}")
```

```Python
# since dates doesn't have a left child, we'll check if it has a right child
print(f"{node} has right child? {node.has_right_child()}")
```

```Python
# since "dates" is a leaf node (has no children), we can start to retrace our steps
# in other words, we can pop it off the stack.
print(stack.pop())
```

```Python
print(stack)
```

```Python
# now we'll set the node to the new top of the stack, which is banana
node = stack.top()
print(node)
```
```Python
# we already checked for banana's left child, so we'll check for its right child
print(f"{node} has right child? {node.has_right_child()}")
```
```Python
# banana doesn't have a right child, so we're also done tracking it.
# so we can pop banana off the stack
print(f"pop {stack.pop()} off stack")
print(f"""
stack
{stack}
""")
```
```Python
# now we'll track the new top of the stack, which is apple
node = stack.top()
print(node)
```
```Python
# we've already checked if apple has a left child; we'll check if it has a right child
print(f"{node} has right child? {node.has_right_child()}")
```

```Python
# since it has a right child (cherry), 
# we'll visit cherry and add it to the stack.
if node.has_right_child():
    node = node.get_right_child()
    stack.push(node)
    
print(f"""
visit_order {visit_order} 
stack
{stack}
""")
```

```Python
# visit cherry
print(f"visit {node}")
visit_order.append(node.get_value())
print(f"""visit_order: {visit_order}""")
```

```Python
# Now we'll check if cherry has a left child
print(f"{node} has left child? {node.has_left_child()}")

# it doesn't, so we'll check if it has a right child
print(f"{node} has right child? {node.has_right_child()}")
```

```Python
# since cherry has neither left nor right child nodes,
# we are done tracking it, and can pop it off the stack

print(f"pop {stack.pop()} off the stack")

print(f"""
visit_order {visit_order} 
stack
{stack}
""")
```

```Python
# now we're back to apple at the top of the stack.
# since we've already checked apple's left and right child nodes,
# we can pop apple off the stack

print(f"pop {stack.pop()} off stack")
print(f"pre-order traversal visited nodes in this order: {visit_order}")
```

```Python
print(f"""stack
{stack}""")
```

___

**pre-order traversal using a stack (something's missing)**

> it's going from B and then checking if there is a left child and there is, so it goes back to D. We don't want that! 


Here is some code that has an error, so it will have an infinite loop. There is a counter to make the loop stop so that it doesn't run forever.
```Python
def pre_order_with_stack_buggy(tree):
    visit_order = list()
    stack = Stack()
    node = tree.get_root()
    stack.push(node)
    node = stack.top()
    visit_order.append(node.get_value())
    count = 0
    loop_limit = 7
    while(node and count < loop_limit): 
        print(f"""
loop count: {count}
current node: {node}
stack:
{stack}
        """)
        count +=1
        if node.has_left_child():
            node = node.get_left_child()
            stack.push(node)
            # using top() is redundant, but added for clarity
            node = stack.top() 
            visit_order.append(node.get_value())
            
        elif node.has_right_child():
            node = node.get_right_child()
            stack.push(node)
            node = stack.top()
            visit_order.append(node.get_value())

        else:
            stack.pop()
            if not stack.is_empty():
                node = stack.top()
            else:
                node = None
        
        
    return visit_order
```

```Python
pre_order_with_stack_buggy(tree)
```

___

**pre-order traversal using a stack, tracking state**

Here's how we implement DFS with a stack, where we also track whether we've already visited the left or right child of the node.

```Python
class State(object):
    def __init__(self,node):
        self.node = node
        self.visited_left = False
        self.visited_right = False
        
    def get_node(self):
        return self.node
    
    def get_visited_left(self):
        return self.visited_left
    
    def get_visited_right(self):
        return self.visited_right
    
    def set_visited_left(self):
        self.visited_left = True
        
    def set_visited_right(self):
        self.visited_right = True
        
    def __repr__(self):
        s = f"""{self.node}
visited_left: {self.visited_left}
visited_right: {self.visited_right}
        """
        return s
```

```Python
def pre_order_with_stack(tree, debug_mode=False):
    visit_order = list()
    stack = Stack()
    node = tree.get_root()
    visit_order.append(node.get_value())
    state = State(node)
    stack.push(state)
    count = 0
    while(node):
        if debug_mode:
            print(f"""
loop count: {count}
current node: {node}
stack:
{stack}
            """)
        count +=1
        if node.has_left_child() and not state.get_visited_left():
            state.set_visited_left()
            node = node.get_left_child()
            visit_order.append(node.get_value())
            state = State(node)
            stack.push(state)

        elif node.has_right_child() and not state.get_visited_right():
            state.set_visited_right()
            node = node.get_right_child()
            visit_order.append(node.get_value())
            state = State(node)

        else:
            stack.pop()
            if not stack.is_empty():
                state = stack.top()
                node = state.get_node()
            else:
                node = None
            
    if debug_mode:
            print(f"""
loop count: {count}
current node: {node}
stack:
{stack}
            """)
    return visit_order
```

```Python
# check pre-order traversal

pre_order_with_stack(tree, debug_mode=True)
```

**task 01: pre-order traversal with recursion**

Use recursion and perform pre_order traversal.

```Python 
def pre_order(tree):
    pass
```

`pre_order(tree)`

**Task: do in-order traversal**

We want to traverse the left subtree, then visit the node, and then traverse the right subtree. 

hint: it's very similar in structure to pre-order traversal.

```Python
# define in order 
def in_order(tree):
    pass
```

```Python
# check solution: should ge: ['dates', 'banana', 'apple', 'cherry']
in_order(tree)
```

**Task: post-order traversal**

Traverse left subtree, then right subtree, and then visit the node 

```Python
# define post_order traversal
def post_order(tree):
    pass
```

```Python
# check solution: should get: ['dates', 'banana', 'cherry', 'apple']
post_order(tree)
```

___

Using a stack to keep track of which node we visited:

DFS with a Stack

Pre-Order Traversal

Visit order:

A, B, D, C 

Then you are done with D so you remove (`pop`) it from the stack, check if it has a right child, nope, we remove B from the stack, then we are back to A, we check if it has a right child it does, So we add C to the stack, then check fr C's left and right child, it doesn't have them, so we are done with node C and we can pop it off the stack, then we are back to A, we alread visited it's left subtree and right subtree, so we `pop` it off the stack

___

DFS with Stack 

**Track State**
In-Order Traversal

Visit Order:

A, B, D, C


Start with root node, check if it has left child it does, so we visit it, then we make a node that A: visited left, the with B, we check if it has a subtree, it does, so we visit D, and Push D onto the Stack, and make a note that B: visited left, then we pop D off the stack, and now we are at B, now it already knows we visited the left sub tree and it won't do that again. as well as right subtree, then we can pop B off the stack, we already saved information that we already visited the left, so we are going to visit the right subnode, and visit C, and push C onto the stack, then add that for A, we already visited the left and right subtree as well, so with check we check left, we check right, pop it off the stack, back at A, the save information show we alread visited the left and right subnodes, it can be popped off the stack. 

___


### 14. Code: BFS 

Now, we are going to practice how to implement Breadth First Search in code. 

As a reminder breadth-first search is visiting the tree one level at a time so, if this was level zero we visit level by level, before moving on down to the next level. 

* Visit the tree one level at a time.

* BFS in graph data structures (shortest path)

Visit Order:

A, B, C, D 

___

**Traverse a tree (breadth first search)**

We'll now practice implementing breadth first search (BFS). You'll see breadth first search again when we learn about graph data structures, so BFS is very useful to know.

```Python
# this code makes the tree that we'll traverse

class Node(object):
        
    def __init__(self,value = None):
        self.value = value
        self.left = None
        self.right = None
        
    def set_value(self,value):
        self.value = value
        
    def get_value(self):
        return self.value
        
    def set_left_child(self,left):
        self.left = left
        
    def set_right_child(self, right):
        self.right = right
        
    def get_left_child(self):
        return self.left
    
    def get_right_child(self):
        return self.right

    def has_left_child(self):
        return self.left != None
    
    def has_right_child(self):
        return self.right != None
    
    # define __repr_ to decide what a print statement displays for a Node object
    def __repr__(self):
        return f"Node({self.get_value()})"
    
    def __str__(self):
        return f"Node({self.get_value()})"
    
    
class Tree():
    def __init__(self, value=None):
        self.root = Node(value)
        
    def get_root(self):
        return self.root

tree = Tree("apple")
tree.get_root().set_left_child(Node("banana"))
tree.get_root().set_right_child(Node("cherry"))
tree.get_root().get_left_child().set_left_child(Node("dates"))
```

**Breadth first search**

Breadth first traversal of the tree would visit the nodes in this order:

                                  apple
                                /       \
                            banana      cherry
                            /              
                        dates


apple, banana, cherry, dates


**Think through the algorithm**

We are walking down the tree one level at a time. So we start with apple at the root, and next are banana and cherry, and next is dates.

1) start at the root node
2) visit the root node's left child (banana), then right child (cherry)
3) visit the left and right children of (banana) and (cherry).

**Queue**
Notice that we're waiting until we visit "cherry" before visiting "dates". It's like they're waiting in line. We can use a queue to keep track of the order.

**Define a queue class**

```Python
from collections import deque
q = deque()
q.appendleft("apple")
q.appendleft("banana")
print(q)
```

```Python
q.pop()
```
```Python
print(q)
```

```Python
len(q)
```
```Python
from collections import deque
class Queue():
    def __init__(self):
        self.q = deque()
        
    def enq(self,value):
        self.q.appendleft(value)
        
    def deq(self):
        if len(self.q) > 0:
            return self.q.pop()
        else:
            return None
    
    def __len__(self):
        return len(self.q)
    
    def __repr__(self):
        if len(self.q) > 0:
            s = "<enqueue here>\n_________________\n" 
            s += "\n_________________\n".join([str(item) for item in self.q])
            s += "\n_________________\n<dequeue here>"
            return s
        else:
            return "<queue is empty>"
```

```Python
q = Queue()
q.enq("apple")
q.enq("banana")
q.enq("cherry")
print(q)
```
```Python
print(q.deq())
```
```Python
print(q)
```

**Walk through the steps with code**

```Python
visit_order = list()
q = Queue()

# start at the root node and add it to the queue
node = tree.get_root()
q.enq(node)
print(q)
```

```Python
# dequeue the next node in the queue. 
# "visit" that node
# also add its children to the queue

node = q.deq()
visit_order.append(node)
if node.has_left_child():
    q.enq(node.get_left_child())
if node.has_right_child():
    q.enq(node.get_right_child())
    
print(f"visit order: {visit_order}")
print(q)
```

```Python
# dequeue the next node (banana)
# visit it, and add its children (dates) to the queue 

node = q.deq()
visit_order.append(node)
if node.has_left_child():
    q.enq(node.get_left_child())
if node.has_right_child():
    q.enq(node.get_right_child())
    
print(f"visit order: {visit_order}")
print(q)
```

```Python
# dequeue the next node (cherry)
# visit it, and add its children (there are None) to the queue 

node = q.deq()
visit_order.append(node)
if node.has_left_child():
    q.enq(node.get_left_child())
if node.has_right_child():
    q.enq(node.get_right_child())
    
print(f"visit order: {visit_order}")
print(q)
```

```Python
# dequeue the next node (dates)
# visit it, and add its children (there are None) to the queue 

node = q.deq()
visit_order.append(node)
if node.has_left_child():
    q.enq(node.get_left_child())
if node.has_right_child():
    q.enq(node.get_right_child())
    
print(f"visit order: {visit_order}")
print(q)
```

**Task: write the breadth first search algorithm**

```Python
# BFS algorithm
def bfs(tree):

    pass
```

```Python
# check solution: should be: apple, banana, cherry, dates
bfs(tree)
```

___

**Bonus Task: write a print function**
Define the print function for the Tree class. Nodes on the same level are printed on the same line.

For example, the tree we've been using would print out like this:

Node(apple)
Node(banana) | Node(cherry)
Node(dates) | <empty> | <empty> | <empty>
<empty> | <empty>
We'll have <empty> be placeholders so that we can keep track of which node is a child or parent of the other nodes.

hint: use a variable to keep track of which level each node is on. For instance, the root node is on level 0, and its child nodes are on level 1.


```Python
# starter code

class Tree():
    def __init__(self, value=None):
        self.root = Node(value)
        
    def get_root(self):
        return self.root
    
    """
    define the print function
    """
    def __repr__(self):
        pass
```

```Python
# check solution
tree = Tree("apple")
tree.get_root().set_left_child(Node("banana"))
tree.get_root().set_right_child(Node("cherry"))
tree.get_root().get_left_child().set_left_child(Node("dates"))
print(tree)
```

<details><summary><b>Solution</b></summary>
<p>

```Python 
# Add solution from video 
```
</p>
</details>


___


### 15. Code: BST

Binary Search Trees Intro

* Nodes have an **order**
* Insert: log(n) the average complexity 
* Search: log(n) the average complexity 
* Delete: log(n) the average complexity

```
                              5
                             / \
                            4   6
                           /
                          2
```

6 is greater than 5 so it is to the right of node 5, 4 is less than 5 so it is to the left of 5, 2 is less than 4 so its also to the left of 4.


**Define Node Class**

```Python
# this code makes the tree that we'll traverse

class Node(object):
        
    def __init__(self,value = None):
        self.value = value
        self.left = None
        self.right = None
        
    def set_value(self,value):
        self.value = value
        
    def get_value(self):
        return self.value
        
    def set_left_child(self,left):
        self.left = left
        
    def set_right_child(self, right):
        self.right = right
        
    def get_left_child(self):
        return self.left
    
    def get_right_child(self):
        return self.right

    def has_left_child(self):
        return self.left != None
    
    def has_right_child(self):
        return self.right != None
    
    # define __repr_ to decide what a print statement displays for a Node object
    def __repr__(self):
        return f"Node({self.get_value()})"
    
    def __str__(self):
        return f"Node({self.get_value()})"

```
```Python
from collections import deque
class Queue():
    def __init__(self):
        self.q = deque()
        
    def enq(self,value):
        self.q.appendleft(value)
        
    def deq(self):
        if len(self.q) > 0:
            return self.q.pop()
        else:
            return None
    
    def __len__(self):
        return len(self.q)
    
    def __repr__(self):
        if len(self.q) > 0:
            s = "<enqueue here>\n_________________\n" 
            s += "\n_________________\n".join([str(item) for item in self.q])
            s += "\n_________________\n<dequeue here>"
            return s
        else:
            return "<queue is empty>"
```

**Define insert**

Let's assume that duplicates are overriden by the new node that is to be inserted. Other options are to keep a counter of duplicate nodes, or to keep a list of duplicates nodes with the same value.

```Python
class Tree():
    def __init__(self):
        self.root = None
        
    def set_root(self,value):
        self.root = Node(value)
        
    def get_root(self):
        return self.root
    
    def compare(self,node, new_node):
        """
        0 means new_node equals node
        -1 means new node less than existing node
        1 means new node greater than existing node 
        """
        if new_node.get_value() == node.get_value():
            return 0
        elif new_node.get_value() < node.get_value():
            return -1
        else:
            return 1
    
    """
    define insert here
    can use a for loop (try one or both ways)
    """
    def insert_with_loop(self,new_value):
        pass

    """
    define insert here (can use recursion)
    try one or both ways
    """  
    def insert_with_recursion(self,value):
        pass
                    
    def __repr__(self):
        level = 0
        q = Queue()
        visit_order = list()
        node = self.get_root()
        q.enq( (node,level) )
        while(len(q) > 0):
            node, level = q.deq()
            if node == None:
                visit_order.append( ("<empty>", level))
                continue
            visit_order.append( (node, level) )
            if node.has_left_child():
                q.enq( (node.get_left_child(), level +1 ))
            else:
                q.enq( (None, level +1) )

            if node.has_right_child():
                q.enq( (node.get_right_child(), level +1 ))
            else:
                q.enq( (None, level +1) )

        s = "Tree\n"
        previous_level = -1
        for i in range(len(visit_order)):
            node, level = visit_order[i]
            if level == previous_level:
                s += " | " + str(node) 
            else:
                s += "\n" + str(node)
                previous_level = level

                
        return s
```
```Python

```

```Python
tree = Tree()
tree.insert_with_loop(5)
tree.insert_with_loop(6)
tree.insert_with_loop(4)
tree.insert_with_loop(2)
tree.insert_with_loop(5) # insert duplicate
print(tree)
```

```Python
tree = Tree()
tree.insert_with_recursion(5)
tree.insert_with_recursion(6)
tree.insert_with_recursion(4)
tree.insert_with_recursion(2)
tree.insert_with_recursion(5) # insert duplicate
print(tree)
```

**Search**

Define a search function that takes a value, and returns true if a node containing that value exists in the tree, otherwise false.

```Python
class Tree():
    def __init__(self):
        self.root = None
        
    def set_root(self,value):
        self.root = Node(value)
        
    def get_root(self):
        return self.root
    
    def compare(self,node, new_node):
        """
        0 means new_node equals node
        -1 means new node less than existing node
        1 means new node greater than existing node 
        """
        if new_node.get_value() == node.get_value():
            return 0
        elif new_node.get_value() < node.get_value():
            return -1
        else:
            return 1
    
    def insert(self,new_value):
        new_node = Node(new_value)
        node = self.get_root()
        if node == None:
            self.root = new_node
            return
        
        while(True):
            comparison = self.compare(node, new_node)
            if comparison == 0:
                # override with new node
                node = new_node
                break # override node, and stop looping
            elif comparison == -1:
                # go left
                if node.has_left_child():
                    node = node.get_left_child()
                else:
                    node.set_left_child(new_node)
                    break #inserted node, so stop looping
            else: #comparison == 1
                # go right
                if node.has_right_child():
                    node = node.get_right_child()
                else:
                    node.set_right_child(new_node)
                    break # inserted node, so stop looping
                    
    """
    implement search
    """
    def search(self,value):
        pass
                    
    def __repr__(self):
        level = 0
        q = Queue()
        visit_order = list()
        node = self.get_root()
        q.enq( (node,level) )
        while(len(q) > 0):
            node, level = q.deq()
            if node == None:
                visit_order.append( ("<empty>", level))
                continue
            visit_order.append( (node, level) )
            if node.has_left_child():
                q.enq( (node.get_left_child(), level +1 ))
            else:
                q.enq( (None, level +1) )

            if node.has_right_child():
                q.enq( (node.get_right_child(), level +1 ))
            else:
                q.enq( (None, level +1) )

        s = "Tree\n"
        previous_level = -1
        for i in range(len(visit_order)):
            node, level = visit_order[i]
            if level == previous_level:
                s += " | " + str(node) 
            else:
                s += "\n" + str(node)
                previous_level = level

                
        return s
```
```Python

```

```Python
tree = Tree()
tree.insert(5)
tree.insert(6)
tree.insert(4)
tree.insert(2)

print(f"""
search for 8: {tree.search(8)}
search for 2: {tree.search(2)}
""")
print(tree)
```


Bonus: deletion

<details><summary><b>Solution</b></summary>
<p>

```Python 

```
</p>
</details>

___

<details><summary><b>Solution</b></summary>
<p>

```Python 
# Add solution video 
```
</p>
</details>


___

### 16. Diameter of a Binary Tree

**Problem statement**

Given the root of a binary tree, find the diameter.

Note: Diameter of a Binary Tree is the maximum distance between any two nodes

```Python
class BinaryTreeNode:

    def __init__(self, data):
        self.left = None
        self.right = None
        self.data = data
```
```Python
def diameter_of_binary_tree(root):
    """
    :param: root - Root of binary tree
    TODO: Complete this method and return diameter (int) of binary tree
    """
    pass
```

You can use the following function to test your code with custom test cases. The function `convert_arr_to_binary_tree` takes an array input representing level-order traversal of the binary tree.

                                      1
                                     / \
                                    2   3
                                   /     \
                                  4       5

The above tree would be represented as `arr = [1, 2, 3, 4, None, 5, None, None, None, None, None]`

Notice that the level order traversal of the above tree would be `[1, 2, 3, 4, 5].`

Note the following points about this tree:

`None` represents the lack of a node. For example, `2` only has a left node; therefore, the next node after 4 (in level order) is represented as `None`
Similarly, `3` only has a left node; hence, the next node after `5` (in level order) is represted as `None`.
Also, `4` and `5` don't have any children. Therefore, the spots for their children in level order are represented by four `None` values (for each child of `4` and `5`).

