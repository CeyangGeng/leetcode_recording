# 140 Word Break II

- Description

  > Given a **non-empty** string *s* and a dictionary *wordDict* containing a list of **non-empty** words, add spaces in *s* to construct a sentence where each word is a valid dictionary word. Return all such possible sentences.
  >
  > **Note:**
  >
  > - The same word in the dictionary may be reused multiple times in the segmentation.
  > - You may assume the dictionary does not contain duplicate words.
  >
  > **Example 1:**
  >
  > ```
  > Input:
  > s = "catsanddog"
  > wordDict = ["cat", "cats", "and", "sand", "dog"]
  > Output:
  > [
  >   "cats and dog",
  >   "cat sand dog"
  > ]
  > ```
  >
  > **Example 2:**
  >
  > ```
  > Input:
  > s = "pineapplepenapple"
  > wordDict = ["apple", "pen", "applepen", "pine", "pineapple"]
  > Output:
  > [
  >   "pine apple pen apple",
  >   "pineapple pen apple",
  >   "pine applepen apple"
  > ]
  > Explanation: Note that you are allowed to reuse a dictionary word.
  > ```
  >
  > **Example 3:**
  >
  > ```python
  > Input:
  > s = "catsandog"
  > wordDict = ["cats", "dog", "sand", "and", "cat"]
  > Output:
  > []
  > ```

- Solution

  > 1. backtrack(TLE)
  >
  >    ```python
  >    (1) Backtracking: TLE
  >    class Solution:
  >        def wordBreak(self, s: str, wordDict: List[str]) -> List[str]:
  >            res = []
  >            size = len(s)
  >            for i in range(1, size + 1):
  >                if s[:i] in wordDict:
  >                    self.backtrack(s, wordDict, res, [s[:i]], i)
  >            return res
  >        def backtrack(self, s, word_dict, res, path, begin):
  >            size = len(s)
  >            if begin == size:
  >                res.append(' '.join(path))
  >                return
  >            for end in range(begin + 1, size + 1):
  >                if s[begin : end] in word_dict:
  >                    self.backtrack(s, word_dict, res, path + [s[begin : end]], end)
  >     *******************************************************************
  >    (2)Backtracking: TLE
  >        class Solution:
  >        def wordBreak(self, s: str, wordDict: List[str]) -> List[str]:
  >            res = []
  >            size = len(s)
  >            for i in range(1, size + 1):
  >                self.backtrack(s, wordDict, res, [], 0, i)
  >            return res
  >        def backtrack(self, s, word_dict, res, path, begin, end):
  >            if s[begin: end] not in word_dict:
  >                return
  >            size = len(s)
  >            if end == size:
  >                res.append(' '.join(path + [s[begin : end]]))
  >                return
  >            new_begin = end
  >            for new_end in range(new_begin + 1, size + 1):
  >                self.backtrack(s, word_dict, res, path + [s[begin : end]], new_begin, new_end)
  >    *********************************************************************
  >    # Now that the backtracking(dfs) version exceeds time limits, we could use memo to avoid coping with the same sub problems.
  > # Considering the edge cases is helpful for constructing the framework. There are two kinds of edge cases. When the s is empty, we should return ['']; When there is no match in the s, we should return [].
  >    class Solution:
  >        def wordBreak(self, s: str, wordDict: List[str]) -> List[str]:
  >            memo = dict()
  >            return self.backtrack(s, wordDict, memo, 0)
  >        def backtrack(self, s, word_dict, memo, start):
  >            if start in memo: return memo[start]
  >            size = len(s)
  >            if start == size: return ['']
  >            res = []
  >            for end in range(start + 1, size + 1):
  >                if s[start: end] in word_dict:
  >                    for item in self.backtrack(s, word_dict, memo, end):
  >                        if not item: res.append(s[start:end])
  >                        else: res.append(s[start:end] + ' ' + item)
  >            memo[start] = res
  >            return res
  >            
  >    *********************************************************************
  >    （3）DP: TLE
  >        class Solution:
  >        def wordBreak(self, s: str, wordDict: List[str]) -> List[str]:
  >            size = len(s)
  >            dp = [0] * (size + 1)
  >            dp[size] = [[]]
  >            for i in range(size - 1, -1, -1):
  >                temp = []
  >                for j in range(i + 1, size + 1):
  >                    if s[i:j] in wordDict and dp[j] != 0:
  >                        for item in dp[j]:
  >                            temp.append([s[i:j]]+ item)
  >                if temp: dp[i] = temp
  >            res = []
  >            if dp[0] != 0:
  >                for item in dp[0]:
  >                    res.append(' '.join(item))
  >            return res
  >        
  >      
  >    
  >    ```
  >    
  >    