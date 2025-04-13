# 🌳 Tree Data Structure – Overview

The **Tree** is a non-linear hierarchical data structure made up of nodes connected by edges. It is widely used in various applications such as databases, compilers, operating systems, and artificial intelligence.

---

## 📌 Basic Terminologies

- **Node**: Each element in the tree.
- **Root**: The topmost node in the tree.
- **Parent**: A node that has children.
- **Child**: A node that descends from another node.
- **Leaf**: A node with no children.
- **Edge**: Connection between one node and another.
- **Height of Tree**: Number of edges on the longest path from the root to a leaf.
- **Depth of Node**: Number of edges from the root to the node.
- **Subtree**: A tree formed from a node and its descendants.
- **Level**: Root is at level 0, its children at level 1, and so on.

---

## 🌲 Why Use Trees?

- Represent hierarchical relationships.
- Fast search, insert, delete (especially in BSTs and Heaps).
- Organize data (file systems, XML parsers).
- Efficient indexing (B-Trees in databases).

---

## 🧠 Real-World Applications

- **File System Management** (Hierarchical structure)
- **Database Indexing** (B-Trees, B+ Trees)
- **Routing Tables in Networks**
- **AI Decision Trees**
- **Compiler Syntax Trees**
- **Autocomplete and Spell Checker** (Trie)

---

## 📁 Types of Trees (Summary)

| Tree Type             | Description                                              | Usage Example                         |
|----------------------|----------------------------------------------------------|----------------------------------------|
| General Tree          | Node can have any number of children                     | Organization chart                     |
| Binary Tree           | Each node has at most two children                       | Base for many tree types               |
| Binary Search Tree    | Left < Root < Right                                      | Fast lookup, insertion, deletion       |
| AVL Tree              | Self-balancing BST with height check                     | Search operations                      |
| Red-Black Tree        | Self-balancing BST using color rules                     | STL `map`, `set` in C++                |
| N-ary Tree            | Node can have up to N children                           | XML/HTML DOM structure                 |
| Trie (Prefix Tree)    | Stores words character by character                      | Dictionary search, autocomplete        |
| Segment Tree          | Stores intervals and supports efficient range queries    | Range queries on arrays                |
| Fenwick Tree (BIT)    | Supports prefix sum and update efficiently               | Competitive programming                |
| Heap (Min/Max)        | Complete binary tree following heap property             | Priority queues, heapsort              |
| B-Tree                | Balanced M-way tree for sorted data                      | Databases, file systems                |
| B+ Tree               | Variant of B-tree where data stored in leaf nodes only   | Database indexing                      |

---

## ⏭️ Next Step

👉 [Start with Binary Trees (Structure + Representation)](./Binary_Tree.md)

# 🌲 Binary Tree – Detailed Guide

A **Binary Tree** is a hierarchical tree data structure in which each node has at most **two children** referred to as the **left** and **right** child.

---

## 📌 Properties of Binary Tree

- **Maximum Nodes at level `l`**: `2^l`
- **Maximum Nodes in a tree of height `h`**: `2^(h+1) - 1`
- **Minimum possible height for `n` nodes**: `ceil(log2(n+1)) - 1`

---

- `A` is the root
- `B` and `C` are children of `A`
- `D` and `E` are children of `B`

---

## 🧑‍💻 Binary Tree Representation

### 1. **Using Nodes and Pointers (Linked Representation)**

```java
class Node {
    int data;
    Node left, right;
    
    Node(int value) {
        data = value;
        left = right = null;
    }
}
```
---
## 🌳 Types of Binary Trees

| Type                | Description                                                |
|---------------------|------------------------------------------------------------|
| **Full Binary Tree**     | Each node has 0 or 2 children                              |
| **Perfect Binary Tree**  | All internal nodes have 2 children & all leaves are at the same level |
| **Complete Binary Tree** | All levels filled, except the last (filled left to right)  |
| **Skewed Binary Tree**   | All nodes have only one child                              |
| - Left Skewed       | All nodes have only left child                             |
| - Right Skewed      | All nodes have only right child                            |


