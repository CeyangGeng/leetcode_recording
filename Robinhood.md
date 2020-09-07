# Robinhood

1. > - find all the pairwise distinct triplets
   >
   > - Solution:
   >
   >   > ```python
   >   > class Solution:
   >   >     def __init__(self, s):
   >   >         self.s = s
   >   >         size = len(s)
   >   >         self.dp = [[False for _ in range(size)] for _ in range(size)]
   >   >         self.dp[1][0] = True if self.s[1] != self.s[0] else False
   >   >         for i in range(2, size):
   >   >             self.dp[i][i - 1] = True if self.s[i] != self.s[i - 1] else False
   >   >             self.dp[i][i - 2] = True if self.s[i] != self.s[i - 2] else False
   >   >     def is_valid(self, index):
   >   >         return self.dp[index][index - 1] and self.dp[index][index - 2] and self.dp[index - 1][index - 2]
   >   > if __name__ == "__main__":
   >   >     str = "abcdaaae"
   >   >     s = Solution(str)
   >   >     count = 0
   >   >     size = len(str)
   >   >     for i in range(2, size):
   >   >         if s.is_valid(i):
   >   >             count += 1
   >   >     print(count)
   >   > ```

   
   