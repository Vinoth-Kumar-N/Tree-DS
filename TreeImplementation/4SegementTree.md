# 🧩 Segment Tree in Java

## 📖 Definition

A **Segment Tree** is a binary tree used for storing intervals or segments. It allows querying and updating a range of values efficiently — particularly useful for **range sum**, **minimum**, or **maximum queries**.

### Why Segment Tree?
It gives:
- **O(log n)** query time
- **O(log n)** update time
- **O(n)** build time

---

## 🔧 Core Methods

| Method             | Description                                      |
|--------------------|--------------------------------------------------|
| `build()`          | Build the segment tree from the input array      |
| `query(l, r)`      | Return result (sum/min/max) in the range [l, r]  |
| `update(index, val)` | Update a value at a specific index in the array |

---

## 💻 Java Code Implementation (Range Sum Segment Tree)

```java
class SegmentTree {
    int[] tree;
    int n;

    public SegmentTree(int[] nums) {
        n = nums.length;
        tree = new int[4 * n];
        build(nums, 0, n - 1, 0);
    }

    private void build(int[] nums, int start, int end, int node) {
        if (start == end) {
            tree[node] = nums[start];
            return;
        }

        int mid = (start + end) / 2;
        build(nums, start, mid, 2 * node + 1);
        build(nums, mid + 1, end, 2 * node + 2);

        tree[node] = tree[2 * node + 1] + tree[2 * node + 2];
    }

    public int query(int l, int r) {
        return queryUtil(0, n - 1, l, r, 0);
    }

    private int queryUtil(int start, int end, int l, int r, int node) {
        if (r < start || l > end) return 0;
        if (l <= start && end <= r) return tree[node];

        int mid = (start + end) / 2;
        int left = queryUtil(start, mid, l, r, 2 * node + 1);
        int right = queryUtil(mid + 1, end, l, r, 2 * node + 2);

        return left + right;
    }

    public void update(int index, int value) {
        updateUtil(0, n - 1, index, value, 0);
    }

    private void updateUtil(int start, int end, int idx, int value, int node) {
        if (start == end) {
            tree[node] = value;
            return;
        }

        int mid = (start + end) / 2;
        if (idx <= mid)
            updateUtil(start, mid, idx, value, 2 * node + 1);
        else
            updateUtil(mid + 1, end, idx, value, 2 * node + 2);

        tree[node] = tree[2 * node + 1] + tree[2 * node + 2];
    }
}
public class Main {
    public static void main(String[] args) {
        int[] arr = {1, 3, 5, 7, 9, 11};
        SegmentTree st = new SegmentTree(arr);

        System.out.println("Sum of values in range [1, 3]: " + st.query(1, 3)); // 15
        st.update(1, 10);
        System.out.println("Updated sum in range [1, 3]: " + st.query(1, 3));   // 22
    }
}
```

## Interview Tips
- Use when frequent updates and range queries are needed (e.g. stock prices, rainfall data).
- Know difference between:
  - Segment Tree (good for range queries)
  - Binary Indexed Tree (good for prefix sums)
- Variants of Segment Tree:
  - Lazy Propagation (for range updates)
  - Min/Max Tree (instead of sum)
- Watch out for:
  - 0-based vs 1-based indexing
  - Tree size: use 4 * n to be safe
- Common Problems:
  - Range Sum Query
  - Range Minimum/Maximum Query
  - Dynamic Range Queries with Updates
