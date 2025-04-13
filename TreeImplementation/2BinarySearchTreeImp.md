# 🌳 Binary Search Tree (BST)

A **Binary Search Tree (BST)** is a type of Binary Tree in which each node follows the property:
- The **left subtree** of a node contains only nodes with **values less than** the node’s value.
- The **right subtree** contains only nodes with **values greater than** the node’s value.
- Both left and right subtrees must also be binary search trees.

---

## 🔧 Methods (Operations)

- **Insertion** – Add a new node following BST properties.
- **Search** – Find a node with a specific value.
- **Traversal** – Inorder (sorted), Preorder, Postorder.
- **Delete** – Remove a node and maintain BST structure.
- **Find Min/Max** – Smallest or largest value in BST.
- **Height** – Depth of the tree from root to deepest node.

---

## 🧑‍💻 Java Code Implementation (With Comments)

```java
class BSTNode {
    int key;
    BSTNode left, right;

    public BSTNode(int item) {
        key = item;
        left = right = null;
    }
}

public class BinarySearchTree {
    BSTNode root;

    // Insert a key in BST
    public BSTNode insert(BSTNode node, int key) {
        if (node == null) return new BSTNode(key);

        if (key < node.key)
            node.left = insert(node.left, key);
        else if (key > node.key)
            node.right = insert(node.right, key);

        return node;
    }

    // Inorder Traversal (gives sorted order)
    public void inorder(BSTNode node) {
        if (node == null) return;
        inorder(node.left);
        System.out.print(node.key + " ");
        inorder(node.right);
    }

    // Search for a value
    public boolean search(BSTNode node, int key) {
        if (node == null) return false;
        if (node.key == key) return true;
        if (key < node.key)
            return search(node.left, key);
        else
            return search(node.right, key);
    }

    // Find the node with minimum value
    public BSTNode findMin(BSTNode node) {
        while (node.left != null)
            node = node.left;
        return node;
    }

    // Delete a key from BST
    public BSTNode delete(BSTNode node, int key) {
        if (node == null) return null;

        if (key < node.key)
            node.left = delete(node.left, key);
        else if (key > node.key)
            node.right = delete(node.right, key);
        else {
            // Node with one child or no child
            if (node.left == null)
                return node.right;
            else if (node.right == null)
                return node.left;

            // Node with two children
            BSTNode minNode = findMin(node.right);
            node.key = minNode.key;
            node.right = delete(node.right, minNode.key);
        }
        return node;
    }

    // Height of BST
    public int height(BSTNode node) {
        if (node == null) return 0;
        return 1 + Math.max(height(node.left), height(node.right));
    }

    // Main method to test
    public static void main(String[] args) {
        BinarySearchTree bst = new BinarySearchTree();
        bst.root = bst.insert(bst.root, 50);
        bst.insert(bst.root, 30);
        bst.insert(bst.root, 70);
        bst.insert(bst.root, 20);
        bst.insert(bst.root, 40);
        bst.insert(bst.root, 60);
        bst.insert(bst.root, 80);

        System.out.print("Inorder (Sorted): ");
        bst.inorder(bst.root);
        System.out.println();

        System.out.println("Search 60: " + bst.search(bst.root, 60));
        System.out.println("Min Value: " + bst.findMin(bst.root).key);
        System.out.println("Height: " + bst.height(bst.root));

        bst.delete(bst.root, 30);
        System.out.print("Inorder after deleting 30: ");
        bst.inorder(bst.root);
    }
}
```
---
## Interview Tips
- Inorder traversal of BST always gives sorted order.
- Learn deletion cases: leaf, one child, and two children.
- Be confident in writing recursive insert, search, delete functions.
- Interviewers often ask “Is this a BST?” → Do inorder and check sorted.
- Understand time complexity:Best/Average: O(log n)
- Worst (unbalanced): O(n)
