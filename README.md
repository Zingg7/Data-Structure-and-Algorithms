# Lecture 1: Course Introduction 

## Data Structure vs. Abstracted Data Type

### Data Structure

- Collection containing:
  - Data values
  - Relationshis among the data
  - Operations applied to the data
- Describes exactly how the data are organized and how tasks are performed
  确定了数据结构究竟应该怎么实现(e.g. Array List)

### Abstract Data Types

- Defined by its behavior from the view of the user
  - What operations must it have?
- Describes only what need to be done, not how it is done
  阐述该结构有哪些功能(e.g. List)


# Lecture 2: C++ Review 

## C++ Classess, Source Code, and Headers

### Member Initializer List

```
class Point {
	private:
		int x;
		int y;

	public:
		Point(int i, int j);
};

Point::Point(int i, int j) {
	x = i;
	y = j;
}

// Which equals to
Point::Point(int i, int j) : x(i), y(j) {}
```

### Header and Source File

Header Files(.h): Contains just the class with the declaration of everything
Source Files(.cpp): Implementations of everything declared in the header file 


## C++ Memory Diagram

### Reference: Like an alias

```
Student s1 = Student("Niema");
Student & s2 = s1;
Student s3 = s2;
```

### Pointer: A pointer which stores the address of object, like the reference of Java

int * a: 

```
Student s = Student("Niema");
Student* ptr = &s;
Student** ptrPtr = &ptr;
```

```
int i = 1;
int* a = &i;
cout << a << endl;      // address
cout << *a << endl;    // 1
cout << &i << endl;    // address
cout << *&i << endl;   // 1
```

* : 取这个地址对应的值
  & : 取它的地址

### Modifying Arguments

```
void zero(int x) {
    x = 0;
}

int main() {
    int myInt = 42;
    zero(myInt);
    cout << myInt;      // print 42
}
```

```
void zero(int & x) {
    x = 0;
}

int main() {
    int myInt = 42;
    zero(myInt);
    cout << myInt;       // print 0
}
```


```
void zero(int* x) {
    *x = 0;
}

int main() {
    int myInt = 42;
    zero(&myInt);
    cout << myInt;        // print 0
}
```


## The const Keyword

### const and Pointers

const int * : value cannot change, but the pointer could point to other value
int * const : cannot reassign the pointer(const pointer)

```
int a = 42;
const int * ptr1 = &a;
int const * ptr2 = &a;  // this two lines is the same
int * const ptr3 = &a;
const int * const prt4 = &a;
```

### const and References

const int & : cannot modifu the var through the const ref

```
int a = 42;
const int & ref1 = a;    // a = 21 is ok, ref1 = 20 is not ok
int const & ref2 = a;    // same as above
```

### const Functions

cannot modify my object 


## C++ Input/Output

```
using namespace std;
int n;
cout << "Enter a number: ";
cin >> n;

string message;
cout << "Enter a message: ";
getline(cin, message);

if (cin.fail()) {
	cerr << "Bad input!" << endl;
}
```


## C++ Template

```
template<typeanme Data>
class Node {
	public:
		Data const data;
		Node(const Data &d) : data(d) {}
};

Node<string> a(s);
Node<int> b(n);
```

# Lecture 3: C++ Iterators 

## Iterating Over Arrays

```
void print_inorder(int * p, int size) {
	for (int i = 0; i < size; ++i) {
		cout << * p << endl;
		++p;
	}
}
```


## Using Iterators

for vector: Keeping track of the index

```
vector<string> names;
/ * populate with data */

vector<string>::iterator itr = names.begin();
vector<string>::iterator end = names.end();

while(itr != end) {
	cout << * itr << endl;       // overload
	++itr;
}
```

for LinkedList: `curr` would be a node pointer


## Creating an Iterator Class

- Operators in the Iterator class:
  - `==` 
  - `!=`
  - `*`(derefernce) return a refernce to the current data value
  - `--`(pre) and `++`(post) move our iteratore to the next item
- Functions in the Data Structure class:
  - `begin()` returns iterator to the first element
  - `end()` returns iterator to just after last element

> the size of iterator is O(1)

### Question about Iterator

In the video, linked list iterators were represented as tracking a current node, in contrast to the vector iterator which tracked an index.

Say we tried to use an index (along with information about the head node) as the internal state of the iterator for a linked list. What problems could result?

- There would be no problems and it could be just as efficient
- It would not be possible to implement a linked list iterator with just the index and a head node
- The overloading of the ++ operator would likely be much slower (linear rather than constant time in list size)
- The overloading of the * dereference operator would likely be much slower (linear rather than constant time in list size)

Ans: D
because you have to starting from the beginning to dereference the pointer, instead of dereferencing directly via the current node's address, eg we want to dereference node 3, one way is to start from head and then compute the address of node 3, the other way is via the address of node 3 directly

### Question about Arrays and iterators

You're implementing an iterator class called VectorIterator that you want to use to iterate through a vector of integers (vector<int>).

You're working on overloading the * (dereference) operator. So far, you've written the following code:

class VectorIterator {
	private:
		vector<int>* ptr;
		int index;

	public:
		int operator*() const { 
		return (*(this->ptr))[index];
	}

}

## Difference between `.`, `->`, `::`

`.` for object
`->` for pointer
`::` for class

# Lecture 4: Time and Space Complexity 

## Notations of Complexity

- Big-O: uppder bound
  C * g(n) ≥ f(n) when n->inf
  e.g. 2n is O(n)
- Big-Ω: lower bound
  C * g(n) ≤ f(n) when n->inf
  e.g. 0.5n is Ω(n)
- Big-ø: both upper and lower bound
  A * g(n) ≤ f(n) ≤ B * g(n)


## Finding Big-O Time Complexity

1. Determine f(n): # operattions vs. n
2. Drop all lower terms of n
3. Drop constant coefficients 


## Common Big-O Time Complexities

- O(1): Constant
- O(logn): Logarithmic
- O(n): Linear
- O(nlogn)
- O(n^2): Quadratic
- O(n^2): Cubic


### Question about Comparative runtime analysis

Which of the following are true? Select one or more answers.

- 12n is O(13n)
- 12n is Θ(13n)
- 2^n is Θ(3^n)
- n^2 is Ω(2n)
- log(n) is Ω(nlog(n))
- nlog(k) is Θ(n) (where k is a constant)

Ans: ABDF


# Lecture 5: Binary Search Trees

## What Are Trees?

1. No undirected cycles
2. Connected

- For a graph T to be considered a tree, it must follow all of the following constraints (which can be proven to be equivalent constraints):

1. T is connected and has no undirected cycles (i.e., if we made T's directed edges undirected, there would be no cycles)
2. T is acyclic, and a simple cycle is formed if any edge is added to T
3. T is connected, but is not connected if any single edge is removed from T
4. There exists a unique simple path connecting any two vertices in T

- If T has n vertices (where n is a finite number), then the above statements are equivalent to the following two conditions:

1. T is connected and has n−1 edges
2. T has no simple cycles and has n−1 edges

https://stepik.org/lesson/28726/step/3?unit=9784


## Tree Traversals

- Preorder: Visit, Left, Right
- Inorder: Left, Visit, Right (only binary tree)
- Postorder: Left, Right, Visit
- Level-Order: 1st level(left to right), 2nd level


## Properties of a Binary Search Tree (BST)

1. Rooted Binary Tree
   - All nodes except the root have a parent
   - All nodes have either 0, 1, or 2 children
2. Every node is larger than all nodes in its left subtree
3. Every node is smaller than all nodes in its right subtree


## BST Algorithm

### Find

1. Start at the root
2. If query == current, success
3. Otherwise, if query > current, traverse right and go to #2
4. Otherwise, if query < current, traverse left and go to #2
   If you every try to traverse left/right but no such child exists, fails

### Insert

1. Perform "find" algorithm starting at root
2. If "find" succeed, duplicate element!
3. If "find" doesn't succeed, insert the new element at the site of failure

[implementation](https://stepik.org/lesson/28727/step/4?unit=9785)

### Successor

1. If the node has a right child, traverse right once, then all the way left
2. Otherwise, traverse up the tree. The first time the current node is its parent's left child, the parent is our successor

[implementation](https://stepik.org/lesson/28727/step/6?unit=9785)

### Remove

- Case 1: No children
  - Just delete the node
- Case 2: 1 child
  - Just directly connect my child to my parent
- Case 3: 2 children
  - Replace my value with my successor's value, and remove me

[implementation](https://stepik.org/lesson/28727/step/7?unit=9785)

## BST Time Complexity

- Height of a node: Longest distance (#edges) from node to a left
- Hiehgt of a tree: Height of the root of the 
- Depth of a node: Number of **nodes** in the path from that node to the root (one more)

For BST, after making two assumptions about randomness:

1. All n elements are equally likely to be searched for
2. All n! possible insertion orders are equally likely

- Insertion, removal, and finding is O(log n)

### Tree Balance

- A **balanced binary tree** is one where most leaves are equidistant from the root and most internal nodes have two children. A **perfectly balanced binary tree** is one where all leaves are equidistant from the root, and all﻿ internal nodes have two children. 
  - Time Complexity: log2(n+1)-1
- An **unbalanced binary tree** is one where many internal nodes have exactly one child and/or leaves are not equidistant from the root. A **perfectly unbalanced binary tree** is one where all internal nodes have exactly one child.
  - Time Complexity: n - 1

### Question

#### BST deletion

You're writing a method deleteSubtree() that removes a given node and all of its children (i.e. the node and its subtree) from a BST, including deleting their memory.

```
void deleteSubtree(Node* n) {
  // TODO
}
```

Which of the following traversals would be particularly useful to implement this method?

In-order, because it will preserve the ordering of the BST
Pre-order, because it's important to delete the parents before the children
Post-order, because it's important to delete the children before the parents
Level-order, because it's important to clear each level of the hierarchy one at a time

Ans: C

#### BST vs Linked List

You're given a vector of integers, sortedNums, which is sorted in ascending order (i.e. lowest to highest). You create a BST by iterating through sortedNums and inserting each element:

```
BST tree;
for (int num : sortedNums) {
  tree.insert(num);
}
```

In which of the following ways is the BST created by this process better than a Linked List? Select one or more answers.

This BST offers a faster average-case lookup
This BST offers a faster average-case deletion
This BST offers a faster worst-case lookup
This BST offers a faster worst-case deletion
None of the above

Ans: E

Reason: Tree created by sortedNums insertion is an unbalanced tree.

### Comment

It turns out that, unfortunately for us, real-life data do not usually follow these two assumptions, and as a result, in practice, a regular Binary Search Tree does not fare very well. However, is there a way we can be a bit more creative with our binary search tree to improve its average-case (or hopefully even worst-case) time complexity? In the next sections of this text, we will discuss three "self-balancing" tree structures that come about from clever modifications to the typical Binary Search Tree that will improve the performance we experience in practice: the Randomized Search Tree (RST), AVL Tree, and Red-Black Tree.

# Lecture 6: K-D Trees

A special case of Binary Search Trees to allow data across two or more dimensions. K-dimensional extension of a BST, each level of the tree organizes the data along a different dimension, cycling through each dimension repeatedly.


## KDT Insertion Order and Balance

1. Sort elements by current dim (start with x)
2. Pick medium element to insert next
3. Recurese on left and on right remaining points, switch dimension


## KDT Closest Point

1. Search the tree for the query point, until we reach a leaf
2. Checks to see if the node is closer to the current nearest neighbor.  If it is, it chooses the node as the new current nearest neighbor.
3. Checks to see if the nearest neighbor might be in the other subtree of the current node (the one it didn't just come from) by checking if the distance between the splitting coordinate of the current node and the query point is smaller than the distance to the current nearest neighbor.  If so, it checks the other side of the tree via a recursive call.  

https://stepik.org/lesson/330393/step/8?unit=313763

```
nearest_neighbor(query, root, 0)
nearest_neighbor(query, root, d):
	if node is leaf:
		return node
	if query[d] < node[d]:
		best = nearest_neighbor(query, node.leftChild, d+1)
	else if query[d] > node[d]:
		best = nearest_neighbor(query, node.rightChild, d+1)
	else:  // equal
		return node

	// best is the current nearest neighbor
	if distance(node ,query) < distance(query, best):
		best = node
		tmp = nearest_neighbor(query, node.otherChild, d+1)
		if distance(node, query) > distance(tmp, query):
			best = temp
	return best
```

# Lecture 7: Treaps and Randomized Search Trees (RSTs)

## Random Numbers

- True random numbers: truly random, but can only be generated by harvesting natural entropy, which is slow
- Pseudo-random numbers: seemingly random, but deterministic upon the seed, but can be generated very quickly

Remember that we can combine these two random number generation approaches by using a true random number to seed a pseudo-random number generator.

### Generate random number

1. Seed random number generator using system time
2. generate random number from 0 through RAND_MAX

```
srand(time(NULL));
int number = rand(); 
```

### Generate number from 0 to 1

```
x = rand() / RAND_MAX;
```


## Heap

Heap is a tree that satisfies the Heap Property: For all nodes A and B﻿, if node A is the parent of node B, then node A has higher priority (or equal priority) than node B.

- Inserting and popping: worst-case time complexity of O(log n)
- Peeking: O(1) worst-case time complexity for highest-priority element.

### Binary Heap

The binary heap has three constraints:

- Binary Tree Property: All nodes in the tree must have either 0, 1, or 2 children
- Heap Property (explained above)
- Shape Property: A heap is a **complete** tree. In other words, all levels of the tree, except possibly the bottom one, are fully filled, and, if the last level of the tree is not complete, the nodes of that level are filled from left to right


### Min-heap and Max-heap

- Min-heap: a heap where every node is smaller than (or equal to) all of its children (or has no children)
- Max-heap: a heap where every node is larger than (or equal to) all of its children (or has no children)


### Store a binary heap as an array

- its parent is at index `⌊(i−1)/2⌋`
- its left child is at index `2i+1`
- its right child is at index `2i+2`


### Exercise

#### Which property (or properties) of a binary heap give rise to the O(log n) worst-case time complexity of the insertion algorithm? (Select all that apply)

- Shape Property
- Heap Property
- Binary Tree Property

Ans: AB

https://stepik.org/lesson/28863/step/9?unit=9900

#### Which of the following statements are true? (Select all that apply)

- Given an index in the array representation of a binary heap, we can find the parent, left child, and right child of the element at that index in constant time using arithmetic
- The element at index i of the array representation of a binary heap must have a higher priority than all elements at indices larger than i
- By representing a heap as an array, we save on the memory costs from pointers in the tree representation
- If we were to iterate through the elements of the array representation of a binary heap, we would be traversing the corresponding tree representation in an in-order traversal

Ans: AC

https://stepik.org/lesson/28863/step/14?unit=9900


## Treaps

a Treap is a binary tree in which nodes contain two items, a key and a priority, and which must obey the following two restrictions:

1. The tree must follow the **Binary Search Tree** properties with respect to its **keys** (letter, max-heap)
   - larger than all keys in left subtree
   - smaller than all keys in right subtree
2. The tree must follow the **Heap Property** with respect to its **priorities** (number)
   - larger than all priorities below


## AVL Rotation

left rotation: 左边的左子树不变/右边的右子树不变，右边的左子树连到左边的右子树

### Treap Insertion

1. Insert via BST insert algorithm with respect to keys
2. Use AVL Rotation to "bubble up" to fix Heap with respect to priorities


## Randomized Search Trees 

A Randomized Search Tree is a Treap where, instead of us supplying both a key and a priority for insertion, we only supply a key, and the priority for the new (key, priority) pair is randomly generated for us.

- Find: Worst O(n), average O(logn)



# Lecture 8: AVL Trees

An AVL Tree is a Binary Search Tree in which, for all nodes in the tree, the heights of the two child subtrees of the node differ by at most one.

- Worst time complexity for finding, inserting, or removing: O(logn)

In order to analyze the AVL Tree, we will first provide some formal definitions:

1. The **balance factor** of a node u is equal to the **height** of u's right subtree minus the height of u's left subtree
2. A Binary Search Tree is an AVL Tree if, for all nodes u in the tree, the balance factor of u is either -1, 0, or 1


### AVL Tree Insertion

1. Perform the regular BST insertion algorithm. 
2. Starting at the newly-inserted node, traverse up the tree and update the balance factor of each of the new node's ancestors. For any nodes that are now "out of balance" (i.e., their balance factor is now less than -1 or greater than 1), perform AVL rotations to fix the balance.

AVL Tree required to make two passes through the tree for inserting or removing elements: 

1. One pass down the tree to actually perform the insertion or removal, 
2. Another pass up the tree to maintain the tree's balance. 



# Lecture 9: Red-Black Trees

A Red-Black Tree is a Binary Search Tree in which the following four properties must hold:

1. All nodes must be "colored" either red or black
2. The root of the tree must be black
3. If a node is red, all of its children must be black (i.e., we can’t have a red node with a red child)
4. For any given node u, every possible path from u to a "null reference" (i.e., an empty left or right child) must contain the same number of black nodes

### Red-Black Tree Insertion

1. Perform regular BST Insertion
   - If you see black node with 2 red children, recolor all 3
     - If the parent is the root, color it black
2. Color new node red
3. Potentially fix tree for Red-Black tree properties

### Which of the following statements are true? (Select all that apply)

- The height of a Red-Black Tree can be larger than the height of an AVL Tree with the same elements
- Red-Black Trees and AVL Trees have the same worst-case find, insert, and remove Big-O time complexities
- Some, but not all, Red-Black Trees are AVL Trees
- Red-Black Trees and AVL Trees have the same average-case find, insert, and remove Big-O time complexities
- The height of a Red-Black Tree is at most twice the height of an AVL Tree with the same elements
- All Red-Black Trees are AVL Trees

Ans: ABCDE



# Lecture 10: Set and Map ADTs

## The Set ADT

- Set: Store multiple elements (keys)
  - find(x): True if x exists in the set, otherwise false
  - insert(x): Add x to the set
  - remove(x): Remove x from the set


## The Map ADT

- Map: Store multiple (key, value) pairs
  - get(k): Return the value associated with key k if k exists in the map
  - put(k,v): Map the key k to the value v
  - remove(k): Remove key k and its value from the map


## Implementing the Set and Map ADTs

- Unsorted Linked List: O(n) find/remove, O(1) insert
- Sorted Linked List: O(n) find/remove/insert, can tierate in sorted order
- Unsorted ArrayList: O(n) find/remove, amortized O(1) insert
- Sorted ArrayList: O(logn) find, O(n) remove/insert, can iterate sorted
- Self-Balancing BST: O(logn) find/insert/remove, can iterate sorted
- Hash Table: O(1) expected, need to first perform O(k) hash

Set: Red-Black Tree
Unorder_Set: Hash Table

### Exercise

#### What is the worst-case time complexity of the find/insert/remove function defined in the previous pseudocode, ignoring the time it takes to compute an element's hash value?

- O(1)
- O(log n)
- O(n)
- O(n * log n)
- O(n²)
- Not enough information

Ans: C



# Lecture 11: Multiway Tries

- Trie: Tree structure in which elements are represented by paths 
- Multiway Tries: Trie in which nodes can have more than 2 children

## MWT Insert, Find, and Remove

### Find

1. Start at the root at the first letter
2. For each letter in my word, does my current node have a child edge labeled by  that letter
3. If it does, traverse it; if it doesn't, that word does not exist in my tree
4. Once I finish every single letter in my word, if the current node that I'm at happens to be a word node, return true; otherwise, return false

### Insert

1. Start at the root, start at the first letter 
2. For each letter in my word, does my current node have a child labeled by that letter
3. If it doesn't, create one, and then traverse down
4. When I finish, mark my current node as a word node

5. Attempt to follow the find algorithm
6. If, at any point, the edge we need to traverse does not exist, simply create the edge (and node to which it should point), and continue

### Remove

1. Follow the find algorithm
2. If the find algorithm fails, the word does not exist in the trie, meaning nothing has to be done
3. If the find algorithm succeeds, simply remove the "word node" label from the node at which the find algorithm terminates


## MWT Complexity

n = number of words
k = length of longest word

- Time Complexity: O(k)
- Space Complexity: O(n^k) 


## Cool Algorithms on MWTs

- Iterate in ascending order: preorder, iterate over children ascending
- Iterate in descending order: postorder, iterate over children descending
- Iterate in increasing order: preorder, level-order traversel
- Autocomplete: find, traversal from node I end at


### Question

#### BST vs MWT height

In Q3, we saw that a (well-balanced) BST and MWT can have different heights when populated with the same set of words.

This is not always true. Let's say we have an alphabet of `X` characters, and we're inserting all strings of length `D` (i.e. we're inserting X^D strings).

For a BST and MWT to have the same height, which of the following must be true about the words being inserted? Select one or more options (⌈⌉ and ⌊⌋ represent the ceiling and floor operators).

- X = 1
- D >= X
- ⌈log_2(X^D)⌉ = D
- ⌊log_2(X^D)⌋ = D
- X <= 2
- None of the above

Ans: C


# Lecture 12: Ternary Search Trees (TSTs)

A middle-ground between the Binary Search Tree and the Multiway Trie. 

The Ternary Search Tree (TST) is a type of trie in which nodes are arranged in a manner similar to a Binary Search Tree, but with up to three children rather than the binary tree's limit of two. 

Just like in a Binary Search Tree, for every node u, the left child of u must have a value less than u, and the right child of u must have a value greater than u. The middle child of u represents the next character in the current word.

(If the next step is not going down, do not count this word in)


## TST Algorithms

### TST Find

- current node = root
- c = first letter of query
- if c > current node's letter:
  - traverse to right child
- else if c < current node's letter:
  - traverse to left child
- else:
  - If c is last letter of query and current node is "word" node:
    - success!
  - else:
    - traverse to middle child and go to next letter in query

### TST Insert

- Perform TST Find
- If you every need to traverse to a child that doesn't exist, simply create it and traverse
- Make the last node in the traversal a "word" node

### TST Remove

- Perform TST Find
- Make the last node in the traversal not a "word" node


## TST Time Complexity

- Worst case: O(n)
- Average case: O(logn)


## Tree Summary

1. Balanced Binary Search Tree: AVL Tree or Red-Black Tree

- **Most space-efficient**
- **Worst case time complexity**: O(logn)
- Able to iterate over the elements of the lexicon in **alphabetical order**

2. Hash Table

- Not quite as space-efficient as a Binary Search Tree (but not too bad)
- **Average-case time complexity**: O(k)
- **Worst-case time complexity**: O(n)
- Unordered, no clean way of iterating through the elements of our lexicon in a meaningful order

3. Multiway Trie

- Most **time-efficient** we can get in worst case: O(k)
- **Extremely inefficient memory-wise**
- Able to iterate over the elements of the lexicon in **alphabetical order**
- Can perform **auto-complete** by performing a simple pre-order traversal

4. Ternary Search Tree


# Lecture 13: Hashing, Hash Tables, Hash Maps, and Collisions

## Hash Functions

- Input: An object x
- Output: An integer representation of x

#### Hash function property

- Requirement of all valid hash functions:
  - Property of Equality: Given two keys k and l, if k and l are equal, h(k) must equal h(l). In other words, if two keys are equal, they must have the same hash value
    -- hash function that fulfills requirement is call "good" hash function --
- A feature that would be "nice to have" if at all possible, but not necessary:
  - Property of Inequality: Given two keys k and l, if k and l are not equal, it would be nice if h(k) was not equal to h(l). In other words, if two keys are not equal, it would be nice (but not necessary!) for them to have different hash values
    -- hash function that fulfills requirement and feature is call "perfect" hash function --

#### Hash function Time Compelxity

if a given object key has k elements (e.g. a string with k characters, or a list with k numbers), a good hash function for key will incorporate each of key's k elements into key﻿'s hash value, meaning a good hash function would be O(k).

- Average-case for insert and find: O(1)
- Worst-case for insert and find: O(n)

## Hash Table and Hash Maps

Hash Table can be thought as a collection of items that, on average, can be retrieved really fast. A Hash Table is implemented by an array, and more formally, we define a Hash Table to be an array of size M (which we call the Hash Table's capacity) that stores keys k by using a hash function to compute an index in the array at which to store k.

- Hash Table: implements the Set ADT
- Hash Map: implements the Map ADT


## Probability of At Least 1 Collision

Insert N keys into M slots:

P_N,M(>= 1 collision) = 1 - P_N,M(0 collision)
P_N,M(0 collision) = 1 * (M-1)/M * (M-2)/M * ... (M-N+1)/M



# Lecture 14: Collision Resolution Strategies

## Open Addressing (Linear Probing)

**Linear Probing**: If an object key maps to an index that is already occupied, simply shift over and try the next available index.

Notice that the core of the Linear Probing algorithm is defined by this equation:

`index = (index + 1) % M`

By obeying the equation above, we are ensuring that our key is inserted strictly within an index (or more formally, an address) inside our Hash Table. 

Consequently, we call this a **closed hashing** collision resolution strategy (i.e., we will insert the actual key only in an address bounded by the realms of our Hash Table). 

Moreover, since we are inserting the keys themselves into the calculated addresses, we like to say that Linear Probing is an **open addressing** collision resolution strategy (i.e., the keys are open to move to an address other than the address to which they initially hashed.


## Double Hashing

**Double Hashing**: To use two hash functions: H_1(k) to calculate the hashing index and H_2(k) to calculate the offset in the probing sequence.

The solution to avoid keys having a higher probability to insert themselves into certain locations:

- Designate a different offset for each particular key

#### Time Complexity

Average: O(1)
Worst: O(n)


## Closed Addressing (Separate Chaining)

**Separate Chaining**: To keep pointers to Linked Lists as the keys in our Hash Table.

#### Time Complexity

Average: O(1)
Worst: O(n)

### Question

#### Consider a Hash Table with 100 slots. Collisions are resolved using Separate Chaining. Assuming that there is an equal probability of mapping to any index of the Hash Table, what is the probability that the first 3 slots (index 0, index 1, and index 2) are unfilled after the first 3 insertions? Enter your answer as a decimal (i.e., not a percentage) and round to the nearest thousandth.

0.97\*0.97\*0.97 = 0.913

#### What is the worst-case time complexity for \*find/insert\* in a hash table using Separate Chaining? Assume a **Linked-List** is used for the bucket implementation.

O(n), if all the keys mapped to the same index

#### What is the worst-case time complexity for find in a hash table using Separate Chaining? Assume an **AVL-tree** is used for the bucket implementation.

O(log(n)), 

#### What is the worst-case time complexity for \*insert\* in a hash table using Separate Chaining? Assume an **AVL-Tree** is used for the bucket implementation, and that the hash table may need to be resized after insertion.

O(nlog(n)), O(1) for finding the position of insertion, O(logn) to find the place for insetion in AVL tree, then supersede the load factor, create a new hash table with more slots, and rehash all the elements fell into the same bucket, to do a O(n) insertion. 

### Advantages and Disadvantages

#### Advatages

1. The average-case performance is considered much better than Linear Probing and Double Hashing as the amount of keys approaches, and even exceeds, M, the capacity of the Hash Table

2. We could never have exceeded M in Linear Probing or Double Hashing (not that we would want to in the first place) without having to resize the backing array and reinsert the elements from scratch.


#### Disadvantages

1. We require extra storage now for pointers (when storing primitive data types).

2. All the data in our Hash Table is no longer huddled near a single memory location (since pointers can point to memory anywhere), and as a result, this poor locality causes poor cache performance (i.e., it often takes the computer longer to find data that isn't located near previously accessed data)



# Lecture 15: Bloom Filters and Count-Min Sketches

## Bloom Filter

**Bloom filter**: Relies on a backing array structure to represent the stored elements. Instead of storing actual elements, the array simply stores boolean values, typically in the form of a bit array. The array is initialized with `m` bits, all set to false (or 0).$$

Bloom filter requires us to define k different hash functions, each mapping to any of the `m` bits uniformly. 

![img](https://i.imgur.com/XP6cAzK.png)

- Probabilitic data structure
- Memory-efficient
- No **false negatives**
- Can have **false positives**



## Designing an Optimal Bloom Filter

Probability of False Positive: 
$$
\epsilon=\left(1-\left(\frac{m-1}{m}\right)^{k n}\right)^{k} \approx\left(1-e^{-\frac{k n}{m}}\right)^{k}
$$
k = #hash functions.   m = #bits.    n = #insertions

- If m is sufficiently big, we could minimized the probability of False Positive



So, inorder to design an optimal Count-Min Sketch:

1. Guess roughly how many elements (*n*) the user will insert (we can over-estimate if we are unsure)

2. Pick a **FP** probability (*ε*) that we feel is appropriate (smaller = fewer **FPs** but more memory)

3. Determine the optimal number of hash functions: 
   $$
   k=-\log_2(\epsilon)
   $$

4. Determine the optimal size of the backing array: 
   $$
   m=-\frac{n\ln(\epsilon)}{\left(\ln(2)\right)^2}
   $$

## Count-Min Sketches	

**Count-Min Sketch** is essentially the same as a Bloom filter, but instead of storing an array of booleans, you store an array of counts (which are unsigned integers).

<img src="https://i.imgur.com/XdJbQ7q.png" style="zoom:50%;" />

**Count-Min Sketch** relies on a backing 2D array structure with `m` columns and `k` rows, with every cell initialized to 0, to represent the stored counts. Instead of defining a single hash function for the keys, a **Count-Min Sketch** requires us to define `k` different hash functions (one per row of our 2D array), each mapping to any of `m` cells of its row uniformly.

<img src="https://i.imgur.com/gMjfu5G.png" alt="img" style="zoom: 50%;" />

- Probabilitic data structure
- Memory-efficient
- Provides upper-bound on counts (go through the way, the minimum is the upper bound)

## Designing an Optimal Count-Min Sketch	

m = #columns.    k = #rows/hash functions

n = #elements.    Cx = true count of x.     ~Cx = estimated count of x

Let *ε* denote an additive factor and *δ* denote a probability such that (with probability `1-δ`)
$$
\hat{c}_x\le c_x+\epsilon n
$$


So, inorder to design an optimal Count-Min Sketch:

1. Determine the optimal number of columns, where *e* is Euler's number:
   $$
   m=\lceil\frac{e}{\epsilon}\rceil
   $$

2. Determine the optimal number of rows / hash functions: 
   $$
   k=\lceil\ln\left(\frac{1}{\delta}\right)\rceil
   $$

# Lecture 16: Aho-Corasick Algorithm


## Aho-Corasick Automaton	

- The Aho-Corasick Automaton takes advantage of the fact that, at any point during the trie traversal, the suffix of the path from the root to the current node could potentially also exist as a path starting at the root.

Build a **Multiway Trie**: A, AG, GAG, GC, GCA, C, and CAA.

<img src="https://imgur.com/B4JhvTL.png" style="zoom:50%;" />

### Failure Links

**Failure links**: edges that can be traversed if we try and fail to traverse down a non-existent child edge. Formally, for every node *u*, we can create a **failure link** from *u* to a node *v* such that the path from the root to node *v* is equivalent to the _**longest suffix**_ of the path from the root to node *u*.

Note that we do not include the full path from the root to *u* as a valid suffix (otherwise the **failure link** would always just point to *u*), and we include the 0-edge path as a valid suffix (meaning, in the worst case, *u* will have a **failure link** to the root).

1) 沿father的fail，找到temp

2) 看temp的后继是否有和child一样的，有则指向后继

3) 若无，则沿temp的fail继续行走，重复2，直到root，若root也无，则指向root

<img src="https://i.imgur.com/rvJs2a1.png" style="zoom:50%;" />

### Dictionary Links

Current data structure may miss instances of words that appear as substrings of other words in our database.

**Dictionary Links**: for each node *u*, draw a link to the _**first word node**_  you would encounter if you were to traverse **failure links** as far as you can. 



<img src="https://i.imgur.com/nzUwaco.png" style="zoom:50%;" />



```python
scan(query):
    curr = root
    for each letter c in query:
        while curr does not have a child edge labeled by c:
            if curr == root:
                go to the next iteration of the for-loop (c = next letter in query)
            else:
                curr = follow failure link from curr
        curr = follow curr's child edge labeled by c
        if curr has a dictionary link:
            output all words represented by nodes in the chain of dictionary links
        if curr is a word node:
            output curr's word
```

### Question

#### Build Aho-Corasick automation

You’re inserting N distinct strings, all of the same length K into an Aho-Corasick automaton.

Given only the information above, which of the following can you deduce about the resulting automaton?  Select all that apply.

- The number of nodes in the automaton

- The number of failure links in the automaton

- The number of dictionary links in the automaton

- The memory (in bytes) occupied by the automaton

- The number of leaf nodes in the automaton

- The height of the automaton

- None of the above

Ans: CEF, they're all the same length, but all different words a definitely. They definitely do not have any words as sub strings of other words. So I have zero dictionary links.



# Lecture 17: Suffix Array

## Suffix Arrays

- Sort all (non-empty) suffixes of the database string in ascending alphabetical order, and we will be able to search for query strings via binary search. 

Worst-case space complexity to store all sorted suffixes of a string of length n: O(n^2)



### Example

With a database string *D* = GCATCGC, we had the following (unsorted) suffixes:

<img src="https://imgur.com/9SbSaWS.png" style="zoom:50%;" />

Given that we have *D* in memory, we can instead represent our (unsorted) suffixes as the following array:

<img src="https://imgur.com/SMKy8XE.png" style="zoom: 33%;" />

We can then sort this array of integers using a custom comparator where, when we want to compare numbers *i* and *j*, we will return the result of comparing the suffixes of *D* starting at indices *i* and *j*, respectively. In this specific example, this custom sort will yield the following array:

<img src="https://imgur.com/4qXywYf.png" style="zoom:33%;" />



### Time Complexity

Worst case time complexity to build: **O(n² logn)**.

Worst-case time complexity to find all occurences: **O(klogn)**



# Lecture 18: Burrows-Wheeler Transform

## Burrows Wheeler Transform (BWT)  

1. Add an end-of-string symbol `$` that does not exist in our alphabet to the end of the string.

   ​														BANANA$

2. Construct the "Burrows-Wheeler Matrix, which is simply all rotations of our string (including the end-of-string symbol).

<img src="https://imgur.com/6R0F4QT.png" style="zoom:50%;" />

3. Sort the rotations in our Burrows-Wheeler Matrix in ascending alphabetical order (we assume our end-of-string symbol is the smallest character in alphabetical order).

<img src="https://imgur.com/YaLjl4I.png" style="zoom:50%;" />

4. The last column of the sorted Burrows-Wheeler Matrix (emphasized in bold) is our **Burrows-Wheeler Transform**

   ​														ANNB$AA

## Inverting the BWT

1. We know the last column of Burrows-Wheeler Matrix 

<img src="https://imgur.com/j5cmnRr.png" style="zoom:50%;" />

2. The first column is simply the result of sorting our **BWT** alphabetically

<img src="https://imgur.com/7ZmagVs.png" style="zoom:50%;" />

3. Construct the original string by order

<img src="https://imgur.com/xn7C6BO.png" style="zoom: 50%;" />

### Complexity

Worst-case time complexity for reconstruction: O(n)

Worst-case time complexity for find all occurrences of a query string *w* of length *k*: O(k)

Construction space complexity: O(n)



## Pattern Matching Using the BWT

<img src="https://imgur.com/6dp7fcK.png" style="zoom:50%;" />

Find Algorithm:

```java
find(w):
    top = 0
    bottom = n-1
    for each character c in w in reverse order:
        if c does not exist in the range Last[top,bottom]:
            return null // w does not exist
        i = first occurrence of c in the range Last[top,bottom]
        j = last occurrence of c in the range Last[top,bottom]
        top = L2F[i]
        bottom = L2F[j]
    return all positions in original string corresponding to First[top,bottom]
```

# Lecture 19: Coding Trees and Entropy

## Information vs. Data	

- Information: Content of some message, tell us detail(s) about some system(s)

- Data: Raw unit of information, representation (or encoding) of information

## Entropy

- Entropy: Mesaure of disorder (non-uniformity) of a system
- Shannon Entropy: Expected value (average) of the information contained in some data

# Lecture 20: Huffman Coding

## Prefix Codes

- Prefix Codes: An encoding in which no symbol is represented by a code that is a prefix of the code representing another symbol

<img src="https://imgur.com/J7uDhYY.png" style="zoom:50%;" />

>  Letter located at the leaves

## Huffman Coding

We have a set of *n* possible items and we want to represent them uniquely. We could construct a **balanced binary tree** of height ⌈log₂(*n*)⌉

#### Which of the following statements about Huffman compression are true?

A header must be added to the compressed file to provide enough information so that the recipient can reconstruct the same coding tree that was used to encode the file

The Huffman algorithm always generates a balanced binary tree to ensure ⌈log₂(n)⌉ symbol encoding length

The Huffman algorithm takes into account symbol frequencies when deciding how to encode symbols

Ans: AC

## Huffman Tree Construction

1. Compute the frequencies of all symbols that appear in the input
2. Start with a "forest" of single-node trees, one for each symbol that appeared in the input (ignore symbols with count 0, since they don't appear at all in the input)
3. While there is more than 1 tree in the forest:
   1. Remove the two trees (T1 and T2) from the forest that have the lowest count contained in their roots
   2. Create a new node that will be the root of a new tree. This new tree will have T1 and T2 as left and right subtrees. The count in the root of this new tree will be the sum of the counts in the roots of T1 and T2. Label the edge from this new root to T1 as "1" and label the edge from this new root to T2 as "0"
   3. Insert this new tree in the forest, and go back to the While statement
4. Return the one tree in the forest as the Huffman tree



Message: AAAAABBAHHBCBGCCC

<img src="https://imgur.com/iUZR20m.png" style="zoom:50%;" />



## Huffman Tree Message Encoding

For each symbol in the message, output the sequence of bits given by 1's and 0's on the path from the root of the tree to that symbol. 

## Huffman Tree Message Decoding

1. Start with the first bit in the coded message, and start with the root of the code tree

2. As you read each bit, move to the left or right child of the current node, matching the bit just read with the label on the edge

3. When you reach a leaf, output the symbol stored in the leaf, return to the root, and continue



#  Lecture 21: Bitwise Input/Output (I/O)

## Bytewise I/0

The smallest unit of data that can be written to disk is a *byte*, which is a chunk of 8 *bits*.

In most languages, we can create an "output stream" that handles filling the buffer, writing to disk, etc. for us on its own. Below is a typical workflow of **writing** some *bytewise* data from **memory** to **disk**,

The basic workflow for **writing** *bytes* to disk is as follows:

- Write bytes to buffer, one byte at a time
- Once the buffer is full, write the entire buffer to disk and clear the buffer (i.e., "flush" the buffer)
- Repeat

Like with writing from disk, in most languages, one can create an "input stream" that handles reading from disk, filling the buffer, etc. Below is a typical workflow of **reading** some *bytewise* data from **disk** to **memory**:

<img src="https://imgur.com/FjvDJUh.png" style="zoom:50%;" />

## Bitwise I/O

The process of reading and writing data to and from disk *bit*-wise (as opposed to traditional I/O, which is *byte*-wise)

The basic workflow for **writing** *bits* to disk is as follows:

- Write bits to bitwise buffer, one bit at a time
- Once the bitwise buffer is full, write the bitwise buffer (which is 1 byte) to the bytewise buffer and clear the bitwise buffer (i.e., "flush" the bitwise buffer)
- Repeat until the bytewise buffer is full
- Once the bytewise buffer is full, write the entire bytewise buffer to disk and clear the bytewise buffer (i.e., "flush" the bytewise buffer)
- Repeat from the beginning

<img src="https://imgur.com/BbT1OmT.png" style="zoom:50%;" />



## Reading from a Bitwise Buffer





## Writing to a Bitwise Buffer



## Question

### Bitwise operations

Consider this method:

```
// Returns true if the nth bit is set to 1, false otherwise.
// Count from the most significant bit,
// so 0xF0 returns true for N=0 and false for N=7
bool getNthBit(unsigned char c, unsigned char N) {
  return ???
}
```

Which expression(s) correctly fill the `???`? Remember that true is any nonzero value.

(c >> (7 - N)) & 1;
(c >> (7 - N)) == 1;
(c & (7 - N)) >> 1;
(c == (7 - N)) >> 1;
c & (1 << (7 - N));
c & (1 << N);
None of the above

Ans: AE

Which of the following input(s) demonstrates that ALL the wrong answers above actually produce the wrong answer? (That is, it would return the wrong result for all of the incorrect options above).

c = 0x01, N = 0
c = 0xF0, N = 0
c = 0xF0, N = 3
c = 0xF0, N = 4
None of the above

Ans: C

<font color=red>need to find the explaination. </font>



# Lecture 22: Graphs and Graph Representation 

## Graphs

Formally, a graph consists of the following:

- A set of elements called **nodes** (or **vertices**)
- A set of connections between pairs of nodes called **edges**

**Graph**: Collection of nodes and edges

**Node**(aka Vertex): A single entity

**Edge**: A relationship between a pair of nodes

### Directed vs. Undirected

**Directed**: An edge (u,v) is from u to v, not v to u

**Undirected**: An edge (u,v0 is from u to v and v to u

### Weighted vs. Unweighted

**Weighted**: Each edge has a "weight" ("cost") associated with it

**Unweighted**: Edges do not have weights

### Cycles

**Cycle**: A valid path starting and ending at the same node

### Classes of Graphs

**Unstructed**: A disconnected collection of nodes

**Sequential**: An ordered collection of connected nodes

**Hierachical**: A ranked collection of connected nodes

**Structured**: A collection of both connected and disconnected nodes

**Multigraph**: Graph in which a pair of nodes may have multiple distinct edges

## Graph Representation

### Adjacency matrix

<img src="https://imgur.com/AF6RX6M.png" style="zoom:50%;" />

- Space complexity: O(|V|^2)

### Adjacency list

<img src="https://imgur.com/M9YGcEE.png" style="zoom:50%;" />

- Space complexity: O(|V|+|E|)
- Not ideal for **dense** graphs.

# Lecture 23: Breadth First Search (BFS) and Depth First Search (DFS)

## Breadth First Search

1. Add (0, start) to queue
2. While the queue is not empty:
   1. Pop (d, curr) from the queue 
   2. If curr has not been visited:
      1. Mark curr as visited with distance d
      2. For all edges (curr, w):
         1. If w has not been visited, add (d+1,w) to queue

```python
BFSShortestPath(u,v):
    q = an empty queue
    add (0,u) to q // (0,u) -> (length from u, current vertex)
    while q is not empty:
        (length,curr) = q.dequeue()
        mark curr as visited
        if curr == v: // if we have reached the vertex we are searching for
            return length
        for all outgoing edges (curr,w) from curr: // otherwise explore all neighbors
            if w has not yet been visited:
                add (length+1,w) to q
    return "FAIL" // if I reach this point, then no path exists from u to v
```

- Worst-case time complexity: O(|V|+|E|)

## Depth First Search

1. Add start to stack
2. While the stack is not empty:
   1. Pop curr from the stack
   2. If curr has not been visited
      1. Mark curr as visited 
      2. For all edges (curr, w):
         1. If w has not been visited, add w to stack

```python
DFS(u,v):
    s = an empty stack
    push (0,u) to s // (0,u) -> (length from u, current vertex)
    while s is not empty:
        (length,curr) = s.pop()
        if curr == v: // if we have reached the vertex we are searching for
            return length
        for all outgoing edges (curr,w) from curr: // otherwise explore all neighbors
            if w has not yet been visited:
                add (length+1,w) to s
    return "FAIL" // if I reach this point, then no path exists from u to v
```

```python
DFSRecursion(s): // s is the starting vertex
    mark s as explored 
    for each unexplored neighbor v of s:
        DFSRecursion(v) 
```

Worst-case time complexity: O(|V|+|E|)
