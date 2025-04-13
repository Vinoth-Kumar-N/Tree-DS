# 🌳 Binary Tree

A **Binary Tree** is a hierarchical data structure in which each node has at most **two children**, referred to as the **left child** and **right child**.

---

## 🔧 Methods (Operations)

- **Insertion** – Add a new node in the binary tree (usually level-order).
- **Traversal** – Visit all nodes (Inorder, Preorder, Postorder, Level Order).
- **Search** – Find if a value exists in the tree.
- **Height** – Determine the longest path from root to a leaf.
- **Count Nodes / Leaves** – Count all nodes or only leaf nodes.
- **Delete Tree** – Remove all nodes from the tree.

---

## 🧑‍💻 Java Code Implementation (With Comments)

```java
import java.util.*;

// Node structure for Binary Tree
class Node {
    int data;
    Node left, right;

    Node(int item) {
        data = item;
        left = right = null;
    }
}

public class BinaryTree {
    Node root;

    // Level Order Insertion (BFS)
    public void insert(int key) {
        Node newNode = new Node(key);
        if (root == null) {
            root = newNode;
            return;
        }

        Queue<Node> q = new LinkedList<>();
        q.add(root);

        while (!q.isEmpty()) {
            Node temp = q.poll();

            if (temp.left == null) {
                temp.left = newNode;
                break;
            } else {
                q.add(temp.left);
            }

            if (temp.right == null) {
                temp.right = newNode;
                break;
            } else {
                q.add(temp.right);
            }
        }
    }

    // Inorder Traversal (Left → Root → Right)
    public void inorder(Node node) {
        if (node == null) return;
        inorder(node.left);
        System.out.print(node.data + " ");
        inorder(node.right);
    }

    // Preorder Traversal (Root → Left → Right)
    public void preorder(Node node) {
        if (node == null) return;
        System.out.print(node.data + " ");
        preorder(node.left);
        preorder(node.right);
    }

    // Postorder Traversal (Left → Right → Root)
    public void postorder(Node node) {
        if (node == null) return;
        postorder(node.left);
        postorder(node.right);
        System.out.print(node.data + " ");
    }

    // Level Order Traversal (BFS)
    public void levelOrder(Node node) {
        if (node == null) return;

        Queue<Node> q = new LinkedList<>();
        q.add(node);

        while (!q.isEmpty()) {
            Node temp = q.poll();
            System.out.print(temp.data + " ");

            if (temp.left != null) q.add(temp.left);
            if (temp.right != null) q.add(temp.right);
        }
    }

    // Search for a key
    public boolean search(Node node, int key) {
        if (node == null) return false;
        if (node.data == key) return true;

        return search(node.left, key) || search(node.right, key);
    }

    // Height of the tree
    public int height(Node node) {
        if (node == null) return 0;
        return 1 + Math.max(height(node.left), height(node.right));
    }

    // Count total number of nodes
    public int countNodes(Node node) {
        if (node == null) return 0;
        return 1 + countNodes(node.left) + countNodes(node.right);
    }

    // Count total number of leaf nodes
    public int countLeaves(Node node) {
        if (node == null) return 0;
        if (node.left == null && node.right == null) return 1;
        return countLeaves(node.left) + countLeaves(node.right);
    }

    // Delete the entire tree
    public void deleteTree() {
        root = null;
        System.out.println("Binary Tree deleted.");
    }

    // Main method to test
    public static void main(String[] args) {
        BinaryTree tree = new BinaryTree();
        tree.insert(10);
        tree.insert(20);
        tree.insert(30);
        tree.insert(40);
        tree.insert(50);

        System.out.print("Inorder: ");
        tree.inorder(tree.root);
        System.out.println();

        System.out.print("Preorder: ");
        tree.preorder(tree.root);
        System.out.println();

        System.out.print("Postorder: ");
        tree.postorder(tree.root);
        System.out.println();

        System.out.print("Level Order: ");
        tree.levelOrder(tree.root);
        System.out.println();

        System.out.println("Search 30: " + tree.search(tree.root, 30));
        System.out.println("Height: " + tree.height(tree.root));
        System.out.println("Total Nodes: " + tree.countNodes(tree.root));
        System.out.println("Leaf Nodes: " + tree.countLeaves(tree.root));

        tree.deleteTree();
    }
}
```
---
##  Interview Tips
- Be comfortable with writing all traversals recursively.
- BFS with a Queue is commonly asked.
- Focus on counting nodes, height, and leaf nodes – basic recursive patterns.
- Practice constructing a tree from given traversals (Inorder + Preorder/Postorder).
- You may be asked to implement serialization/deserialization (advanced).
