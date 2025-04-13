# 🌳 AVL Tree (Adelson-Velsky and Landis Tree)

An **AVL Tree** is a **self-balancing Binary Search Tree (BST)** where the difference in height (balance factor) between the left and right subtrees of **any node is at most 1**.

This balance is maintained after every insertion and deletion using rotations.

---

## 🔧 Methods (Operations)

- **Insert** – Insert while maintaining the balance via rotations.
- **Delete** – Remove a node and rebalance if needed.
- **Rotations** – LL, RR, LR, RL to restore balance.
- **Traversal** – Inorder/Preorder/Postorder.
- **Height** – Measure tree depth.
- **Balance Factor** – Height(left subtree) - Height(right subtree)

---

## 🧑‍💻 Java Code Implementation (With Comments)

```java
class AVLNode {
    int key, height;
    AVLNode left, right;

    public AVLNode(int d) {
        key = d;
        height = 1;
    }
}

public class AVLTree {
    AVLNode root;

    // Get height of a node
    int height(AVLNode N) {
        return N == null ? 0 : N.height;
    }

    // Get balance factor
    int getBalance(AVLNode N) {
        return N == null ? 0 : height(N.left) - height(N.right);
    }

    // Right rotate
    AVLNode rightRotate(AVLNode y) {
        AVLNode x = y.left;
        AVLNode T2 = x.right;

        x.right = y;
        y.left = T2;

        y.height = Math.max(height(y.left), height(y.right)) + 1;
        x.height = Math.max(height(x.left), height(x.right)) + 1;

        return x;
    }

    // Left rotate
    AVLNode leftRotate(AVLNode x) {
        AVLNode y = x.right;
        AVLNode T2 = y.left;

        y.left = x;
        x.right = T2;

        x.height = Math.max(height(x.left), height(x.right)) + 1;
        y.height = Math.max(height(y.left), height(y.right)) + 1;

        return y;
    }

    // Insert and rebalance
    AVLNode insert(AVLNode node, int key) {
        if (node == null) return new AVLNode(key);

        if (key < node.key)
            node.left = insert(node.left, key);
        else if (key > node.key)
            node.right = insert(node.right, key);
        else
            return node; // Duplicate keys not allowed

        node.height = 1 + Math.max(height(node.left), height(node.right));
        int balance = getBalance(node);

        // Balancing
        if (balance > 1 && key < node.left.key)  // LL
            return rightRotate(node);

        if (balance < -1 && key > node.right.key)  // RR
            return leftRotate(node);

        if (balance > 1 && key > node.left.key) {  // LR
            node.left = leftRotate(node.left);
            return rightRotate(node);
        }

        if (balance < -1 && key < node.right.key) {  // RL
            node.right = rightRotate(node.right);
            return leftRotate(node);
        }

        return node;
    }

    // Inorder Traversal
    void inorder(AVLNode node) {
        if (node != null) {
            inorder(node.left);
            System.out.print(node.key + " ");
            inorder(node.right);
        }
    }

    // Main method to test
    public static void main(String[] args) {
        AVLTree tree = new AVLTree();
        tree.root = tree.insert(tree.root, 10);
        tree.root = tree.insert(tree.root, 20);
        tree.root = tree.insert(tree.root, 30);
        tree.root = tree.insert(tree.root, 40);
        tree.root = tree.insert(tree.root, 50);
        tree.root = tree.insert(tree.root, 25);

        System.out.print("Inorder traversal of AVL tree: ");
        tree.inorder(tree.root);
    }
}
```
## Interview Tips
- AVL Tree maintains balance to keep time complexity at O(log n) for insert/search/delete.
- Know the 4 types of rotations:
     - LL (Single Right Rotate)
     - RR (Single Left Rotate)
     - LR (Left Right Double Rotate)
     - RL (Right Left Double Rotate)
- Compare AVL vs. BST: AVL avoids the worst-case linear time of an unbalanced BST.
- Used where faster lookups are more important than insert/delete speed.
