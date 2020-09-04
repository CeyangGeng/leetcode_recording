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

   > 第一题是两个list，A和B，长度分别为n和m，对于B中所有数，返回A中小于等于该数的数字个数，返回长度为m的列表。m和n的上限都是10^5，一下子想到的是O((m+n)logn)的算法，所以上限是10^6。

   - Solution (Binary search)

     ```python
     def find(num1, num2):
         num1.sort()
         res = []
         for num in num2:
             left, right = 0, len(num1)
             while left < right:
                 mid = left + (right - left) // 2
                 if num1[mid] <= num:
                     left = mid + 1
                 else:
                     right = mid
             res.append(left)
     ```

3. - Question

     > \684. Redundant Connection
     >
     > In this problem, a tree is an **undirected** graph that is connected and has no cycles.
     >
     > The given input is a graph that started as a tree with N nodes (with distinct values 1, 2, ..., N), with one additional edge added. The added edge has two different vertices chosen from 1 to N, and was not an edge that already existed.
     >
     > The resulting graph is given as a 2D-array of `edges`. Each element of `edges` is a pair `[u, v]` with `u < v`, that represents an **undirected** edge connecting nodes `u` and `v`.
     >
     > Return an edge that can be removed so that the resulting graph is a tree of N nodes. If there are multiple answers, return the answer that occurs last in the given 2D-array. The answer edge `[u, v]` should be in the same format, with `u < v`.
     >
     > **Example 1:**
     >
     > ```
     > Input: [[1,2], [1,3], [2,3]]
     > Output: [2,3]
     > Explanation: The given undirected graph will be like this:
     >   1
     >  / \
     > 2 - 3
     > ```
     >
     > 
     >
     > **Example 2:**
     >
     > ```
     > Input: [[1,2], [2,3], [3,4], [1,4], [1,5]]
     > Output: [1,4]
     > Explanation: The given undirected graph will be like this:
     > 5 - 1 - 2
     >     |   |
     >     4 - 3
     > ```
     >
     > 
     >
     > **Note:**
     >
     > The size of the input 2D-array will be between 3 and 1000.
     >
     > Every integer represented in the 2D-array will be between 1 and N, where N is the size of the input array.
     >
     > 
     >
     > 
     >
     > **Update (2017-09-26):**
     > We have overhauled the problem description + test cases and specified clearly the graph is an ***undirected\*** graph. For the ***directed\*** graph follow up please see **[Redundant Connection II](https://leetcode.com/problems/redundant-connection-ii/description/)**). We apologize for any inconvenience caused.

   - Solution

     > 1. dfs: Everty time we meet a new edge, try to find if they are connected alreay. If they are, return this edge; else connect these two nodes of this edge.
     >
     >    ```python
     >    class Solution:
     >        def findRedundantConnection(self, edges: List[List[int]]) -> List[int]:
     >            self.connect = defaultdict(list)
     >            for from_node, to_node in edges:
     >                visit = set()
     >                if self.dfs(visit, from_node, to_node):
     >                    return [from_node, to_node]
     >                else:
     >                    self.connect[from_node].append(to_node)
     >                    self.connect[to_node].append(from_node)
     >        def dfs(self, visit, from_node, to_node):
     >            if from_node == to_node: return True
     >            visit.add(from_node)
     >            for adj_node in self.connect[from_node]:
     >                if adj_node not in visit:
     >                    if self.dfs(visit, adj_node, to_node): return True
     >            return False
     >    ```
     >
     > 2. union find
     >
     >    ```python
     >    class UF:
     >        def __init__(self, N):
     >            self.parent = [i for i in range(N)]
     >        def find(self, x):
     >            while x != self.parent[x]:
     >                self.parent[x] = self.parent[self.parent[x]]
     >                x = self.parent[x]
     >            return x
     >        def union(self, p, q):
     >            root_p = self.find(p)
     >            root_q = self.find(q)
     >            if root_p == root_q: return False
     >            self.parent[root_p] = root_q
     >            return True
     >    class Solution:
     >        def findRedundantConnection(self, edges: List[List[int]]) -> List[int]:
     >            size = len(edges)
     >            uf = UF(size)
     >            for from_node, to_node in edges:
     >                if not uf.union(from_node - 1, to_node - 1):
     >                    return [from_node, to_node]
     >    ```

4. - Question

     > ![img](https://oss.1point3acres.cn/forum/202008/24/002956a4axdtdwidiuxjca.jpeg)

   - Solution

     ```python
     from collections import defaultdict
     def find(languages, person_language, friends):
         dic_for_person_languages = defaultdict(list)
         for item in person_languages:
             person, langua = item.split(" speaks ")
             for language in languages:
                 if language in langua:
                     dic_for_person_languages[person].append(language)
         edges = []
         for friend_pair in friends:
             pair = friend_pair.split(" is friends with ")
             edges.append(pair)
         graph = defaultdict(list)
         persons = set()
         for a, b in edges:
             persons.add(a)
             persons.add(b)
             language_a = dic_for_person_languages[a]
             language_b = dic_for_person_languages[b]
             if set(language_a) & set(language_b):
                 continue
             else:
                 graph[a].append(b)
                 graph[b].append(a)
         visit = set()
         language_times = defaultdict(int)
         for person in persons:
             if person not in visit:
                 stack = [person]
                 while stack:
                     p = stack.pop()
                     visit.add(p)
                     for lang in dic_for_person_languages[p]:
                         language_times[lang] += 1
                     for adj in graph[p]:
                         if adj not in visit:
                             stack.append(adj)
         max_times = 0
         res = []
         for language, times in language_times.items():
             if times >= max_times:
                 max_times = times
                 res.append(language)
         res.sort()
         return res[0]
     if __name__ == "__main__":
         languages = {"Korean", "French", "Romanian"}
         person_languages = ["Alice speaks French and Korean",\
                             "Chris speaks Korean",\
                             "Bob speaks Romanian",\
                             "Daniel speaks Romanian"]
         friends = ["Alice is friends with Bob",\
                    "Alice is friends with Chris",\
                    "Bob is friends with Chris",\
                    "Bob is friends with Daniel"]
         res = find(languages, person_languages, friends)
         print(res)
     ```

5. - Question

     > 第一道题是validate word。给你一个正确单词的list和一个input的list.要求你判断每一个input word 是不是valid，return bool[]。valid的criteria 是 长度得一样，不一样的字母<=1。tricky的地方在于有runtime 限制。一个8个testcases，

   - Solution

     > Trie:
     >
     > ```python
     > class Solution:
     >     def __init__(self, standard_list):
     >         self.standard_list = standard_list
     >         self.trie = {}
     >         self.count = 0
     >     def construct(self):
     >         t = self.trie
     >         for word in self.standard_list:
     >             t = self.trie
     >             for w in word:
     >                 t = t.setdefault(w, {})
     >             t['#'] = {}
     >     def find(self, word, dic):
     >         for w in word:
     >             self.count = 0
     >             if w in dic:
     >                 return self.find(word[1:], dic[w])
     >             else:
     >                 self.count += 1
     >                 if self.count > 1: return False
     >                 return any (self.find(word[1:], d) for d in dic.values())
     >         return True if '#' in dic else False
     > 
     > if __name__ == "__main__":
     >     standard_list = ["abc", "acd", "adj"]
     >     input_list = ["ace", "abd", "adj"]
     >     s = Solution(standard_list)
     >     s.construct()
     >     size = len(standard_list[0])
     >     res = []
     >     for word in input_list:
     >         if len(word) != size:
     >             res.append(False)
     >         else:
     >             res.append(s.find(word, s.trie))
     >     print(res)
     > 
     > ```

6. - Question

     > 实现一个加密、解密的类。明文的每一个字符映射到密文的两个字符。不同明文可能映射到同一密文。 比如: 'z' --> 'aw', 'r' -->'wo', 't' --> 'wo'.
     > 实现加密功能: 'zr' --> 'awwo'
     > 实现解密功能，揭秘需要输出所有的可能性: 'wowo' --> ['rr', 'rt', 'tt', 'tr']
     >
     > 进阶问题：
     > \1. 写测试
     > \2. 算复杂度
     > \3. 若解密时提供一个英语字典，要求输出的词必须是英语词的话，如何优化

   - Solution

     > ```python
     > from collections import defaultdict
     > class Solution:
     >     def __init__(self, code, dic):
     >         self.encode_dic = dict()
     >         self.decode_dic = defaultdict(list)
     >         self.trie = {}
     >         self.dic = dic
     >         for item in code:
     >             plain, cypher = item.split('-->')
     >             self.encode_dic[plain] = cypher
     >             self.decode_dic[cypher].append(plain)
     >     def construct(self):
     >         for word in self.dic:
     >             t = self.trie
     >             for w in word:
     >                 t = t.setdefault(w, {})
     >             t['#'] = {}
     >     def find(self, word, dic):
     >         for w in word:
     >             return self.find(word[1:], dic[w])
     >         else: return False
     >         return True if '#' in dic else False
     > 
     >     def encode(self, word):
     >         res = ''
     >         for w in word:
     >             res += self.encode_dic[w]
     >         return res
     >     def decode(self, word):
     >         size = len(word)
     >         res = []
     >         for i in range(0, size, 2):
     >             temp = word[i:i + 2]
     >             if res == []:
     >                 for p in self.decode_dic[temp]:
     >                     res.append(p)
     >             else:
     >                 res = [r + p for r in res for p in self.decode_dic[temp]]
     >         ret = []
     >         for r in res:
     >             if self.find(r, self.trie):
     >                 ret.append[r]
     >         return ret
     > 
     > if __name__ == "__main__":
     >     dic = {'zr'}
     >     pair = ['z-->aw', 'r-->wo', 't-->wo']
     >     s = Solution(pair, dic)
     >     s.construct()
     >     res_1 = s.encode("zr")
     >     res_2 = s.decode("wowo")
     >     print(res_1, res_2)
     > ```

7. - Question

     > ![image-20200904012003671](C:\Users\gcy\AppData\Roaming\Typora\typora-user-images\image-20200904012003671.png)

   - Solution

     > coin chage
     >
     > ```python
     > class Solution:
     >     def change(self, amount: int, coins: List[int]) -> int:
     >         dp = [0] * (amount + 1)
     >         dp[0] = 1
     >         for coin in coins:
     >             for num in range(coin, amount + 1):
     >                 dp[num] += dp[num - coin]
     >         return dp[-1]
     >         
     > ```

8. - Question

     > ![image-20200904013158835](C:\Users\gcy\AppData\Roaming\Typora\typora-user-images\image-20200904013158835.png)

   - Solution

     > 

9. - Description

     > - 一个买本子题，大概描述如下：
     >
     > ​    比如有三家店第一家：一梱本子20元，30个本子一捆，第二家：一梱本子25元，40个本子一梱，第三家：一梱本子3元，2本一梱，问给100元最多能买多少本。

   - Solution

     > 1. backtrack:
     >
     >    ```python
     >    class Solution:
     >        def __init__(self, dic):
     >            self.dic = dic
     >            self.max_count = 0
     >            self.res = []
     >        def find(self, money, path, count):
     >            if money < 0:
     >                return
     >            if money == 0:
     >                if count > self.max_count:
     >                    self.max_count = count
     >                    self.res = path
     >                return
     >            for key, val in self.dic.items():
     >                self.find(money - key, path + [(key, val)], count + val)
     >    if __name__ == "__main__":
     >        dic = {20:30, 25:40, 3:2}
     >        s = Solution(dic)
     >        s.find(100, [], 0)
     >        print(s.max_count, s.res)
     >    ```
     >
     > 2. dp: similar as coin change
     >
     >    ```
     >    def helper(amount, dic):
     >        dp = [0] * (amount + 1)
     >        for key, val in dic.items():
     >            for num in range(key, amount + 1):
     >                dp[num] = max(dp[num], dp[num - key] + val)
     >        return dp[-1]
     >    ```

10. - Question

     > \697. Degree of an Array
     >
     > Given a non-empty array of non-negative integers `nums`, the **degree** of this array is defined as the maximum frequency of any one of its elements.
     >
     > Your task is to find the smallest possible length of a (contiguous) subarray of `nums`, that has the same degree as `nums`.
     >
     >  
     >
     > **Example 1:**
     >
     > ```
     > Input: nums = [1,2,2,3,1]
     > Output: 2
     > Explanation: 
     > The input array has a degree of 2 because both elements 1 and 2 appear twice.
     > Of the subarrays that have the same degree:
     > [1, 2, 2, 3, 1], [1, 2, 2, 3], [2, 2, 3, 1], [1, 2, 2], [2, 2, 3], [2, 2]
     > The shortest length is 2. So return 2.
     > ```
     >
     > **Example 2:**
     >
     > ```
     > Input: nums = [1,2,2,3,1,4,2]
     > Output: 6
     > Explanation: 
     > The degree is 3 because the element 2 is repeated 3 times.
     > So [2,2,3,1,4,2] is the shortest subarray, therefore returning 6.
     > ```
     >
     >  
     >
     > **Constraints:**
     >
     > - `nums.length` will be between 1 and 50,000.
     > - `nums[i]` will be an integer between 0 and 49,999.

   - Solution

     > One pass, record the max frequency when traversing the array and update the max frequency and minimum length of the most frequent elements.
     >
     > ```python
     > class Solution:
     >     def findShortestSubArray(self, nums: List[int]) -> int:
     >         first, count, res, degree = {}, {}, 0, 0
     >         for i, num in enumerate(nums):
     >             first.setdefault(num, i)
     >             count[num] = count.get(num, 0) + 1
     >             c = count[num]
     >             if c > degree:
     >                 degree = c
     >                 res = i - first[num] + 1
     >             elif c == degree:
     >                 res = min(res, i - first[num] + 1)
     >         return res
     > ```

11. - Question

      > \264. Ugly Number II
      >
      > Medium
      >
      > 2062127Add to ListShare
      >
      > Write a program to find the `n`-th ugly number.
      >
      > Ugly numbers are **positive numbers** whose prime factors only include `2, 3, 5`. 
      >
      > **Example:**
      >
      > ```
      > Input: n = 10
      > Output: 12
      > Explanation: 1, 2, 3, 4, 5, 6, 8, 9, 10, 12 is the sequence of the first 10 ugly numbers.
      > ```
      >
      > **Note:** 
      >
      > 1. `1` is typically treated as an ugly number.
      > 2. `n` **does not exceed 1690**.

    - Solution

      > dp: the three pointer increase from 1 one by one
      >
      > ```python
      > class Solution:
      >     def nthUglyNumber(self, n: int) -> int:
      >         dp = [1]
      >         i2, i3, i5 = 0, 0, 0
      >         while n > 1:
      >             u2, u3, u5 = dp[i2] * 2, dp[i3] * 3, dp[i5] * 5
      >             num = min(u2, u3, u5)
      >             if num == u2: i2 += 1
      >             if num == u3: i3 += 1
      >             if num == u5: i5 += 1
      >             dp.append(num)
      >             n -= 1
      >         return dp[-1]
      > ```

12. - Question

      > 313. Super Ugly Number
      >
      > Write a program to find the `nth` super ugly number.
      >
      > Super ugly numbers are positive numbers whose all prime factors are in the given prime list `primes` of size `k`.
      >
      > **Example:**
      >
      > ```
      > Input: n = 12, primes = [2,7,13,19]
      > Output: 32 
      > Explanation: [1,2,4,7,8,13,14,16,19,26,28,32] is the sequence of the first 12 
      >              super ugly numbers given primes = [2,7,13,19] of size 4.
      > ```
      >
      > **Note:**
      >
      > - `1` is a super ugly number for any given `primes`.
      > - The given numbers in `primes` are in ascending order.
      > - 0 < `k` ≤ 100, 0 < `n` ≤ 106, 0 < `primes[i]` < 1000.
      > - The nth super ugly number is guaranteed to fit in a 32-bit signed integer.

    - Solution

      > ```python
      > class Solution:
      >     def nthSuperUglyNumber(self, n: int, primes: List[int]) -> int:
      >         dp = [1]
      >         dic = defaultdict(int)
      >         while n > 1:
      >             min_num = float('inf')
      >             min_index = -1
      >             for p in primes:
      >                 temp = dp[dic[p]] * p
      >                 if temp < min_num:
      >                     min_num = temp
      >             for p in primes:
      >                 if dp[dic[p]] * p == min_num:
      >                     dic[p] += 1
      >             dp.append(min_num)
      >             n -= 1
      >         return dp[-1]
      > ```

13. - Question

      > https://oss.1point3acres.cn/forum/201910/07/031723r695ifoa95tx0u0t.png

    - Solution

      > ```python
      > def helper(nums):
      >     size = len(nums)
      >     dic = {}
      >     for i in range(1, size):
      >         for j in range(nums[i - 1], nums[i] + 1):
      >             dic[j] = dic.get(j, 0) + 1
      >     max_frequency = 0
      >     res = 0
      >     for key, val in dic.items():
      >         if val > max_frequency:
      >             res = key
      >             max_frequency = val
      >     return res           
      >         
      > ```
