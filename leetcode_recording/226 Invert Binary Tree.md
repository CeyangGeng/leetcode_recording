# 226 Invert Binary Tree

- Description

  > Invert a binary tree.
  >
  > **Example:**
  >
  > Input:
  >
  > ```
  >      4
  >    /   \
  >   2     7
  >  / \   / \
  > 1   3 6   9
  > ```
  >
  > Output:
  >
  > ```
  >      4
  >    /   \
  >   7     2
  >  / \   / \
  > 9   6 3   1
  > ```

- Solution

  > 1. recursive(really slow) 
  >
  >    ```python
  >    class Solution:
  >        def invertTree(self, root: TreeNode) -> TreeNode:
  >            if not root: return root
  >            tmp = root.left # Don't forget to save the root.left before change
  >            root.left = self.invertTree(root.right)
  >            root.right = self.invertTree(tmp)
  >            return root
  >    ```
  >
  > 2. iterative dfs + stack
  >
  >    ```python3
  >    class Solution:
  >        def invertTree(self, root: TreeNode) -> TreeNode:
  >            if not root: return root
  >            stack = [(root, root.left, root.right)]
  >            while stack:
  >                node, left, right = stack.pop()
  >                node.right, node.left = left, right
  >                if left: stack.append((left, left.left, left.right))
  >                if right: stack.append((right, right.left, right.right))
  >            return root
  >    ------------------------------------------------------------------------
  >    # It is not necessary to put the node.left and node.right into the stack, the relationship always exists.
  >    class Solution:
  >        def invertTree(self, root: TreeNode) -> TreeNode:
  >            if not root: return root
  >            stack = [root]
  >            while stack:
  >                node = stack.pop()
  >                left, right = node.left, node.right
  >                node.left, node.right = right, left
  >                if left: stack.append(left)
  >                if right: stack.append(right)
  >            return root
  >    ```
  >
  > 3. iterative +  bfs + deque
  >
  >    ```python3
  >    class Solution:
  >        def invertTree(self, root: TreeNode) -> TreeNode:
  >            from collections import deque
  >            queue = deque()
  >            if not root: return root
  >            queue.append((root, root.left, root.right))
  >            while queue:
  >                node, left, right = queue.popleft()
  >                node.right, node.left = left, right
  >                if left: queue.append((left, left.left, left.right))
  >                if right: queue.append((right, right.left, right.right))
  >            return root
  >     --------------------------------------------------------------------------
  >     class Solution:
  >        def invertTree(self, root: TreeNode) -> TreeNode:
  >            from collections import deque
  >            queue = deque()
  >            if not root: return root
  >            queue.append(root)
  >            while queue:
  >                node = queue.popleft()
  >                left, right = node.left, node.right
  >                node.left, node.right = right, left
  >                if left: queue.append(left)
  >                if right: queue.append(right)
  >            return root
  >    ```