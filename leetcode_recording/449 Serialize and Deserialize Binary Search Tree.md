#  449 Serialize and Deserialize Binary Search Tree

- Descrition

  > Serialization is the process of converting a data structure or object into a sequence of bits so that it can be stored in a file or memory buffer, or transmitted across a network connection link to be reconstructed later in the same or another computer environment.
  >
  > Design an algorithm to serialize and deserialize a **binary search tree**. There is no restriction on how your serialization/deserialization algorithm should work. You just need to ensure that a binary search tree can be serialized to a string and this string can be deserialized to the original tree structure.
  >
  > **The encoded string should be as compact as possible.**
  >
  > **Note:** Do not use class member/global/static variables to store states. Your serialize and deserialize algorithms should be stateless.

- Solution

  > The difference between 449 and 297 is the requirement of compacting. There are no '#'s in the serialization process. As a result, the deserialize process in the 297 with the help of '#' is no longer function. So we need to restore the tree with the preorder and inorder lists or the postorder and inorder.  Restoring with the help of preorder and inorder needs reverse the preorder and inorder. So I serialize the tree in the postorder directly. 
  >
  > ```python3
  > class Codec:
  > 
  >     def serialize(self, root: TreeNode) -> str:
  >         """Encodes a tree to a single string.
  >         """
  >         def helper(node):
  >             if node:
  >                 helper(node.left)
  >                 helper(node.right)
  >                 res.append(str(node.val))
  >         res = []
  >         helper(root)
  >         return ' '.join(res)
  >         
  > 
  >     def deserialize(self, data: str) -> TreeNode:
  >         """Decodes your encoded data to tree.
  >         """
  >         postorder = list(map(int, data.split()))
  >         inorder = sorted(postorder)
  >         return self.build_tree(postorder, inorder)
  >     
  >     def build_tree(self, postorder, inorder):
  >         def helper(stop):
  >             if inorder and inorder[-1] != stop:
  >                 root_val = postorder.pop()
  >                 root = TreeNode(root_val)
  >                 root.right = helper(root_val)
  >                 inorder.pop()
  >                 root.left = helper(stop)
  >                 return root
  >         return helper(None)
  > ```
  >
  > 