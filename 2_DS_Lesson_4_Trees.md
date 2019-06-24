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

A level order traveral is exactly what it sounds like. Start at the root then visit it's children on the second level then all of their children on the third level until you've visited every single leaf. 

By convention, we start on the left most side of the level and move right. 

___

### 5. Depth-First Traversals 

There are several different approaches to DFS and trees. 

First there is **Pre-Order** traversals, check off a node as you see it before you traverse any furthere in the tree. 

Check the root node, then by convention go down the next node on the left and continue traversing down the left most nodes until we hit a leaf. 








