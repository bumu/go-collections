# go-collections

[![Go Report Card](https://goreportcard.com/badge/github.com/idsulik/go-collections)](https://goreportcard.com/report/github.com/idsulik/go-collections)
![Build Status](https://img.shields.io/github/actions/workflow/status/idsulik/go-collections/go.yaml?branch=main)
[![Version](https://img.shields.io/github/v/release/idsulik/go-collections)](https://github.com/idsulik/go-collections/releases)
[![License](https://img.shields.io/github/license/idsulik/go-collections)](https://github.com/idsulik/go-collections/blob/main/LICENSE)
[![GoDoc](https://pkg.go.dev/badge/github.com/idsulik/go-collections)](https://pkg.go.dev/github.com/idsulik/go-collections)

`go-collections` is a Go package that provides implementations of common data structures, including a double-ended queue (Deque), various stack implementations, a linked list, a queue, a trie, a priority queue, a binary search tree, a skip list, and a graph. This package offers a simple and efficient way to use these structures in Go, with support for generic types.

## Table of Contents

1. [Installation](#installation)
2. [Usage](#usage)
3. [Data Structures](#data-structures)
   - [Set](#set)
   - [Deque](#deque)
   - [LinkedList](#linkedlist)
   - [Queue](#queue)
   - [Stack Interface](#stack-interface)
   - [ArrayStack](#arraystack)
   - [LinkedListStack](#linkedliststack)
   - [Trie](#trie)
   - [Priority Queue](#priority-queue)
   - [Binary Search Tree](#binary-search-tree)
   - [Skip List](#skip-list)
   - [Graph](#graph)
   - [BloomFilter](#bloom-filter)
4. [License](#license)

## [Installation](#installation)

You can install the package using the Go module system:

```sh
go get github.com/idsulik/go-collections
```

## [Usage](#usage)

Here is a brief example of how to use the `Deque`:

```go
package main

import (
  "fmt"
  "github.com/idsulik/go-collections/deque"
)

func main() {
  d := deque.New[int](0)
  d.PushBack(1)
  d.PushFront(2)

  front, _ := d.PopFront()
  back, _ := d.PopBack()

  fmt.Println(front) // Output: 2
  fmt.Println(back)  // Output: 1
}
```

## [Data Structures](#data-structures)

### [Set](#set)

A set represents a collection of unique items.

#### Type `Set[T comparable]`

- **Constructor:**

  ```go
  func New[T comparable]() *Set[T]
  ```

- **Methods:**

  - `Add(item T)`: Adds an item to the set.
  - `Remove(item T)`: Removes an item from the set.
  - `Has(item T) bool`: Returns `true` if the set contains the specified item.
  - `Clear()`: Removes all items from the set.
  - `Len() int`: Returns the number of items in the set.
  - `IsEmpty() bool`: Returns `true` if the set is empty.
  - `Elements() []T`: Returns a slice containing all items in the set.
  - `AddAll(items ...T)`: Adds multiple items to the set.
  - `RemoveAll(items ...T)`: Removes multiple items from the set.
  - `Diff(other *Set[T]) *Set[T]`: Returns a new set containing items that are in the receiver set but not in the other set.
  - `Intersect(other *Set[T]) *Set[T]`: Returns a new set containing items that are in both the receiver set and the other set.
  - `Union(other *Set[T]) *Set[T]`: Returns a new set containing items that are in either the receiver set or the other set.
  - `IsSubset(other *Set[T]) bool`: Returns `true` if the receiver set is a subset of the other set.
  - `IsSuperset(other *Set[T]) bool`: Returns `true` if the receiver set is a superset of the other set.
  - `Equal(other *Set[T]) bool`: Returns `true` if the receiver set is equal to the other set.

---

### [Deque](#deque)

A double-ended queue (Deque) allows adding and removing elements from both the front and the back.

#### Type `Deque[T any]`

- **Constructor:**

  ```go
  func New[T any](initialCapacity int) *Deque[T]
  ```

- **Methods:**

  - `PushFront(item T)`: Adds an item to the front of the deque.
  - `PushBack(item T)`: Adds an item to the back of the deque.
  - `PopFront() (T, bool)`: Removes and returns the item at the front of the deque.
  - `PopBack() (T, bool)`: Removes and returns the item at the back of the deque.
  - `PeekFront() (T, bool)`: Returns the item at the front of the deque without removing it.
  - `PeekBack() (T, bool)`: Returns the item at the back of the deque without removing it.
  - `Len() int`: Returns the number of items in the deque.
  - `IsEmpty() bool`: Checks if the deque is empty.
  - `Clear()`: Removes all items from the deque.

---

### [LinkedList](#linkedlist)

A singly linked list where elements can be added or removed from both the front and the end.

#### Type `LinkedList[T any]`

- **Constructor:**

  ```go
  func New[T any]() *LinkedList[T]
  ```

- **Methods:**

  - `AddFront(value T)`: Adds a new node with the given value to the front of the list.
  - `AddBack(value T)`: Adds a new node with the given value to the end of the list.
  - `PeekFront() (T, bool)`: Returns the value of the node at the front without removing it.
  - `PeekBack() (T, bool)`: Returns the value of the node at the end without removing it.
  - `RemoveFront() (T, bool)`: Removes the node from the front and returns its value.
  - `RemoveBack() (T, bool)`: Removes the node from the end and returns its value.
  - `Iterate(fn func(T) bool)`: Iterates over the list and applies a function to each node's value until the function returns false or the end is reached.
  - `IsEmpty() bool`: Checks if the list is empty.
  - `Size() int`: Returns the number of elements in the list.
  - `Clear()`: Removes all elements from the list.

---

### [Queue](#queue)

A FIFO (first-in, first-out) queue that supports basic queue operations.

#### Type `Queue[T any]`

- **Constructor:**

  ```go
  func New[T any](initialCapacity int) *Queue[T]
  ```

- **Methods:**

  - `Enqueue(item T)`: Adds an item to the end of the queue.
  - `Dequeue() (T, bool)`: Removes and returns the item at the front of the queue.
  - `Peek() (T, bool)`: Returns the item at the front of the queue without removing it.
  - `Len() int`: Returns the number of items currently in the queue.
  - `IsEmpty() bool`: Checks if the queue is empty.
  - `Clear()`: Removes all items from the queue.

---

### [Stack Interface](#stack-interface)

An interface representing a LIFO (last-in, first-out) stack.

#### Type `Stack[T any]`

- **Methods:**

  - `Push(item T)`: Adds an item to the top of the stack.
  - `Pop() (T, bool)`: Removes and returns the item from the top of the stack.
  - `Peek() (T, bool)`: Returns the item at the top without removing it.
  - `Len() int`: Returns the number of items in the stack.
  - `IsEmpty() bool`: Checks if the stack is empty.
  - `Clear()`: Removes all items from the stack.

---

### [ArrayStack](#arraystack)

An array-based stack implementation using a slice.

#### Type `ArrayStack[T any]`

- **Constructor:**

  ```go
  func New[T any](initialCapacity int) *ArrayStack[T]
  ```

- **Implements:** `Stack[T]`

- **Methods:**

  - `Push(item T)`: Adds an item to the top of the stack.
  - `Pop() (T, bool)`: Removes and returns the item from the top.
  - `Peek() (T, bool)`: Returns the item at the top without removing it.
  - `Len() int`: Returns the number of items currently in the stack.
  - `IsEmpty() bool`: Checks if the stack is empty.
  - `Clear()`: Removes all items, leaving the stack empty.

---

### [LinkedListStack](#linkedliststack)

A linked list-based stack implementation.

#### Type `LinkedListStack[T any]`

- **Constructor:**

  ```go
  func New[T any]() *LinkedListStack[T]
  ```

- **Implements:** `Stack[T]`

- **Methods:**

  - `Push(item T)`: Adds an item to the top of the stack.
  - `Pop() (T, bool)`: Removes and returns the item from the top.
  - `Peek() (T, bool)`: Returns the item at the top without removing it.
  - `Len() int`: Returns the number of items currently in the stack.
  - `IsEmpty() bool`: Checks if the stack is empty.
  - `Clear()`: Removes all items from the stack.

---

### [Trie](#trie)

A Trie (prefix tree) data structure that supports insertion and search operations for words and prefixes.

#### Type `Trie`

- **Constructor:**

  ```go
  func New() *Trie
  ```

- **Methods:**

  - `Insert(word string)`: Adds a word to the Trie.
  - `Search(word string) bool`: Checks if the word exists in the Trie.
  - `StartsWith(prefix string) bool`: Checks if there is any word in the Trie that starts with the given prefix.

---

### [Priority Queue](#priorityqueue)

A priority queue allows for efficient retrieval and removal of the highest (or lowest) priority element. It's commonly used in algorithms like Dijkstra's shortest path and task scheduling.

#### Type `PriorityQueue[T any]`

- **Constructor:**

  ```go
  func New[T any](less func(a, b T) bool) *PriorityQueue[T]
  ```

  - `less`: A comparison function that determines the priority of elements. If `less(a, b)` returns `true`, then `a` has higher priority than `b`.

- **Methods:**

  - `Push(item T)`: Adds an item to the priority queue.
  - `Pop() (T, bool)`: Removes and returns the highest priority item.
  - `Peek() (T, bool)`: Returns the highest priority item without removing it.
  - `Len() int`: Returns the number of items in the priority queue.
  - `IsEmpty() bool`: Checks if the priority queue is empty.
  - `Clear()`: Removes all items from the priority queue.

---

### [Binary Search Tree](#binarysearchtree)

A Binary Search Tree (BST) maintains elements in sorted order, allowing for efficient insertion, deletion, and lookup operations. Each node has at most two children, with left child values less than the parent and right child values greater.

#### Type `BST[T Ordered]`

- **Constructor:**

  ```go
  func New[T Ordered]() *BST[T]
  ```

  - `T Ordered`: A type constraint that ensures the elements can be compared using `<` and `>` operators. Supported types include integers, floats, and strings.

- **Methods:**

  - `Insert(value T)`: Inserts a value into the BST.
  - `Remove(value T)`: Removes a value from the BST.
  - `Contains(value T) bool`: Checks if a value exists in the BST.
  - `InOrderTraversal(fn func(T))`: Traverses the BST in order and applies a function to each node's value.
  - `Len() int`: Returns the number of nodes in the BST.
  - `IsEmpty() bool`: Checks if the BST is empty.
  - `Clear()`: Removes all nodes from the BST.

---

### [Skip List](#skiplist)

A Skip List is a probabilistic data structure that allows fast search, insertion, and deletion operations within an ordered sequence of elements. It achieves efficiency by maintaining multiple levels of linked lists, where each higher level skips over a larger number of elements, allowing operations to be performed in O(log n) average time.

#### Type `SkipList[T Ordered]`

- **Constructor:**

  ```go
  func New[T Ordered](maxLevel int, p float64) *SkipList[T]
  ```

  - `maxLevel`: The maximum level of the skip list (controls the space vs. time trade-off).
  - `p`: The probability factor used to determine the level of new nodes (usually set to 0.5).

- **Methods:**

  - `Insert(value T)`: Inserts a value into the skip list.
  - `Delete(value T)`: Deletes a value from the skip list.
  - `Search(value T) bool`: Searches for a value in the skip list.
  - `Len() int`: Returns the number of elements in the skip list.
  - `IsEmpty() bool`: Checks if the skip list is empty.
  - `Clear()`: Removes all elements from the skip list.

---
### [Graph](#graph)

Represents networks of nodes and edges, suitable for various algorithms like search, shortest path, and spanning trees.

#### Type `Graph[T comparable]`

- **Constructor:**

  ```go
  func New[T comparable](directed bool) *Graph[T]
  ```

  - `directed`: Specifies whether the graph is directed or undirected.

- **Methods:**

  - `AddNode(value T)`: Adds a node to the graph.
  - `AddEdge(from, to T, weight float64)`: Adds an edge between two nodes with an optional weight.
  - `RemoveNode(value T)`: Removes a node and all connected edges.
  - `RemoveEdge(from, to T)`: Removes an edge between two nodes.
  - `Neighbors(value T) []T`: Returns adjacent nodes.
  - `HasNode(value T) bool`: Checks if a node exists.
  - `HasEdge(from, to T) bool`: Checks if an edge exists.
  - `GetEdgeWeight(from, to T) (float64, bool)`: Retrieves the weight of the edge between two nodes.
  - `Traverse(start T, visit func(T))`: Traverses the graph from a starting node using Breadth-First Search.
  - `Nodes() []T`: Returns a slice of all node values in the graph.
  - `Edges() [][2]T`: Returns a slice of all edges in the graph.

---
### [Bloom Filter](#bloom-filter)

A Bloom Filter is a space-efficient probabilistic data structure used to test whether an element is a member of a set. False positive matches are possible, but false negatives are not. Elements can be added to the set, but not removed.

#### Type `BloomFilter[T any]`

- **Constructor:**

  ```go
  func NewBloomFilter[T any](expectedItems uint, falsePositiveProb float64) *BloomFilter[T]
  ```

    - `expectedItems`: Expected number of items to be added to the filter
    - `falsePositiveProb`: Desired false positive probability (between 0 and 1)

- **Methods:**

    - `Add(item T)`: Adds an item to the Bloom Filter.
    - `Contains(item T) bool`: Tests whether an item might be in the set.
    - `EstimatedFalsePositiveRate() float64`: Returns the current estimated false positive rate.
    - `Clear()`: Removes all items from the Bloom Filter.
    - `Len() int`: Returns the number of items added to the Bloom Filter.
    - `IsEmpty() bool`: Returns true if no items have been added.
    - `BitSize() uint`: Returns the size of the underlying bit array.
    - `NumberOfHashes() uint`: Returns the number of hash functions being used.

#### Example Usage:

```go
// Create a new Bloom Filter expecting 1000 items with 1% false positive rate
bf := collections.NewBloomFilter[string](1000, 0.01)

// Add some items
bf.Add("apple")
bf.Add("banana")
bf.Add("cherry")

// Check for membership
if bf.Contains("apple") {
    fmt.Println("'apple' is probably in the set")
}

// Get current false positive rate
fmt.Printf("False positive rate: %f\n", bf.EstimatedFalsePositiveRate())

// Clear the filter
bf.Clear()
```

#### Performance Characteristics:

- Space Complexity: O(m), where m is the size of the bit array
- Time Complexity:
    - Add: O(k), where k is the number of hash functions
    - Contains: O(k), where k is the number of hash functions
- False Positive Probability: (1 - e^(-kn/m))^k
    - k: number of hash functions
    - n: number of inserted elements
    - m: size of bit array

#### Use Cases:

- Duplicate detection
- Cache filtering
- URL shorteners
- Spell checkers
- Network routing
- Database query optimization

#### Notes:

- The Bloom Filter automatically optimizes the number of hash functions and bit array size based on the expected number of items and desired false positive rate.
- The actual false positive rate may vary slightly from the target rate due to the probabilistic nature of the data structure.
- The filter supports any type that can be converted to a string representation.

## [License](#license)
This project is licensed under the [MIT License](LICENSE) - see the [LICENSE](LICENSE) file for details.
