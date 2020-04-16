# House Robber

1.  198  House Robber

   - Description

     > You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security system connected and **it will automatically contact the police if two adjacent houses were broken into on the same night**.
     >
     > Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight **without alerting the police**.
     >
     > **Example 1:**
     >
     > ```
     > Input: [1,2,3,1]
     > Output: 4
     > Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3).
     >              Total amount you can rob = 1 + 3 = 4.
     > ```
     >
     > **Example 2:**
     >
     > ```python
     > Input: [2,7,9,3,1]
     > Output: 12
     > Explanation: Rob house 1 (money = 2), rob house 3 (money = 9) and rob house 5 (money = 1).
     >              Total amount you can rob = 2 + 9 + 1 = 12.
     > ```

   - Solution

     > ```python
     > # Only record the max amount if the current house is stolen
     > class Solution:
     >     def rob(self, nums: List[int]) -> int:
     >         size = len(nums)
     >         if size == 0: return 0
     >         if size == 1: return nums[0]
     >         if size == 2: return max(nums[0], nums[1])
     >         nums[2] += nums[0]
     >         if size == 3: return max(nums[2], nums[1])
     >         res = max(nums[2], nums[1])
     >         for i in range(3, size):
     >             nums[i] += max(nums[i - 2], nums[i - 3])
     >             res = max(res, nums[i])
     >         return res
     >     *************************************************************
     > # Use another space to record the max amount of the current house is not stolen
     >     class Solution:
     >     def rob(self, nums: List[int]) -> int:
     >         if not nums: return 0
     >         size = len(nums)
     >         pre = [0, 0]
     >         for i in range(size):
     >             stolen = nums[i] + pre[1]
     >             not_stolen = max(pre)
     >             cur = [stolen, not_stolen]
     >             pre = cur
     >         return max(pre)
     > ```

2.  213House Robber II

   - Description

     > You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed. All houses at this place are **arranged in a circle.** That means the first house is the neighbor of the last one. Meanwhile, adjacent houses have security system connected and **it will automatically contact the police if two adjacent houses were broken into on the same night**.
     >
     > Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight **without alerting the police**.
     >
     > **Example 1:**
     >
     > ```
     > Input: [2,3,2]
     > Output: 3
     > Explanation: You cannot rob house 1 (money = 2) and then rob house 3 (money = 2),
     >              because they are adjacent houses.
     > ```
     >
     > **Example 2:**
     >
     > ```python
     > Input: [1,2,3,1]
     > Output: 4
     > Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3).
     >              Total amount you can rob = 1 + 3 = 4.
     > ```

   - Solution

     > Because the first and the last house can not be stolen at the same night, there are two basic cases: the first house is stolen, then the last house must not be stolen; the first house is not stolen, then the last house can be stolen but nor for sure!
     >
     > So I split this problem into two sub problems.
     >
     > ```python
     > class Solution:
     >     def rob(self, nums: List[int]) -> int:
     >         def rob_sub(nums):
     >             if not nums: return 0
     >             pre = [0, 0]
     >             size = len(nums)
     >             for i in range(size):
     >                 stolen = nums[i] + pre[1]
     >                 not_stolen = max(pre)
     >                 pre = [stolen, not_stolen]
     >             return max(pre)
     >         if not nums: return 0
     >         if len(nums) == 1: return nums[0]
     >         return max(rob_sub(nums[:-1]) , rob_sub(nums[1:]))
     >         
     > ```
     >
     > 

3.  337  House Robber III

   - Description

     > The thief has found himself a new place for his thievery again. There is only one entrance to this area, called the "root." Besides the root, each house has one and only one parent house. After a tour, the smart thief realized that "all houses in this place forms a binary tree". It will automatically contact the police if two directly-linked houses were broken into on the same night.
     >
     > Determine the maximum amount of money the thief can rob tonight without alerting the police.
     >
     > **Example 1:**
     >
     > ```
     > Input: [3,2,3,null,3,null,1]
     > 
     >      3
     >     / \
     >    2   3
     >     \   \ 
     >      3   1
     > 
     > Output: 7 
     > Explanation: Maximum amount of money the thief can rob = 3 + 3 + 1 = 7.
     > ```
     >
     > **Example 2:**
     >
     > ```python
     > Input: [3,4,5,1,3,null,1]
     > 
     >      3
     >     / \
     >    4   5
     >   / \   \ 
     >  1   3   1
     > 
     > Output: 9
     > Explanation: Maximum amount of money the thief can rob = 4 + 5 = 9.
     > ```

   - Solution

     > - Recursive + memo(overlapping sub questions)
     >
     >   ```python
     >   class Solution:
     >       def rob(self, root: TreeNode) -> int:
     >           look_up = dict()
     >           return self.rob_sub(root, look_up)
     >       def rob_sub(self, root, memo):
     >           if not root: return 0
     >           if root in memo: return memo[root]
     >           val = 0
     >           if root.left:
     >               val += self.rob_sub(root.left.left, memo) + self.rob_sub(root.left.right, memo)
     >           if root.right:
     >               val += self.rob_sub(root.right.left, memo) + self.rob_sub(root.right.right, memo)
     >           cur_max = max(val + root.val, self.rob_sub(root.left, memo) + self.rob_sub(root.right, memo))
     >           memo[root] = cur_max
     >           return memo[root]
     >   ```
     >
     > - Bottom up dp
     >
     >   ```python
     >   class Solution:
     >       def rob(self, root: TreeNode) -> int:
     >           return max(self.rob_sub(root))
     >       def rob_sub(self, root):
     >           if not root: return [0, 0]
     >           # the first element reprensents that the root is not stolen
     >           # the second element represents that the root is stloen
     >           left = self.rob_sub(root.left)
     >           right = self.rob_sub(root.right)
     >           first = max(left) + max(right)
     >           second = left[0] + right[0] + root.val
     >           return[first, second]
     >   ```
     >
     >   





