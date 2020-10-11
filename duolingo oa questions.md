1. > ![img](https://oss.1point3acres.cn/forum/202008/24/002848ug4ykuyz1vqgq1uq.png)

2. >  第一题是两个list，A和B，长度分别为n和m，对于B中所有数，返回A中小于等于该数的数字个数，返回长度为m的列表。m和n的上限都是10^5，一下子想到的是O((m+n)logn)的算法，所以上限是10^6。

3. > 684. Redundant Connection
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
   > 1
   > / \
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
   >  |   |
   >  4 - 3
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
   > We have overhauled the problem description + test cases and specified clearly the graph is an ***undirected\*** graph. For the ***direc**
   >
   > 
   >
   > **ted\*** graph follow up please see **[Redundant Connection II](https://leetcode.com/problems/redundant-connection-ii/description/)**). We apologize for any inconvenience caused.

4. > ![img](https://oss.1point3acres.cn/forum/202008/24/002956a4axdtdwidiuxjca.jpeg)

5. > 第一道题是validate word。给你一个正确单词的list和一个input的list.要求你判断每一个input word 是不是valid，return bool[]。valid的criteria 是 长度得一样，不一样的字母<=1。tricky的地方在于有runtime 限制。一个8个testcases，

6. > 实现一个加密、解密的类。明文的每一个字符映射到密文的两个字符。不同明文可能映射到同一密文。 比如: 'z' --> 'aw', 'r' -->'wo', 't' --> 'wo'.
   > 实现加密功能: 'zr' --> 'awwo'
   > 实现解密功能，揭秘需要输出所有的可能性: 'wowo' --> ['rr', 'rt', 'tt', 'tr']
   >
   > 进阶问题：
   > \1. 写测试
   > \2. 算复杂度
   > \3. 若解密时提供一个英语字典，要求输出的词必须是英语词的话，如何优化

   ```python
   from collections import defaultdict
   class Solution:
       def __init__(self):
           self.match = {"z": "aw", "r":"wo", "t":"wo"}
       def encode(self, str):
           res = ''
           for s in str:
               res += self.match[s]
           return res
       def decode(self, str):
           self.reverse_match = defaultdict(list)
           for key, val in self.match.items():
               self.reverse_match[val].append(key)
           self.memo = dict()
           self.str = str
           return self.backtrack(0, self.trie)
       def backtrack(self, start, dictionary):
           if start == len(self.str) :
               if '#' in dictionary:
                   return []
               else:
                   return '*'
           #if start in self.memo:
               #return self.memo[start]
           temp_res = []
           for end in range(start, len(self.str)):
               cur_str = self.str[start : end + 1]
               if cur_str in self.reverse_match:
                   cur_temp_res = []
                   for decoded_str in self.reverse_match[cur_str]:
                       if decoded_str in dictionary.keys():
                           temp = self.backtrack(end + 1, dictionary[decoded_str])
                           if temp and temp != '*':
                               for later_decodes_str in temp:
                                   cur_temp_res.append(decoded_str + later_decodes_str)
                           elif temp == []:
                               cur_temp_res.append(decoded_str)
                   temp_res += cur_temp_res
           #self.memo[start] = temp_res
           return temp_res
       def construct(self, dictionary):
           self.trie = dict()
           for word in dictionary:
               t = self.trie
               for w in word:
                   t = t.setdefault(w, {})
               t['#'] = {}
   
   
   if __name__ == "__main__":
       s = Solution()
       s.construct(["rr", "rt", "tt"])
       res = s.decode("wowo")
       print(res)
   ```
   
   
   
7. > ![image-20200904012003671](C:\Users\gcy\AppData\Roaming\Typora\typora-user-images\image-20200904012003671.png)

8. > ![image-20200904013158835](C:\Users\gcy\AppData\Roaming\Typora\typora-user-images\image-20200904013158835.png)

9. > - 一个买本子题，大概描述如下：
   >
   > ​    比如有三家店第一家：一梱本子20元，30个本子一捆，第二家：一梱本子25元，40个本子一梱，第三家：一梱本子3元，2本一梱，问给100元最多能买多少本。

10. > \697. Degree of an Array
    >
    > Given a non-empty array of non-negative integers `nums`, the **degree** of this array is defined as the maximum frequency of any one of its elements.
    >
    > Your task is to find the smallest possible length of a (contiguous) subarray of `nums`, that has the same degree as `nums`.

11. > \264. Ugly Number II
    >
    > Medium
    >
    > 2062127Add to ListShare
    >
    > Write a program to find the `n`-th ugly number.
    >
    > Ugly numbers are **positive numbers** whose prime factors only include `2, 3, 5`. 

12. > 313. Super Ugly Number
    >
    > Write a program to find the `nth` super ugly number.
    >
    > Super ugly numbers are positive numbers whose all prime factors are in the given prime list `primes` of size `k`.

13. > https://oss.1point3acres.cn/forum/201910/07/031723r695ifoa95tx0u0t.png

14. > 第二次问题就是地里出现过的queue, stack, priority queue。给你一串operation，让你判断可能是哪些data structure。
    > 例如，(insert, 1) (insert 2) (insert 3) (pop 3), 那就只能是stack。
    > follow-up是如果你不知道从头开始完整的trace，只知道最后n个，会有什么Difficulty
    >
    > ```
    > from collections import deque
    > import heapq
    > def is_stack(operations):
    >     stack = []
    >     for operation, val in operations:
    >         if operation == 'insert':
    >             stack.append(val)
    >         if operation == 'pop':
    >             if stack[-1] == val:
    >                 stack.pop()
    >             else:
    >                 return False
    >     return True
    > 
    > def is_deque(operations):
    >     queue = deque()
    >     for operation, val in operations:
    >         if operation == 'insert':
    >             queue.append(val)
    >         if operation == 'pop':
    >             if val == queue[0]:
    >                 queue.popleft()
    >             else:
    >                 return False
    >     return True
    > 
    > def is_priority_queue(operations):
    >     heap = []
    >     for operation, val in operations:
    >         if operation == 'insert':
    >             heapq.heappush(heap, val)
    >         if operation == 'pop':
    >             temp = heapq.heappop(heap)
    >             if val != temp:
    >                 return False
    >     return True
    > if __name__ == '__main__':
    >     operations_stack = [('insert', 1), ('insert', 3), ('insert', 2), ('pop', 1), ('pop', 2), ('pop', 3)]
    >     res = is_priority_queue(operations_stack)
    >     print(res)
    > ```
    >
    > Follow up
    >
    > If the input is only a few last elements of the complete input array, how will you improve your solution?
    >
    > If the data structure is stack, the latter popped out element should be in the front position. If the data structure is deque, the later popped out elements should be in the later position. 
    >
    > ```
    > from collections import deque
    > import heapq
    > def is_stack(operations):
    >     stack = []
    >     for operation, val in operations[::-1]:
    >         if operation == 'pop':
    >             stack.append(val)
    >         if operation == 'insert':
    >             if stack.pop() != val:
    >                 return False
    >     return True
    > def is_deque(operations):
    >     queue = deque()
    >     for operation, val in operations[::-1]:
    >         if operation == 'pop':
    >             queue.insert(0, val)
    >         if operation == 'insert':
    >             if val != queue.pop():
    >                 return False
    >     return True
    > def is_prioroty_queue(operations):
    >     heap = []
    >     heapq.heapify(heap)
    >     for operation, val in operations:
    >         if operation == 'insert':
    >             heapq.heappush(heap, val)
    >         if operation == 'pop':
    >             if heap:
    >                 cur_min = heap[0]
    >                 if val < cur_min: continue
    >                 if val == cur_min: heapq.heappop(heap)
    >                 if val > cur_min: return False
    >     return True
    > ```

15. > \329. Longest Increasing Path in a Matrix
    >
    > Hard
    >
    > 228342Add to ListShare
    >
    > Given an integer matrix, find the length of the longest increasing path.
    >
    > From each cell, you can either move to four directions: left, right, up or down. You may NOT move diagonally or move outside of the boundary (i.e. wrap-around is not allowed).
    >
    > **Example 1:**
    >
    > ```
    > Input: nums = 
    > [
    >   [9,9,4],
    >   [6,6,8],
    >   [2,1,1]
    > ] 
    > Output: 4 
    > Explanation: The longest increasing path is [1, 2, 6, 9].
    > ```
    >
    > **Example 2:**
    >
    > ```python
    > Input: nums = 
    > [
    >   [3,4,5],
    >   [3,2,6],
    >   [2,2,1]
    > ] 
    > Output: 4 
    > Explanation: The longest increasing path is [3, 4, 5, 6]. Moving diagonally is not allowed.
    > ```
    >
    > Solution:
    >
    > Here is what I'm thinking. 
    >
    > - We do not need to record the positions in the increasing path to avoid repeated search because the increasing condition has already filtered the visited positions in the path.
    >
    > - During the dfs process, we can get much more information. For example, if we want to find the longest increasing path from the index (0, 0), during the dfs process, we will traverse all the neighbor indexes around (0, 0). If the number at index(0, 1) is larger than the number at index (0, 0), we will also get the longest increasing path from index (0, 1). So we need a dictionary to record the longest increasing path to avoid repeated search.
    >
    >   ```python
    >   class Solution:
    >       def longestIncreasingPath(self, matrix: List[List[int]]) -> int:
    >           if not matrix: return 0
    >           self.m, self.n = len(matrix), len(matrix[0])
    >           self.memo = {}
    >           self.matrix = matrix
    >           self.max_len = 1
    >           self.directions = [(-1, 0), (1, 0), (0, 1), (0, -1)]
    >           for i in range(self.m):
    >               for j in range(self.n):
    >                   if (i, j) not in self.memo:
    >                       self.helper(i, j)
    >           return self.max_len
    >       def helper(self, x, y):
    >           cur_max_len = 1
    >           for delta_x, delta_y in self.directions:
    >               new_x, new_y = x + delta_x, y + delta_y
    >               if 0 <= new_x < self.m and 0 <= new_y < self.n and self.matrix[new_x][new_y] > self.matrix[x][y]:
    >                   if (new_x, new_y) in self.memo: cur_len = 1 + self.memo[(new_x, new_y)]
    >                   else: cur_len = 1 + self.helper(new_x, new_y)
    >                   cur_max_len = max(cur_len, cur_max_len)
    >           self.memo[(x, y)] = cur_max_len
    >           self.max_len = max(self.max_len, cur_max_len)
    >           return cur_max_len
    >   ```
    >
    > Follow up:
    >
    > 如果允许有一次往下走的机会怎么做（把“是否往下走过”加进状态里，DP方法一样）
    >
    > ```python
    > class Solution:
    >     def longest_increasing_path(self, matrix):
    >         if not matrix: return 0
    >         self.m, self.n = len(matrix), len(matrix[0])
    >         self.matrix = matrix
    >         self.max_len = 1
    >         self.directions = [(-1, 0), (1, 0), (0, -1), (0, 1)]
    >         for i in range(self.m):
    >             for j in range(self.n):
    >                 if (i, j) not in self.memo:
    >                     self.helper(i, j, 0)
    >         return self.max_len
    >     def heler(self, x, y, used):
    >         cur_max_len = 1
    >         for delta_x, delta_y in directions:
    >             new_x, new_y = x + delta_x, y + delta_y
    >             cur_len = 1
    >             if 0 <= new_x < m and 0 <= new_y < n:
    >                 if used == 1:
    >                     if self.matrix[new_x][new_y] > self.matrix[x][y]:
    >                         if (new_x, new_y, 1) in self.memo:
    >                             cur_len = 1 + self.memo[(new_x, new_y, 1)]
    >                         else:
    >                             cur_len = 1 + self.helper(new_x, new_y, 1)
    >                 elif used == 0:
    >                     if self.matrix[new_x][new_y] > self.matrix[x][y]:
    >                         if (new_x, new_y, 0) in self.memo:
    >                             cur_len = 1 + self.memo[(new_x, new_y, 0)]
    >                         else:
    >                             cur_len = 1 + self.helper(new_x, new_y, 0)
    >                     elif self.matrix[new_x][new_y] < self.matrix[x][y]:
    >                         if (new_x, new_y, 1) in self.memo:
    >                             cur_len = 1 + self.memo[(new_x, new_y, 1)]
    >                         else:
    >                             cur_len = 1 + self.helper(new_x, new_y, 1)
    >                 cur_max_len = max(cur_max_len, cur_len)
    >         self.max_len = max(self.max_len, cur_max_len)
    > ```
    >
    > 

16. > # Largest Sum Contiguous Subarray
    >
    > <img src="C:\Users\gcy\AppData\Roaming\Typora\typora-user-images\image-20201004101141345.png" alt="image-20201004101141345" style="zoom:50%;" />
    >
    > ```python
    > #################################prefix version#################################
    > #To record the start and finish index, I use the two variables start and finish. The start index is supposed to be initialized to be 0 and the finish index is supposed to be initialized to be -1. 
    > '''
    > While traversing the all the elements in the array, we can record the prefix. Besides, we should initialize the min_prefix_sum to be 0. If all the numbers are positive, we could always keep the min_prefix_sum to be 0. If all the numbers are negative, we will update the start index contiguously while traversing the list.
    > If there are negative numbers and positive numbers, if the current prefix sum is less than the current minimum prefix sum, we could update the current minimum prefix sum to be the current prefix sum and update the start index to be the current index + 1. Else if the current prefix sum minus the minimum prefix sum is larger than the max_range_sum, we will update the max_range_sum. These two if condition has to be paralled but not contiguous. At the end, if we find that the finish index is still the -1, we can determine that all the number in the list is negative. In this case, we just need to find the maximum number in the list and update the start and finish index to be the current index.
    > '''
    > def find_max_sub_array(nums):
    >     min_prefix_sum = 0
    >     max_range_sum = float('-inf')
    >     cur_sum = 0
    >     size = len(nums)
    >     start = 0
    >     finish = -1
    >     for i in range(size):
    >         cur_sum += nums[i]
    >         if cur_sum < min_prefix_sum:
    >             min_prefix_sum = cur_sum
    >             start = i + 1
    >         elif cur_sum - min_prefix_sum > max_range_sum:
    >             max_range_sum = cur_sum - min_prefix_sum
    >             finish = i
    >     if finish != -1:
    >         return start, finish, max_range_sum
    >     for i in range(size):
    >         if nums[i] > max_range_sum:
    >             max_range_sum  = nums[i]
    >             start = finish = i
    >     return max_range_sum, start, finish
    >     
    > ############################reverse max_ending_here to be 0 whenever the max_ending_here becomes negative#######################################
    > def find_max_sub_array(nums):
    >     start, finish = 0, -1
    >     max_so_far, max_ending_here = float('-inf'), 0
    >     for i, num in enumerate(nums):
    >         max_ending_here += num
    >         if max_ending_here < 0:
    >             max_ending_here = 0
    >             start = i + 1
    >         if max_ending_here > max_so_far:
    >             max_so_far = max_ending_here
    >             finish = i
    >     if finish != -1:
    >         return start, finish, max_so_far
    >     for i in range(len(nums)):
    >         if nums[i] > max_so_far:
    >             max_so_far = nums[i]
    >             start, finish = i, i
    >     return max_so_far, start, finish
    > 
    > if __name__ == "__main__":
    >     nums = [-2, -3, 4, -1, -2, 1, 5, -3]
    >     res = find_max_sub_array(nums)
    >     print(res)
    > ```

17. > <img src="C:\Users\gcy\AppData\Roaming\Typora\typora-user-images\image-20201004121704817.png" alt="image-20201004121704817" style="zoom:50%;" />
    >
    > ```python
    > def find_max_sub_array(nums):
    >     start, end = 0, -1
    >     max_ending_here, max_so_far = 0, float('-inf')
    >     for i, num in enumerate(nums):
    >         max_ending_here += num
    >         if max_ending_here < 0:
    >             max_ending_here = 0
    >             start = i + 1
    >         elif max_ending_here > max_so_far:
    >             max_so_far = max_ending_here
    >             finish = i
    >     if finish != -1:
    >         return start, finish, max_so_far
    >     for i, num in enumerate(nums):
    >         if num > max_so_far:
    >             max_so_far = num
    >             start, finish = i, i
    >     return start, finish, max_so_far
    > 
    > def find_max_sum(matrix):
    >     if not matrix: return 0
    >     m, n = len(matrix), len(matrix[0])
    >     max_sum = float('-inf')
    >     final_left, final_right, final_top, final_bottom = -1, -1, -1, -1
    >     temp = [0] * m
    >     for left in range(n):
    >         temp = [0] * m
    >         for right in range(left, n):
    >             for i in range(m):
    >                 temp[i] += matrix[i][right]
    >             temp_start, temp_finish, temp_max_sum = find_max_sub_array(temp)
    >             if temp_max_sum > max_sum:
    >                 max_sum = temp_max_sum
    >                 final_left, final_right, final_top, final_bottom = left, right, temp_start, temp_finish
    >     return max_sum, final_left, final_right, final_top, final_bottom
    > if __name__ == "__main__":
    >     matrix = [
    >                 [1, 2, -1, -4, -20],
    >                 [-8, -3, 4, 2, 1],
    >                 [3, 8, 10, 1, 3],
    >                 [-4, -1, 1, 7, -6]
    >             ]
    >     res = find_max_sum(matrix)
    >     print(res)
    > ```

18. > \5. Longest Palindromic Substring
    >
    > Medium
    >
    > 8157579Add to ListShare
    >
    > Given a string `s`, return *the longest palindromic substring* in `s`.
    >
    >  
    >
    > **Example 1:**
    >
    > ```
    > Input: s = "babad"
    > Output: "bab"
    > Note: "aba" is also a valid answer.
    > ```
    >
    > **Example 2:**
    >
    > ```
    > Input: s = "cbbd"
    > Output: "bb"
    > ```
    >
    > **Example 3:**
    >
    > ```
    > Input: s = "a"
    > Output: "a"
    > ```
    >
    > **Example 4:**
    >
    > ```
    > Input: s = "ac"
    > Output: "a"
    > ```
    >
    >  
    >
    > **Constraints:**
    >
    > - `1 <= s.length <= 1000`
    > - `s` consist of only digits and English letters (lower-case and/or upper-case),
    >
    > > The key point of the palindromic substring is the double pointers. 
    > >
    > > ```python
    > > class Solution:
    > >     def longestPalindrome(self, s: str) -> str:
    > >         max_len = float('-inf')
    > >         self.size = len(s)
    > >         self.s = s
    > >         self.max_len = 0
    > >         res = ''
    > >         for i in range(self.size):
    > >             s_1 = self.helper(i, i)
    > >             s_2 = self.helper(i, i + 1)
    > >             if len(s_1) > self.max_len:
    > >                 self.max_len = len(s_1)
    > >                 res = s_1
    > >             if len(s_2) > self.max_len:
    > >                 self.max_len = len(s_2)
    > >                 res = s_2
    > >         return res
    > >     def helper(self, left, right):
    > >         while left >= 0 and right < self.size and self.s[left] == self.s[right]:
    > >             left, right = left - 1, right + 1
    > >         return self.s[left + 1 : right]
    > >             
    > > ```

    

    19. > \132. Palindrome Partitioning II
        >
        > Given a string `s`, partition `s` such that every substring of the partition is a palindrome.
        >
        > Return *the minimum cuts needed* for a palindrome partitioning of `s`.
        >
        >  
        >
        > **Example 1:**
        >
        > ```
        > Input: s = "aab"
        > Output: 1
        > Explanation: The palindrome partitioning ["aa","b"] could be produced using 1 cut.
        > ```
        >
        > **Example 2:**
        >
        > ```
        > Input: s = "a"
        > Output: 0
        > ```
        >
        > **Example 3:**
        >
        > ```
        > Input: s = "ab"
        > Output: 1
        > ```
        >
        >  
        >
        > **Constraints:**
        >
        > - `1 <= s.length <= 2000`
        > - `s` consists of lower-case English letters only.
        >
        > ```python
        > '''
        > The key point of palindromic substring is the center and radius. I constructed a cut list to record the minimum cut to turn the substring s[:end] into all palindromics. Initialy, we could assign the number at index i of cut list to be i - 1 which is the maximum cuts to make it all palindromic substrings. After initialization, we need to find out the state transfer function. 
        > 
        > We could traverse the given list and see it as the center(odd length palindromic substring) or one of the two centers(even length palindromic substring). For example, if we found that a range centered at index i and the radius of which is j, we could get that cut[i + j + 1] = cut[i - j] + 1
        > '''
        > class Solution:
        >     def minCut(self, s: str) -> int:
        >         size = len(s)
        >         cut = [i - 1 for i in range(size + 1)]
        >         for i in range(size):
        >             j = 0
        >             while i - j >= 0 and i + j < size and s[i - j] == s[i + j]:
        >                 cut[i + j + 1] = min(cut[i + j + 1], 1 + cut[i - j])
        >                 j += 1
        >             j = 1
        >             while i - j + 1 >= 0 and i + j < size and s[i - j + 1] == s[i + j]:
        >                 cut[i + j + 1] = min(cut[i + j + 1], 1 + cut[i - j + 1])
        >                 j += 1
        >         return cut[size]
        > ```

    20. > \516. Longest Palindromic Subsequence
        >
        > Medium
        >
        > 2369195Add to ListShare
        >
        > Given a string s, find the longest palindromic subsequence's length in s. You may assume that the maximum length of s is 1000.
        >
        > **Example 1:**
        > Input:
        >
        > ```
        > "bbbab"
        > ```
        >
        > Output:
        >
        > ```
        > 4
        > ```
        >
        > One possible longest palindromic subsequence is "bbbb".
        >
        >  
        >
        > **Example 2:**
        > Input:
        >
        > ```
        > "cbbd"
        > ```
        >
        > Output:
        >
        > ```
        > 2
        > ```
        >
        > One possible longest palindromic subsequence is "bb".
        >
        >  
        >
        > **Constraints:**
        >
        > - `1 <= s.length <= 1000`
        > - `s` consists only of lowercase English letters.
        >
        
21. > \491. Increasing Subsequences
        >
    > Medium
        >
        > 798123Add to ListShare
        >
        > Given an integer array, your task is to find all the different possible increasing subsequences of the given array, and the length of an increasing subsequence should be at least 2.
        >
        >  
        >
        > **Example:**
        >
        > ```
        > Input: [4, 6, 7, 7]
        > Output: [[4, 6], [4, 7], [4, 6, 7], [4, 6, 7, 7], [6, 7], [6, 7, 7], [7,7], [4,7,7]]
        > ```
        >
        >  
        >
        > **Constraints:**
        >
        > - The length of the given array will not exceed 15.
        > - The range of integer in the given array is [-100,100].
        > - The given array may contain duplicates, and two equal integers should also be considered as a special case of increasing sequence.
        >
        > ```python
        > '''
        > DFS will do. The key point is to avoid repeated search. The most efficient way to avoid repeated search is skip the same number after the first appearance at the same level.
        > '''
        > class Solution:
        >     def findSubsequences(self, nums: List[int]) -> List[List[int]]:
        >         res = []
        >         if not nums: return res
        >         self.nums = nums
        >         self.helper([], res, 0)
        >         return res
        >     def helper(self, path, res, index):
        >         if index > len(self.nums):
        >             return
        >         if len(path) > 1: 
        >             res.append(path)
        >         for i in range(index, len(self.nums)):
        >             if i > index and self.nums[i] in self.nums[index:i]:
        >                 continue
        >             if not path or self.nums[i] >= path[-1]:
        >                 self.helper(path + [self.nums[i]], res, i + 1)
        > ```
    
    22. 
    
    
    
    

