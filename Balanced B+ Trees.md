<br/><br/>

<div style="text-align: center;">
    <h1>Balanced B+ Trees</h1>
	<h3>Algorithms and Data Structures Report</h3>
	<h5>Degree in Bioinformatics, UPF</h5>
    <br/><br/>
    <br/><br/>
    <p>March 2022</p>
	<p>Dante Aviñó - 106390</p>
</div>


<div style="page-break-after: always; break-after: page;"></div>

<br/><br/>

<h2> Contents </h2>

- #### [1. Introduction: Overview](#Introduction)

- #### [2. B+ Tree](#B+Tree)

  - ##### [2.1. Properties](#B+Properties)
  - ##### [2.2. Structure](#B+Structure)
  - ##### [2.3. Operations](#B+Operations)

- #### [3. Uses of the B+ Tree](#B+Uses)

- #### [4. Conclusion: Thoughts](#Conclusion)

- #### [5. References: Sources of Information](#References)

<div style="page-break-after: always; break-after: page;"></div>

<br/><br/>

<div id='Introduction'/>
<h3>1. Introduction </h3>
The goal of this report is to study and learn from authoritative sources topics related to the Algorithms and Data Structures course.

In order to understand what B+ Trees are we first need to talk about some of the history related to this data structure. Why it is created? What problem solves? What was before?

So it's first necessary a bit about to talk about Binary search trees (BST), B-trees and the differences


Explain why B-trees are used when the search structure is on disk

The difference is that in B+-trees only leaf nodes contain the actual key values. The nonleaf nodes of the B+-trees contain router values.

Routers are entities of the same type as the key values, but they are not the keys stored in the search structure. They are only used to guide the search in the tree. In classical B-trees, the key values are stored in both leaf and non-leaf nodes of the tree.





Binary Search Trees:

Search trees are data structures that support many dynamic-set operations, including SEARCH, MINIMUM, MAXIMUM, PREDECESSOR, SUCCESSOR, INSERT, and DELETE. Thus, a search tree can be used both as a dictionary and as a priority queue.

B-trees:

B-trees have become, de facto, a standard for file organization. File indexes of users, dedicated database systems, and general-purpose access methods have all been proposed and nnplemented using B-trees

<div style="page-break-after: always; break-after: page;"></div>

<br/><br/>

<div id='B+Tree'/>
<h3>2. B+ tree</h3>

<div id='B+Structure'/>
<h4>2.1. Structure</h4>

A B+ tree T consists of nodes. One of the nodes is a special node T.root. 

If a node x is a non-leaf node, it has the following fields: 

- x.n the number of router values currently stored in node x 

- The router values stored in node x in increasing order 

  x.router1 < x.router2 < ... < x.routerx.n 

- x.leaf , a boolean field whose value is FALSE meaning that x is a non-leaf node •

- x.n+1 pointers x.c1, x.c2, x.c3,...,x.cx.n+1 to the children of x. 

If the node x is a leaf node, it has the following fields 

- x.n number of key values currently stored in x. 1 

- The key values stored in node x in increasing order 

  x.key1 < x.key2 < ... < x.keyx.n 
  
- x.leaf , a boolean field whose value is TRUE meaning that x is a leaf node. 

If we consider a non-leaf node x and pointers in it x.c1, x.c2, x.c3,...,x.cx.n+1 
the following condition is true: 
k1 ≤ x.router1 < k2 ≤ x.router2 < k3 ... < kx.n ≤ x.routerx.n < kx.n+1

where ki is any key or router value in the subtree pointed by the pointer x.ci. 

An example of the non-leaf node containing 5 router values:

<br/><br/>

<div id='B+Properties'/>
<h4>2.2. B+ Properties </h4>

The B+ tree has to satisfy the following balance conditions: 

• Every path from the root node to a leaf node has an equal length, i.e. every leaf node has the same depth which is the height of the tree. 

• Every node of the B+-tree except the root node is at least half-filled. The latter condition can be formulated more exactly: denote by s(x) the number of children of node x if x is a non-leaf node and the number of keys stored in x if x is a leaf node. Let t ≥ 2 be a fixed integer constant. For each node x of the B+-tree, the following is true: 

​	• 1 ≤ s(x) ≤ 2t, if x is the only node in the tree. 

​	• 2 ≤ s(x) ≤ 2t, if x is the root node and the tree contains also other nodes in addition to the root node. 

​	• t ≤ s(x) ≤ 2t, otherwise. 

Because the B+-tree satisfies the given balance conditions, we can prove that the hight h of the B+ tree 

<p style="text-align: center;">h ≤ logt n</p>

where n is the number of the keys stored in the tree.

<br/><br/>

<div id='B+Operations'/>
<h4>2.3. B+ Operations</h4>

<h5>Searching</h5>

```c++
BTreeSearch(T,k)
x = T.root
while not x.leaf
	i = 1
	while i ≤ x.n and k > x.routeri
		i = i+1
	x = x.ci
	DiskRead(x)
i = 1
while i ≤ x.n and k > x.keyi
	i = i+1
if i ≤ x.n and k = x.keyi
	return ( x, i )
else return NIL
```
<u>**Time Complexity**</u>

<h4>Insertion</h4>

<h4>Deletion</h4>

<div style="page-break-after: always; break-after: page;"></div>

<br/><br/>

<div id='B+Uses'/>
<h3>3. Uses of the B+ Tree</h4>
B+ trees are one of the most popular data structures for databases today. They are used to store and retrieve large amounts of data very quickly.

<div style="page-break-after: always; break-after: page;"></div>

<br/><br/>

<div id='Conclusion'/>
<h3>4. Conclusion: Thoughts</h4>

<div style="page-break-after: always; break-after: page;"></div>
<br/><br/>

<div id='References'/>
<h3>5. References: Sources of Information</h4>

**Introduction to algorithms; [Thomas H. Cormen](https://edutechlearners.com/download/Introduction_to_algorithms-3rd%20Edition.pdf), 3rd Edition (2009)**

**Organization and maintenance of large ordered indices; [R. Bayer, E. McCreight](https://infolab.usc.edu/csci585/Spring2010/den_ar/indexing.pdf), July 1970**

**The Ubiquitous B-Tree; [Comer, Douglas](http://carlosproal.com/ir/papers/p121-comer.pdf), June 1979**

**2-3 and B-Trees; [Shankha, Amartya](https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-046j-design-and-analysis-of-algorithms-spring-2015/recitation-videos/recitation-2-b-trees), March 2016**

