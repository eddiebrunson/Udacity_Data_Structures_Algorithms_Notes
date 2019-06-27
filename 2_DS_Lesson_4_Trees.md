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

### 8. Binary Search Tree

Ordering of elements are different amount different types of trees.

There is a specific type of binary tree called a **binary search tree(BST)**

Every parent node has at most two children. 

BSTs are sorted so every valu on the left of a particular node is smaller than it and every value on the right of a particular node is larger than it. 

Because BSTs have this structure, we can do operations like search, insert, and delete pretty quickly. 

The run time of a search on a BST is just the height of the tree, which we proved was log(n) when we learned about inserting. 

Inserting in a binary tree is pretty much the same process. 

You start at the top and you can make quick decisions about where to look at.


___

### 9. BST Complications

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



