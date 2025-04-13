# 🟥⬛ Red-Black Tree

A **Red-Black Tree** is a type of **self-balancing Binary Search Tree** where each node stores an extra bit representing "color" (red or black) to ensure the tree remains approximately balanced during insertions and deletions.

---

## ✅ Properties of Red-Black Tree

1. Every node is either red or black.
2. Root is always black.
3. Red nodes cannot have red children (No two reds in a row).
4. Every path from a node to its descendant NULL nodes has the same number of black nodes.
5. New insertions are always red (rebalancing is applied afterward).

---

## 🔧 Methods (Operations)

- **Insert** – Standard BST insert + fix-up (rotations + recoloring).
- **Delete** – More complex; rebalancing after deletion.
- **Rotations** – Left and right rotations to maintain balance.
- **Traversal** – Inorder, Preorder, etc.
- **Color management** – Recolor nodes as needed.

---

## 🧑‍💻 Java Code Implementation (With Comments)

```java
class RBNode {
    int data;
    RBNode left, right, parent;
    boolean isRed;

    public RBNode(int data) {
        this.data = data;
        this.isRed = true; // New nodes are red by default
    }
}

public class RedBlackTree {
    private RBNode root;

    // Left rotate
    private void leftRotate(RBNode x) {
        RBNode y = x.right;
        x.right = y.left;

        if (y.left != null) y.left.parent = x;
        y.parent = x.parent;

        if (x.parent == null)
            root = y;
        else if (x == x.parent.left)
            x.parent.left = y;
        else
            x.parent.right = y;

        y.left = x;
        x.parent = y;
    }

    // Right rotate
    private void rightRotate(RBNode y) {
        RBNode x = y.left;
        y.left = x.right;

        if (x.right != null) x.right.parent = y;
        x.parent = y.parent;

        if (y.parent == null)
            root = x;
        else if (y == y.parent.right)
            y.parent.right = x;
        else
            y.parent.left = x;

        x.right = y;
        y.parent = x;
    }

    // Insert node
    public void insert(int data) {
        RBNode node = new RBNode(data);
        root = bstInsert(root, node);
        fixInsert(node);
    }

    // Standard BST insert
    private RBNode bstInsert(RBNode root, RBNode node) {
        if (root == null) return node;

        if (node.data < root.data) {
            root.left = bstInsert(root.left, node);
            root.left.parent = root;
        } else if (node.data > root.data) {
            root.right = bstInsert(root.right, node);
            root.right.parent = root;
        }
        return root;
    }

    // Fix Red-Black Tree after insertion
    private void fixInsert(RBNode node) {
        RBNode parent = null;
        RBNode grandparent = null;

        while (node != root && node.isRed && node.parent.isRed) {
            parent = node.parent;
            grandparent = parent.parent;

            if (parent == grandparent.left) {
                RBNode uncle = grandparent.right;

                if (uncle != null && uncle.isRed) {
                    grandparent.isRed = true;
                    parent.isRed = false;
                    uncle.isRed = false;
                    node = grandparent;
                } else {
                    if (node == parent.right) {
                        node = parent;
                        leftRotate(node);
                    }

                    parent.isRed = false;
                    grandparent.isRed = true;
                    rightRotate(grandparent);
                }
            } else {
                RBNode uncle = grandparent.left;

                if (uncle != null && uncle.isRed) {
                    grandparent.isRed = true;
                    parent.isRed = false;
                    uncle.isRed = false;
                    node = grandparent;
                } else {
                    if (node == parent.left) {
                        node = parent;
                        rightRotate(node);
                    }

                    parent.isRed = false;
                    grandparent.isRed = true;
                    leftRotate(grandparent);
                }
            }
        }
        root.isRed = false;
    }

    // Inorder traversal
    public void inorder(RBNode node) {
        if (node != null) {
            inorder(node.left);
            System.out.print((node.isRed ? "R" : "B") + node.data + " ");
            inorder(node.right);
        }
    }

    public void printTree() {
        inorder(root);
        System.out.println();
    }

    // Main
    public static void main(String[] args) {
        RedBlackTree tree = new RedBlackTree();
        int[] values = {10, 20, 30, 15, 25, 5, 1};

        for (int val : values)
            tree.insert(val);

        System.out.print("Inorder Red-Black Tree: ");
        tree.printTree();
    }
}
```
## 🆚 AVL vs Red-Black Tree

| Feature         | AVL Tree                    | Red-Black Tree              |
|------------------|-----------------------------|-----------------------------|
| Balance Factor   | Strictly balanced            | Loosely balanced            |
| Insert/Delete    | Slower (more rotations)      | Faster (less strict rules)  |
| Search           | Faster due to tighter balance| Slightly slower             |
| Use Case         | Read-heavy operations        | Insert/Delete-heavy ops     |

---

## 🚀 Tips for Success

- Always explain **why** properties are maintained (especially after insert/delete).
- Red-Black Tree ensures **O(log n)** time even in the worst-case scenarios.
- Practice dry-runs of insertions/deletions to show rebalancing clearly.
- Be comfortable coding left and right **rotations**.
- **Interviewers often ask** to visualize the tree at each step — draw it out!
