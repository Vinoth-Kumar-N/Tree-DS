# 🔡 Trie (Prefix Tree) in Java

## 📖 Definition

A **Trie**, also known as a **Prefix Tree**, is a special type of N-ary tree used to store associative data structures, usually strings. It allows **efficient retrieval of strings**, especially when dealing with **prefix searches**.

Each node represents a **character**, and the path from root to leaf forms a word.

---

## 🔧 Core Methods

| Method          | Description                                   |
|-----------------|-----------------------------------------------|
| `insert(word)`  | Inserts a word into the Trie                  |
| `search(word)`  | Returns true if the word is in the Trie       |
| `startsWith(prefix)` | Returns true if any word starts with the given prefix |
| `delete(word)`  | Deletes a word from the Trie (optional/advanced) |

---

## 💻 Java Code Implementation

```java
class TrieNode {
    TrieNode[] children;
    boolean isEndOfWord;

    public TrieNode() {
        children = new TrieNode[26]; // for lowercase a-z
        isEndOfWord = false;
    }
}

public class Trie {
    private final TrieNode root;

    public Trie() {
        root = new TrieNode();
    }

    public void insert(String word) {
        TrieNode current = root;
        for (char ch : word.toCharArray()) {
            int index = ch - 'a';
            if (current.children[index] == null)
                current.children[index] = new TrieNode();
            current = current.children[index];
        }
        current.isEndOfWord = true;
    }

    public boolean search(String word) {
        TrieNode node = searchNode(word);
        return node != null && node.isEndOfWord;
    }

    public boolean startsWith(String prefix) {
        return searchNode(prefix) != null;
    }

    private TrieNode searchNode(String word) {
        TrieNode current = root;
        for (char ch : word.toCharArray()) {
            int index = ch - 'a';
            if (current.children[index] == null)
                return null;
            current = current.children[index];
        }
        return current;
    }
}
public class Main {
    public static void main(String[] args) {
        Trie trie = new Trie();
        trie.insert("apple");
        trie.insert("app");

        System.out.println(trie.search("apple"));    // true
        System.out.println(trie.search("app"));      // true
        System.out.println(trie.search("appl"));     // false
        System.out.println(trie.startsWith("app"));  // true
    }
}
```
## Interview Tips
- Tries are excellent for autocomplete, spell checking, and dictionary problems.
- **Time Complexity**: 
  - Insert/Search/Prefix = O(L), where L is length of word/prefix.
- Can be extended to support:
  - Deletion
  - Case insensitivity
  - Unicode (by using `HashMap` instead of array)
- Common Problems:
  - Implement Trie
  - Word Search II (Leetcode)
  - Longest Prefix Matching
  - Replace Words (Leetcode)
- Pro tip: For large character sets (e.g. Unicode or dictionary with wildcards), use `Map<Character, TrieNode>` instead of fixed array.
