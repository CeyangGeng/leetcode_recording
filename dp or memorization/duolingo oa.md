# duolingo oa

1. Question

   > ![img](https://oss.1point3acres.cn/forum/202008/24/002848ug4ykuyz1vqgq1uq.png)

- Solution

  > 1. dfs + memo
  >
  >    > ```python
  >    > class Solution:
  >    >     def __init__(self, s1, s2):
  >    >         self.s1 = s1
  >    >         self.s2 = s2
  >    >         self.size_1 = len(s1)
  >    >         self.size_2 = len(s2)
  >    >         self.memo = {}
  >    >     def match(self, index1, index2):
  >    >         if index2 >= self.size_2 and index1 < self.size_1:
  >    >             return 0
  >    >         if index2 <= self.size_2 and index1 == self.size_1:
  >    >             return 1
  >    >         if (index1, index2) in self.memo: return self.memo[(index1, index2)]
  >    >         count = 0
  >    >         for i in range(index2, self.size_2):
  >    >             if self.s2[i] == self.s1[index1]:
  >    >                 count += self.match(index1 + 1, i + 1)
  >    >         self.memo[(index1, index2)] = count
  >    >         return count
  >    > if __name__ == "__main__":
  >    >     s1 = "ABCD"
  >    >     s2 = "ABCBABCD"
  >    >     s = Solution(s1, s2)
  >    >     print(s.match(0, 0))
  >    > ```

2. - Question

     