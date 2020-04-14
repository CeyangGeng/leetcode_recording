# Backtracking

- Template:  reference: https://labuladong.gitbook.io/algo and https://leetcode.com/problems/subsets/discuss/429534/General-Backtracking-questions-solutions-in-Python-for-reference-%3A

  There are three key elements in the backtracking: path, choose list and ending condition.

  The framework of backtrack is as following.

  ```python
  result = []
  def backtrack(path, choose_list):
  	if satisefy the ending condition:
  		res.append(path)
  		return
  	for choices in choice_list:
  		make choice(add choice to the path, remove choice from the choice_list)
  		backtrack(path, updated choice_list)
  		remove choice(remove choice from the path, add the choice to the choice_list)		
  ```

- Problems

  > 78 Subsets(It's much better to use index rather than the list slice)
  >
  > ```python
  > class Solution:
  >  def subsets(self, nums: List[int]) -> List[List[int]]:
  >      res = []
  >      self.backtrack(nums, 0, res, [])
  >      return res
  >  def backtrack(self, nums, index, res, path):
  >      res.append(path[:])
  >      for i in range(index, len(nums)):
  >          self.backtrack(nums, i + 1, res, path + [nums[i]])
  > ```
  >
  > 77  Combinations
  >
  > ```python
  > class Solution:
  >  def combine(self, n: int, k: int) -> List[List[int]]:
  >      res = []
  >      self.backtrack(n, k, 1, res, [])
  >      return res
  >  def backtrack(self, n, k, index, res, path):
  >      if len(path) == k:
  >          res.append(path[:])
  >      for i in range(index, n + 1):
  >          self.backtrack(n, k, i + 1, res, path + [i])
  > ```
  >
  > 40. Combination Sum II (Master the method of removing the repeat result!)
  >
  > ```python
  > class Solution:
  >     def combinationSum2(self, candidates: List[int], target: int) -> List[List[int]]:
  >         res = []
  >         self.backtrack(sorted(candidates), 0, res, [], target)
  >         return res
  >     def backtrack(self, nums, index, res, path, target):
  >         if target < 0: return
  >         if target == 0: 
  >             res.append(path[:])
  >             return
  >         size = len(nums)
  >         for i in range(index, size):
  >             if i > index and nums[i] == nums[i - 1]: continue # of great importance! remove the same result on the same level through skip the same element!
  >             self.backtrack(nums, i + 1, res, path + [nums[i]], target - nums[i])
  > ```
  >
  > 216 Combination Sum III
  >
  > ```python
  > class Solution:
  >     def combinationSum3(self, k: int, n: int) -> List[List[int]]:
  >         res = []
  >         self.backtrack(k, n, res, [], 1)
  >         return res
  >     def backtrack(self, k, n, res, path, index):
  >         if len(path) > k or n < 0: return
  >         if len(path) == k and n == 0: 
  >             res.append(path[:])
  >             return
  >         for i in range(index, 10):
  >             self.backtrack(k, n - i, res, path + [i], i + 1)
  > ```
  >
  > 39 Combination Sum
  >
  > ```python
  > class Solution:
  >     def combinationSum(self, candidates: List[int], target: int) -> List[List[int]]:
  >         res = []
  >         self.backtrack(candidates, target, res, [], 0)
  >         return res
  >     def backtrack(self, nums, target, res, path, index):
  >         if target < 0: return
  >         if target == 0: 
  >             res.append(path)
  >             return
  >         size = len(nums)
  >         for i in range(index, size):
  >             self.backtrack(nums, target - nums[i], res, path + [nums[i]], i)
  > ```
  >
  > 332 Coin Change
  >
  > ```python
  > # Backtracking method appears TLE.
  > class Solution:
  >     def __init__(self):
  >         self.count = float('inf')
  >     def coinChange(self, coins: List[int], amount: int) -> int:
  >         self.backtrack(sorted(coins, reverse = True), amount, 0, 0)
  >         return self.count if self.count < float('inf') else -1
  >     def backtrack(self, nums, target, cur_len, index):
  >         if cur_len > self.count: return
  >         if target < 0: return
  >         if target == 0:
  >             self.count = min(cur_len, self.count)
  >             return 
  >         size = len(nums)
  >         for i in range(index, size):
  >             self.backtrack(nums, target - nums[i], cur_len + 1, i)
  > ------------------------------------------------------------------------
  > class Solution:
  >     def coinChange(self, coins: List[int], amount: int) -> int:
  >         m = float('inf')
  >         dp = [0] + [m] * amount
  >         for i in range(1, amount + 1):
  >             dp[i] = min(dp[i - c] if i - c >= 0 else m for c in coins) + 1
  >         return [dp[amount], -1][dp[amount] == float('inf')]
  > ------------------------------------------------------------------------
  > 
  > ```
  >
  > 90  Subsets II
  >
  > ```python
  > Iterative without extra space
  > class Solution:
  >     def subsetsWithDup(self, nums: List[int]) -> List[List[int]]:
  >         res = [[]]
  >         nums.sort()
  >         for i in range(len(nums)):
  >             if i == 0 or nums[i] != nums[i - 1]:
  >                 l = len(res)
  >             for j in range(len(res) - l, len(res)):
  >                 res.append(res[j] + [nums[i]])
  >         return res
  > ------------------------------------------------------------------------
  > class Solution:
  >     def subsetsWithDup(self, nums: List[int]) -> List[List[int]]:
  >         res = [[]]
  >         nums.sort()
  >         for i in range(len(nums)):
  >             if i == 0 or nums[i] != nums[i - 1]:
  >                 l = len(res)
  >             for j in range(len(res) - l, len(res)):
  >                 res.append(res[j] + [nums[i]])
  >         return res
  > ```
  >
  > 46 Permutations
  >
  > ```python
  > class Solution:
  >     def permute(self, nums: List[int]) -> List[List[int]]:
  >         res = []
  >         self.backtrack(nums, res, [])
  >         return res
  >     def backtrack(self, nums, res, path):
  >         size = len(nums)
  >         if len(path) == size:
  >             res.append(path)
  >         for i in nums:
  >             if i in path: continue
  >             self.backtrack(nums, res, path + [i])
  > -----------------------------------------------------------------
  > # iterative version
  > class Solution:
  >     def permute(self, nums: List[int]) -> List[List[int]]:
  >         res = [[]]
  >         for n in nums:
  >             temp = []
  >             for r in res:
  >                 for i in range(len(r) + 1):
  >                     temp.append(r[:i] + [n] + r[i:])
  >             res = temp
  >         return res
  > ```
  >
  > 47 Permutations II
  >
  > ```python
  > class Solution:
  >     def permuteUnique(self, nums: List[int]) -> List[List[int]]:
  >         res = []
  >         nums.sort()
  >         self.backtrack(nums, res, [], len(nums))
  >         return res
  >     def backtrack(self, nums, res, path, size):
  >         if len(path) == size:
  >             res.append(path)
  >         for i in range(len(nums)):
  >             if i > 0 and nums[i] == nums[i - 1]: continue
  >             self.backtrack(nums[:i] + nums[i + 1:], res, path + [nums[i]], size)
  > ----------------------------------------------------------------------
  > #To remove duplicates, just avoid inserting a number after any of its duplicates.
  > class Solution:
  >     def permuteUnique(self, nums: List[int]) -> List[List[int]]:
  >         res = [[]]
  >         for n in nums:
  >             temp = []
  >             for r in res:
  >                 for j in range(len(r) + 1):
  >                     temp.append(r[:j] + [n] + r[j:])
  >                     if j < len(r) and n == r[j]: break
  >             res = temp
  >         return res
  > --------------------------------------------------------------------
  > Use counter to remove duplicates
  > class Solution:
  >     def permuteUnique(self, nums: List[int]) -> List[List[int]]:
  >         def backtrack(path, counter):
  >             if len(path) == len(nums):
  >                 res.append(path[:])
  >             for i in counter:
  >                 if counter[i] > 0:
  >                     counter[i] -= 1
  >                     path.append(i)
  >                     backtrack(path, counter)
  >                     counter[i] += 1
  >                     path.pop()
  >             
  >         res = []
  >         backtrack([], Counter(nums))
  >         return res
  > ```
  >
  > 

  