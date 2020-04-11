# leetcode-538

- description

  > Given the sorted array: [-10,-3,0,5,9],
  >
  > One possible answer is: [0,-3,9,-10,null,5], which represents the following height balanced BST:
  >
  >       0
  >      / \
  >
  >    -3   9
  >    /   /
  >  -10  5

- solution

  > - recursive
  >
  >   """
  >
  >   class Solution:
  >       def __init__(self):
  >           self.offset = 0
  >       def convertBST(self, root: TreeNode) -> TreeNode:
  >           if not root: return root
  >           root.right = self.convertBST(root.right)
  >           root.val += self.offset
  >           self.offset = root.val
  >           root.left = self.convertBST(root.left)
  >           return root
  >
  >   """
  >
  > - iterative
  >
  >   """
  >
  >   class Solution:
  >       def convertBST(self, root: TreeNode) -> TreeNode:
  >           stack, p, pre = [], root, 0
  >           while stack or p:
  >               while p:
  >                   stack.append(p)
  >                   p = p.right
  >               p = stack.pop()
  >               p.val += pre
  >               pre = p.val
  >               p = p.left
  >           return root
  >
  >   """
  >
  > 





