# Python-binary-.tree-.right-..side-..view.py


This code provides **two different approaches** (DFS and BFS) to solving the problem of **finding the right-side view** of a binary tree.

## **Problem Explanation**
Given a binary tree, we need to return a list of values seen when looking at the tree from the right side. This means that for each level of the tree, we should pick **only the rightmost node** visible from that level.

---

# **1st Approach: Depth-First Search (DFS)**
### **Theory**
- This solution uses **pre-order DFS traversal** (root → right → left) to traverse the tree.
- We maintain a `depth` variable to track how deep we are in the tree.
- We maintain a `result` list that stores the first node encountered at each depth.
- We always explore the **right subtree first** so that the first node we see at a given depth is the rightmost one.

### **Code Walkthrough**
```python
class Solution(object):
    def rightSideView(self, root):
        result = []
        self.rightSideViewDFS(root, 1, result)
        return result

    def rightSideViewDFS(self, node, depth, result):
        if not node:  # Base case: If node is None, return
            return

        if depth > len(result):  # If this is the first time visiting this depth, store the node value
            result.append(node.val)

        # First, visit the right subtree to ensure the rightmost node is added first
        self.rightSideViewDFS(node.right, depth + 1, result)
        self.rightSideViewDFS(node.left, depth + 1, result)
```

### **Time & Space Complexity**
- **Time Complexity**: \( O(n) \), since we visit each node once.
- **Space Complexity**: \( O(h) \), where \( h \) is the height of the tree (in the worst case, \( O(n) \) for a skewed tree).

---

# **2nd Approach: Breadth-First Search (BFS)**
### **Theory**
- This solution uses **level-order traversal** (BFS) to traverse the tree level by level.
- At each level, we take the last node encountered and add it to the result.
- We use a queue (`current` list) to store the nodes at each level.
- After processing all nodes at the current level, we move to the next level.

### **Code Walkthrough**
```python
class Solution2(object):
    def rightSideView(self, root):
        if root is None:
            return []

        result, current = [], [root]
        while current:
            next_level = []
            for node in current:
                if node.left:
                    next_level.append(node.left)
                if node.right:
                    next_level.append(node.right)
            result.append(node.val)  # Store the last node of the current level
            current = next_level  # Move to the next level

        return result
```

### **Time & Space Complexity**
- **Time Complexity**: \( O(n) \), since we visit each node once.
- **Space Complexity**: \( O(n) \) in the worst case (when the last level has many nodes).

---

# **Summary**
| Approach | Method | Time Complexity | Space Complexity | Key Idea |
|----------|--------|----------------|----------------|----------|
| DFS (Recursive) | Preorder Traversal (root → right → left) | \( O(n) \) | \( O(h) \) (height of tree) | Add first node at each depth |
| BFS (Iterative) | Level-order traversal using queue | \( O(n) \) | \( O(n) \) | Add last node of each level |

Both methods work efficiently, but **DFS is more memory efficient for balanced trees, while BFS is better for wide trees**.

Would you like a visualization of how these algorithms work? 🚀
