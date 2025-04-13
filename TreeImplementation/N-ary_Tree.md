# 🌳 N-ary Tree in Java

## 📖 Definition

An **N-ary Tree** is a tree data structure where each node can have **at most N children**, unlike a binary tree (which allows only 2 children per node).

### Examples:
- A ternary tree is a 3-ary tree.
- A general tree is often modeled as an N-ary tree without a fixed limit on children.

---

## 🔧 Core Methods

| Method            | Description                                  |
|-------------------|----------------------------------------------|
| `addChild()`      | Add a child node to a given parent           |
| `traverse()`      | Traverse the tree (Preorder or Postorder)   |
| `find()`          | Find a node with a specific value            |
| `printTree()`     | Visualize the tree structure                 |

---

## 💻 Java Code Implementation

```java
import java.util.*;

class NaryNode {
    int val;
    List<NaryNode> children;

    public NaryNode(int val) {
        this.val = val;
        this.children = new ArrayList<>();
    }

    public void addChild(NaryNode child) {
        children.add(child);
    }
}

public class NaryTree {
    NaryNode root;

    public NaryTree(int rootVal) {
        root = new NaryNode(rootVal);
    }

    public void printPreorder(NaryNode node) {
        if (node == null) return;

        System.out.print(node.val + " ");
        for (NaryNode child : node.children) {
            printPreorder(child);
        }
    }

    public void printPostorder(NaryNode node) {
        if (node == null) return;

        for (NaryNode child : node.children) {
            printPostorder(child);
        }
        System.out.print(node.val + " ");
    }

    public boolean find(NaryNode node, int target) {
        if (node == null) return false;
        if (node.val == target) return true;

        for (NaryNode child : node.children) {
            if (find(child, target)) return true;
        }
        return false;
    }

    public void printTree(NaryNode node, String indent) {
        if (node == null) return;

        System.out.println(indent + node.val);
        for (NaryNode child : node.children) {
            printTree(child, indent + "  ");
        }
    }
}
public class Main {
    public static void main(String[] args) {
        NaryTree tree = new NaryTree(1);
        NaryNode root = tree.root;

        NaryNode child1 = new NaryNode(2);
        NaryNode child2 = new NaryNode(3);
        NaryNode child3 = new NaryNode(4);

        root.addChild(child1);
        root.addChild(child2);
        root.addChild(child3);

        child1.addChild(new NaryNode(5));
        child1.addChild(new NaryNode(6));
        child3.addChild(new NaryNode(7));

        System.out.println("Preorder:");
        tree.printPreorder(root); // Output: 1 2 5 6 3 4 7

        System.out.println("\n\nPostorder:");
        tree.printPostorder(root); // Output: 5 6 2 3 7 4 1

        System.out.println("\n\nTree Structure:");
        tree.printTree(root, "");
    }
}

```
## Interview Tips
- N-ary trees are useful when data naturally has variable number of children (e.g. DOM Trees, File Systems).
- Watch out for recursive DFS or BFS implementation for N-ary trees (common Leetcode patterns).
- Preorder and Postorder traversals are key — and often tested in interviews.
- Avoid confusion with Binary Trees — each node has a **list** of children, not just left and right.
- Common Problems:
  - Serialize and Deserialize N-ary tree
  - Level order traversal using Queue
  - Maximum depth of N-ary tree
