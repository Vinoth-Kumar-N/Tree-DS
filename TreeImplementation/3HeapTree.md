# 🌲 Heap Tree

## 📖 Definition
A **Heap Tree** is a complete binary tree that satisfies the **heap property**.

- **Min-Heap**: The value of the parent node is **less than or equal** to the values of its children.
- **Max-Heap**: The value of the parent node is **greater than or equal** to the values of its children.

Heaps are commonly implemented using **arrays**.

---

## 🔧 Supported Methods

- `insert(int value)` – Inserts a value into the heap.
- `extractMin()` – Removes and returns the minimum element (Min-Heap).
- `peek()` – Returns the minimum element without removing it.
- `heapifyDown()` – Maintains heap after removal.
- `heapifyUp()` – Maintains heap after insertion.
- `buildHeap(int[] arr)` – Converts an array into a valid heap.

---

## 🧠 Java Code Implementation (Min-Heap)

```java
public class MinHeap {
    private int[] heap;
    private int size;
    private int capacity;

    public MinHeap(int capacity) {
        this.capacity = capacity;
        this.size = 0;
        this.heap = new int[capacity];
    }

    private int getParent(int i) { return (i - 1) / 2; }
    private int getLeftChild(int i) { return 2 * i + 1; }
    private int getRightChild(int i) { return 2 * i + 2; }

    private void swap(int i, int j) {
        int temp = heap[i];
        heap[i] = heap[j];
        heap[j] = temp;
    }

    private void heapifyUp(int index) {
        while (index > 0 && heap[getParent(index)] > heap[index]) {
            swap(index, getParent(index));
            index = getParent(index);
        }
    }

    private void heapifyDown(int index) {
        int smallest = index;
        int left = getLeftChild(index);
        int right = getRightChild(index);

        if (left < size && heap[left] < heap[smallest])
            smallest = left;
        if (right < size && heap[right] < heap[smallest])
            smallest = right;

        if (smallest != index) {
            swap(index, smallest);
            heapifyDown(smallest);
        }
    }

    public void insert(int val) {
        if (size == capacity) {
            System.out.println("Heap is full");
            return;
        }
        heap[size] = val;
        heapifyUp(size);
        size++;
    }

    public int extractMin() {
        if (size == 0) throw new IllegalStateException("Heap is empty");
        int root = heap[0];
        heap[0] = heap[--size];
        heapifyDown(0);
        return root;
    }

    public int peek() {
        if (size == 0) throw new IllegalStateException("Heap is empty");
        return heap[0];
    }
}
```

---

# 🧠 Heap Tree - Interview Tips

## ✅ Key Concepts

- Complete Binary Tree + Heap Property.
- Min-Heap: Parent is smaller than children.
- Max-Heap: Parent is larger than children.
- Implemented using arrays, not pointers.

---

## 🗣️ Common Interview Questions

### 📌 Theory
- What is a Heap Tree? Difference from BST?
- When do you prefer Min-Heap vs Max-Heap?
- What is the difference between a Heap and Priority Queue?

### 🧑‍💻 Coding
- Insert and delete in Min-Heap/Max-Heap.
- Heapify and BuildHeap algorithms.
- Implement PriorityQueue from scratch.
- Kth smallest/largest element using heap.
- Merge K sorted lists/arrays using heap.

---

## 🆚 Binary Heap vs Binary Search Tree

| Feature         | Binary Heap          | BST                    |
|------------------|----------------------|------------------------|
| Structure        | Complete Binary Tree | Binary Tree            |
| Search Time      | O(n)                 | O(log n) (avg case)    |
| Insert/Delete    | O(log n)             | O(log n) (avg case)    |
| Order Property   | Parent-child relation| Left < Root < Right    |

---

## 💡 Tips for Success

- Know array index rules:
  - Left child: `2*i + 1`
  - Right child: `2*i + 2`
  - Parent: `(i - 1) / 2`
- **Heapify** logic is critical — know both up & down directions.
- Practice writing Min-Heap/Max-Heap from scratch in Java.
- Explain where heaps outperform BSTs (e.g., extract-min/max).

---

## ✅ Interview Scenarios

- Use Min-Heap to solve problems like:
  - Top K smallest/largest numbers
  - Merging K sorted arrays
  - Sliding window maximums
 
# 🧱 Max-Heap in Java

## 📖 Definition

A **Max-Heap** is a complete binary tree where:
- Every parent node is **greater than or equal to** its children.
- The largest element is always at the **root**.

---

## ⚙️ Methods Supported
- `insert(int val)` — Add element into the heap.
- `delete()` — Remove and return the max (root).
- `heapifyDown()` — Maintain max-heap after deletion.
- `heapifyUp()` — Maintain max-heap after insertion.
- `printHeap()` — Print heap as an array.

---

## 💻 Java Code Implementation

```java
public class MaxHeap {
    private int[] heap;
    private int size;
    private int capacity;

    public MaxHeap(int capacity) {
        this.capacity = capacity;
        this.size = 0;
        heap = new int[capacity];
    }

    private int parent(int i) { return (i - 1) / 2; }
    private int leftChild(int i) { return 2 * i + 1; }
    private int rightChild(int i) { return 2 * i + 2; }

    public void insert(int value) {
        if (size == capacity) {
            System.out.println("Heap is full");
            return;
        }

        heap[size] = value;
        size++;
        heapifyUp(size - 1);
    }

    private void heapifyUp(int i) {
        while (i > 0 && heap[i] > heap[parent(i)]) {
            swap(i, parent(i));
            i = parent(i);
        }
    }

    public int delete() {
        if (size == 0) {
            System.out.println("Heap is empty");
            return -1;
        }

        int max = heap[0];
        heap[0] = heap[size - 1];
        size--;
        heapifyDown(0);
        return max;
    }

    private void heapifyDown(int i) {
        int largest = i;
        int left = leftChild(i);
        int right = rightChild(i);

        if (left < size && heap[left] > heap[largest]) {
            largest = left;
        }

        if (right < size && heap[right] > heap[largest]) {
            largest = right;
        }

        if (largest != i) {
            swap(i, largest);
            heapifyDown(largest);
        }
    }

    private void swap(int i, int j) {
        int temp = heap[i];
        heap[i] = heap[j];
        heap[j] = temp;
    }

    public void printHeap() {
        for (int i = 0; i < size; i++) {
            System.out.print(heap[i] + " ");
        }
        System.out.println();
    }
}
```

