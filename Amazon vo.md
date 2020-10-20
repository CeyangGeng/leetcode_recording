# Amazon vo

- ##### Description

  ```
  240. Search a 2D Matrix II
  Write an efficient algorithm that searches for a value in an m x n matrix. This matrix has the following properties:
  
  Integers in each row are sorted in ascending from left to right.
  Integers in each column are sorted in ascending from top to bottom.
  Example:
  
  Consider the following matrix:
  
  [
    [1,   4,  7, 11, 15],
    [2,   5,  8, 12, 19],
    [3,   6,  9, 16, 22],
    [10, 13, 14, 17, 24],
    [18, 21, 23, 26, 30]
  ]
  Given target = 5, return true.
  
  Given target = 20, return false.
  ```

  ##### Solution

  ```python
  # search from the right top corner element. If the target is larget than the current element, increase the row index; Else if target is smaller than the current element, decreasing the column index.
  class Solution:
      def searchMatrix(self, matrix, target):
          """
          :type matrix: List[List[int]]
          :type target: int
          :rtype: bool
          """
          if not matrix: return False
          m, n = len(matrix), len(matrix[0])
          i, j = 0, n - 1
          while 0 <= i < m and 0 <= j < n:
              if matrix[i][j] == target: return True
              if target < matrix[i][j]: j -= 1
              elif target > matrix[i][j]: i += 1
          return False
  ```

- ##### Description

  ```python
  Given a 2D board and a word, find if the word exists in the grid.
  
  The word can be constructed from letters of sequentially adjacent cells, where "adjacent" cells are horizontally or vertically neighboring. The same letter cell may not be used more than once.
  
   
  
  Example 1:
  
  
  Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED"
  Output: true
  Example 2:
  
  
  Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "SEE"
  Output: true
  Example 3:
  
  
  Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCB"
  Output: false
   
  
  Constraints:
  
  board and word consists only of lowercase and uppercase English letters.
  1 <= board.length <= 200
  1 <= board[i].length <= 200
  1 <= word.length <= 10^3
  ```

  ##### Solution

  ```python
  class Solution:
      def exist(self, board: List[List[str]], word: str) -> bool:
          if not word: return True
          if not board: return False
          m, n = len(board), len(board[0])
          for i in range(m):
              for j in range(n):
                  visited = {(i, j)}
                  if self.dfs(i, j, board, 0, word, visited, m, n): return True
          return False
      def dfs(self, x, y, board, index, word, visited, m, n):
          if index == len(word) - 1 and board[x][y] == word[index]: return True
          if word[index] != board[x][y]: return False
          for delta_x, delta_y in [(-1, 0), (1, 0), (0, -1), (0, 1)]:
              new_x, new_y = x + delta_x, y + delta_y
              if 0 <= new_x < m and 0 <= new_y < n and (new_x, new_y) not in visited:
                  visited.add((new_x, new_y))
                  if self.dfs(new_x, new_y, board, index + 1, word, visited, m, n): return True
                  visited.remove((new_x, new_y))
          return False
  ```

- Description

  ```python
  210. Course Schedule II
  Medium
  
  2811
  
  147
  
  Add to List
  
  Share
  There are a total of n courses you have to take labelled from 0 to n - 1.
  
  Some courses may have prerequisites, for example, if prerequisites[i] = [ai, bi] this means you must take the course bi before the course ai.
  
  Given the total number of courses numCourses and a list of the prerequisite pairs, return the ordering of courses you should take to finish all courses.
  
  If there are many valid answers, return any of them. If it is impossible to finish all courses, return an empty array.
  
   
  
  Example 1:
  
  Input: numCourses = 2, prerequisites = [[1,0]]
  Output: [0,1]
  Explanation: There are a total of 2 courses to take. To take course 1 you should have finished course 0. So the correct course order is [0,1].
  Example 2:
  
  Input: numCourses = 4, prerequisites = [[1,0],[2,0],[3,1],[3,2]]
  Output: [0,2,1,3]
  Explanation: There are a total of 4 courses to take. To take course 3 you should have finished both courses 1 and 2. Both courses 1 and 2 should be taken after you finished course 0.
  So one correct course order is [0,1,2,3]. Another correct ordering is [0,2,1,3].
  Example 3:
  
  Input: numCourses = 1, prerequisites = []
  Output: [0]
  ```

  ##### Solution

  ```python
  class Solution:
      def findOrder(self, numCourses: int, prerequisites: List[List[int]]) -> List[int]:
          degree = defaultdict(int)
          graph = defaultdict(list)
          for second, first in prerequisites:
              degree[second] += 1
              graph[first].append(second)
          path = []
          stack = []
          for i in range(numCourses):
              if degree[i] == 0:
                  stack.append(i)
          while stack:
              node = stack.pop()
              path.append(node)
              for neighbor in graph[node]:
                  degree[neighbor] -= 1
                  if degree[neighbor] == 0:
                      stack.append(neighbor)
          return path if len(path) == numCourses else []
  ```

- Description

  ```python
  380. Insert Delete GetRandom O(1)
  Implement the RandomizedSet class:
  
  bool insert(int val) Inserts an item val into the set if not present. Returns true if the item was not present, false otherwise.
  bool remove(int val) Removes an item val from the set if present. Returns true if the item was present, false otherwise.
  int getRandom() Returns a random element from the current set of elements (it's guaranteed that at least one element exists when this method is called). Each element must have the same probability of being returned.
  Follow up: Could you implement the functions of the class with each function works in average O(1) time?
  ```

  ##### Solution

  ```python
  class RandomizedSet:
  
      def __init__(self):
          """
          Initialize your data structure here.
          """
          self.nums = []
          self.dic = dict()
          
  
      def insert(self, val: int) -> bool:
          """
          Inserts a value to the set. Returns true if the set did not already contain the specified element.
          """
          if val not in self.dic:
              self.dic[val] = len(self.nums)
              self.nums.append(val)
              return True
          return False
          
  
      def remove(self, val: int) -> bool:
          """
          Removes a value from the set. Returns true if the set contained the specified element.
          """
          if val in self.dic:
              index = self.dic[val]
              self.nums[index] = self.nums[-1]
              self.dic[self.nums.pop()] = index
              del self.dic[val]
              return True
          return False
          
  
      def getRandom(self) -> int:
          """
          Get a random element from the set.
          """
          return self.nums[random.randint(0, len(self.nums) - 1)]
  ```

- ##### Description

  ```python
  146. LRU Cache
  Medium
  
  6840
  
  288
  
  Add to List
  
  Share
  Design a data structure that follows the constraints of a Least Recently Used (LRU) cache.
  
  Implement the LRUCache class:
  
  LRUCache(int capacity) Initialize the LRU cache with positive size capacity.
  int get(int key) Return the value of the key if the key exists, otherwise return -1.
  void put(int key, int value) Update the value of the key if the key exists. Otherwise, add the key-value pair to the cache. If the number of keys exceeds the capacity from this operation, evict the least recently used key.
  Follow up:
  Could you do get and put in O(1) time complexity?
  ```

  ##### Solution

  ```python
  ### call the python library OrderedDict
  ### noting: there are two capacity: the required capacity and current capacity. When putting the key: if the key exists in the dictionary, update the key value pair and move the key to the end of the ordereddict.(The latter one is easy to be neglected);else if the key does not exist, determine whether the length of the dictioanry is amount to the required capacity, if it is, pop out the least recently used key value pair. after this check, put the key value pair into the dictionary. When getting the key value pair, after getting the key, move the key to the end of the ordereddict because it is the most recently used item.
  from collections import OrderedDict
  class LRUCache:
  
      def __init__(self, capacity: int):
          self.dic = OrderedDict()
          self.capacity = capacity
          self.cur_capacity = 0
          
  
      def get(self, key: int) -> int:
          if key in self.dic: 
              val = self.dic[key]
              self.dic.move_to_end(key, last = True)
              return val
          return -1
          
  
      def put(self, key: int, value: int) -> None:
          if key in self.dic: 
              self.dic[key] = value
              self.dic.move_to_end(key, last = True)
          else:
              if self.cur_capacity == self.capacity:
                  self.dic.popitem(last = False)
                  self.cur_capacity -= 1
              self.dic[key] = value
              self.cur_capacity += 1
              
  #############################################################################
  '''
  using the doubly linked list to record the refer time, the more near to the head, the more least recently used. use the dictionary to match the node key value and node.
  Besides, there are two kind of space: the dictionary space and linked list space. As long as the node is not removed from the linked list, we do not need to care the first remove(delete the dictionary key) and then add process(add the dictionary key). The only case we need to delete the dictionary key is when pop the least recently used node. We only need to match the node key value and the node. The change of the position of the node in the linked list has no impact on the dictionary.
  '''
  class Node:
      def __init__(self, key, val):
          self.key = key
          self.val = val
          self.pre = None
          self.next = None
          
  class LRUCache:
  
      def __init__(self, capacity: int):
          self.head = Node(0, 0)
          self.tail = Node(0, 0)
          self.head.next = self.tail
          self.tail.pre = self.head
          self.capacity = capacity
          self.dic = dict()       
          
  
      def get(self, key: int) -> int:
          if key in self.dic:
              node = self.dic[key]
              self.remove_node(node)
              self.insert_tail(node)
              return node.val
          return -1
          
  
      def put(self, key: int, value: int) -> None:
          if key in self.dic:
              node = self.dic[key]
              self.remove_node(node)
          node = Node(key, value)
          self.dic[key] = node
          self.insert_tail(node)
          if len(self.dic) > self.capacity:
              n = self.remove_head()
              del self.dic[n.key]
      
      def remove_node(self, node):
          node.pre.next = node.next
          node.next.pre = node.pre
      
      def remove_head(self):
          temp = self.head.next
          self.head.next = self.head.next.next
          self.head.next.pre = self.head
          return temp
          
      def insert_tail(self, node):
          self.tail.pre.next = node
          node.pre = self.tail.pre
          node.next = self.tail
          self.tail.pre = node
  ```

- ##### Description

  ```python
  1253. Reconstruct a 2-Row Binary Matrix
  Medium
  
  154
  
  15
  
  Add to List
  
  Share
  Given the following details of a matrix with n columns and 2 rows :
  
  The matrix is a binary matrix, which means each element in the matrix can be 0 or 1.
  The sum of elements of the 0-th(upper) row is given as upper.
  The sum of elements of the 1-st(lower) row is given as lower.
  The sum of elements in the i-th column(0-indexed) is colsum[i], where colsum is given as an integer array with length n.
  Your task is to reconstruct the matrix with upper, lower and colsum.
  
  Return it as a 2-D integer array.
  
  If there are more than one valid solution, any of them will be accepted.
  
  If no valid solution exists, return an empty 2-D array.
  ```

  ##### Solution

  ```python
  ### first dfs version, tle
  class Solution:
      def reconstructMatrix(self, upper: int, lower: int, colsum: List[int]) -> List[List[int]]:
          n = len(colsum)
          memo = dict()
          def dfs(first_row_sum, second_row_sum, index):
              if index == n:
                  if first_row_sum == upper and second_row_sum == lower:
                      return (True, [[], []])
                  return (False, [])
              if first_row_sum > upper or second_row_sum > lower:
                  return (False, [])
              if (first_row_sum, second_row_sum, index) in memo: return memo[(first_row_sum,second_row_sum, index)]
              for i in range(2):
                  if 0 <= colsum[index] - i <= 1:
                      next_bool, next_res = dfs(first_row_sum + i, second_row_sum + colsum[index] - i, index + 1)
                      if next_bool:
                          memo[(first_row_sum, second_row_sum, index)] = (True, [[i] + next_res[0], [colsum[index] - i] + next_res[1]])
                          return memo[(first_row_sum, second_row_sum, index)]
                      
              return (False, [])
          return dfs(0, 0, 0)[1]
          
          
  ############## greedy version #################################3
  '''
  if the current column sum is 1, we should assgin the 1 to the larger sum row. if the current column sum is 2, there is only one case where we should assgin 1 to both column.
  '''
  class Solution:
      def reconstructMatrix(self, upper: int, lower: int, colsum: List[int]) -> List[List[int]]:
          n = len(colsum)
          res = [[0] * n for _ in range(2)]
          for i, v in enumerate(colsum):
              if v == 1:
                  if upper > lower:
                      res[0][i] = 1
                      upper -= 1
                  else:
                      res[1][i] = 1
                      lower -= 1
              elif v == 2:
                  res[0][i] = 1
                  res[1][i] = 1
                  upper -= 1
                  lower -= 1
          return res if upper == 0 and lower == 0 else []
  ```

- Description

  ```python
  505. The Maze II
  Medium
  
  648
  
  30
  
  Add to List
  
  Share
  There is a ball in a maze with empty spaces and walls. The ball can go through empty spaces by rolling up, down, left or right, but it won't stop rolling until hitting a wall. When the ball stops, it could choose the next direction.
  
  Given the ball's start position, the destination and the maze, find the shortest distance for the ball to stop at the destination. The distance is defined by the number of empty spaces traveled by the ball from the start position (excluded) to the destination (included). If the ball cannot stop at the destination, return -1.
  
  The maze is represented by a binary 2D array. 1 means the wall and 0 means the empty space. You may assume that the borders of the maze are all walls. The start and destination coordinates are represented by row and column indexes.
  ```

  ##### Solution

  ```python
  import heapq
  class Solution:
      def shortestDistance(self, maze: List[List[int]], start: List[int], destination: List[int]) -> int:
          m, n = len(maze), len(maze[0])
          start_x, start_y = start
          queue = [(0, start_x, start_y)]
          dic = {(start_x, start_y):0}
          
          while queue:
              distance, x, y = heapq.heappop(queue)
              if [x, y] == destination: return distance
              for delta_x, delta_y in ((-1, 0), (1, 0), (0, -1), (0, 1)):
                  new_x, new_y, d = x, y, 0
                  while 0 <= new_x + delta_x < m and 0 <= new_y + delta_y < n and maze[new_x + delta_x][new_y + delta_y] != 1:
                      new_x += delta_x
                      new_y += delta_y
                      d += 1
                  if (new_x, new_y) not in dic or distance + d < dic[(new_x, new_y)]:
                      dic[(new_x, new_y)] = distance + d
                      heapq.heappush(queue, (distance + d, new_x, new_y))
          return -1
  ```

- ##### Description

  ```python
  632. Smallest Range Covering Elements from K Lists
  Hard
  
  1167
  
  25
  
  Add to List
  
  Share
  You have k lists of sorted integers in non-decreasing order. Find the smallest range that includes at least one number from each of the k lists.
  
  We define the range [a, b] is smaller than range [c, d] if b - a < d - c or a < c if b - a == d - c.
  
   
  
  Example 1:
  
  Input: nums = [[4,10,15,24,26],[0,9,12,20],[5,18,22,30]]
  Output: [20,24]
  Explanation: 
  List 1: [4, 10, 15, 24,26], 24 is in range [20,24].
  List 2: [0, 9, 12, 20], 20 is in range [20,24].
  List 3: [5, 18, 22, 30], 22 is in range [20,24].
  ```

  ##### Solution

  ```python
  ######################### my initial solution ####################################
  '''
  Thinking path: We should keep a pointers array the elements of which indicating the cuurent index of the pointer for each row. Initialy, I initialize the pointers to be all zero. For each pointer index combination, we should find out the maximum value and the minimum value and check whether this range is smaller than the current smallest range.After the checking, we should move the pointer of the smallest value forward for one step. When the smallest value pointer points to the last position of the row, we should break this while loop because there is no need to traverse further since the rows are in ascending order.
  '''
   
  import heapq
  class Solution:
      def smallestRange(self, nums: List[List[int]]) -> List[int]:
          m = len(nums)
          reach_row_ends = 0
          min_pointers, max_pointers = [], []
          heapq.heapify(min_pointers)
          heapq.heapify(max_pointers)
          min_range_len = float('inf')
          min_x = min_y = max_x = max_y = -1
          min_range = []
          for i in range(m):
              heapq.heappush(min_pointers, (nums[i][0], i, 0))
              heapq.heappush(max_pointers, (-nums[i][0], i, 0))
          while reach_row_ends < 1:
              min_val, min_x, min_y = min_pointers[0]
              max_val, max_x, max_y = max_pointers[0]
              max_val *= -1
              if max_val - min_val < min_range_len or (max_val - min_val == min_range_len and min_val < min_range[0]):
                  min_range_len = max_val - min_val
                  min_range = [min_val, max_val]
                  
              if min_y < len(nums[min_x]) - 1:
                  next_val, x, y = nums[min_x][min_y + 1], min_x, min_y + 1
                  a,b,c = heapq.heappop(min_pointers)
                  max_pointers.remove((-a,b,c))
                  heapq.heappush(min_pointers, (next_val, x, y))
                  heapq.heappush(max_pointers, (-next_val, x, y))
              if min_y == len(nums[min_x]) - 1:
                  reach_row_ends += 1
          if max_val - min_val < min_range_len:
              min_range = [min_val, max_val]     
              
          return min_range
      
  ################## improved version######################################
  '''
  Since the array is in ascending order, we do not need a priority queue to record the maximum value, just updating the maximum value whenever move forward the pointer. However, we still need a priority queue to record the minimum value. We should end the comparing when the minimum value comes to the end of that row.
  '''
  import heapq
  class Solution:
      def smallestRange(self, nums: List[List[int]]) -> List[int]:
          pq = [(row[0], i, 0) for i, row in enumerate(nums)]
          heapq.heapify(pq)
          right = max([row[0] for row in nums])
          min_range = [float('-inf'), float('inf')]
          while pq:
              left, min_x_index, min_y_index = heapq.heappop(pq)
              if right - left < min_range[1] - min_range[0] or (right - left == min_range[1] - min_range[0] and left < min_range[0]):
                  min_range = [left, right]
              if min_y_index == len(nums[min_x_index]) - 1:
                  return min_range
              v = nums[min_x_index][min_y_index + 1]
              right = max(right, v)
              heapq.heappush(pq, (v, min_x_index, min_y_index + 1))
  ```

- ##### Description

  ```python
  362. Design Hit Counter
  Medium
  
  852
  
  84
  
  Add to List
  
  Share
  Design a hit counter which counts the number of hits received in the past 5 minutes.
  
  Each function accepts a timestamp parameter (in seconds granularity) and you may assume that calls are being made to the system in chronological order (ie, the timestamp is monotonically increasing). You may assume that the earliest timestamp starts at 1.
  
  It is possible that several hits arrive roughly at the same time.
  ```

  ##### Solution

  ```python
  class HitCounter:
  
      def __init__(self):
          """
          Initialize your data structure here.
          """
          self.time, self.dic = [], defaultdict(int)
          
  
      def hit(self, timestamp: int) -> None:
          """
          Record a hit.
          @param timestamp - The current timestamp (in seconds granularity).
          """
          self.time.append(timestamp)
          self.dic[timestamp] = len(self.time)
          
          
  
      def getHits(self, timestamp: int) -> int:
          """
          Return the number of hits in the past 5 minutes.
          @param timestamp - The current timestamp (in seconds granularity).
          """
          left, right = 0, len(self.time)
          t2 = self.binary_search(left, right, timestamp)
          t1 = self.binary_search(left, right, timestamp - 300)
          return self.dic[t2] - self.dic[t1]
      
      def binary_search(self, left, right, target):
          
          while left < right:
              mid = left + (right - left) // 2
              if self.time[mid] <= target:
                  left = mid + 1
              else:
                  right = mid
          return self.time[left - 1] if left - 1 >= 0 else 0
  ```

- ##### Description

  ```python
  472. Concatenated Words
  Hard
  
  899
  
  121
  
  Add to List
  
  Share
  Given a list of words (without duplicates), please write a program that returns all concatenated words in the given list of words.
  A concatenated word is defined as a string that is comprised entirely of at least two shorter words in the given array.
  
  Example:
  Input: ["cat","cats","catsdogcats","dog","dogcatsdog","hippopotamuses","rat","ratcatdogcat"]
  
  Output: ["catsdogcats","dogcatsdog","ratcatdogcat"]
  
  Explanation: "catsdogcats" can be concatenated by "cats", "dog" and "cats"; 
   "dogcatsdog" can be concatenated by "dog", "cats" and "dog"; 
  "ratcatdogcat" can be concatenated by "rat", "cat", "dog" and "cat".
  Note:
  The number of elements of the given array will not exceed 10,000
  The length sum of elements in the given array will not exceed 600,000.
  All the input string will only include lower case letters.
  The returned elements order does not matter.
  ```

  ##### Solution

  ```python
  class Solution:
      
      def construct(self):
          for word in self.words:
              if not word: continue
              t = self.trie
              for w in word:
                  t = t.setdefault(w, {})
              t['#'] = {}
              
      def findAllConcatenatedWordsInADict(self, words: List[str]) -> List[str]:
          self.words = words
          self.trie = {}
          self.construct()
          self.res = []
          for word in self.words:
              self.dfs(word, 0, 0, self.trie)
          return self.res
      
      def dfs(self, word, index, count, trie):
          if index == len(word):
              if '#' in trie:
                  count += 1
                  if count >= 2:
                      self.res.append(word)
                      return True
                  return False
              return False
          if '#' in trie:
              if self.dfs(word, index, count + 1, self.trie):
                  return True
          if word[index] in trie:
              if self.dfs(word, index + 1, count, trie[word[index]]): return True
          return False
  ```

- ##### Description

  ```python
  759. Employee Free Time
  Hard
  
  625
  
  48
  
  Add to List
  
  Share
  We are given a list schedule of employees, which represents the working time for each employee.
  
  Each employee has a list of non-overlapping Intervals, and these intervals are in sorted order.
  
  Return the list of finite intervals representing common, positive-length free time for all employees, also in sorted order.
  
  (Even though we are representing Intervals in the form [x, y], the objects inside are Intervals, not lists or arrays. For example, schedule[0][0].start = 1, schedule[0][0].end = 2, and schedule[0][0][0] is not defined).  Also, we wouldn't include intervals like [5, 5] in our answer, as they have zero length.
  ```

  ##### Solution

  ```python
  class Solution:
      def employeeFreeTime(self, schedule: '[[Interval]]') -> '[Interval]':
          m = len(schedule)
          res = []
          heap = [(v[0].start, v[0].end, i, 0) for i, v in enumerate(schedule)]
          heapq.heapify(heap)
          while heap:
              start, end, row, col = heapq.heappop(heap)
              #print(start, end, row, col)
              if not res: res.append([start, end])
              else:
                  if start <= res[-1][-1]:
                      res[-1][-1] = max(res[-1][-1], end)
                  else:
                      res.append([start, end])
              if col < len(schedule[row]) - 1:
                  col += 1
                  heapq.heappush(heap, (schedule[row][col].start, schedule[row][col].end, row, col))
          if len(res) == 1: return []
          final = []
          print("the res is", res)
          for i in range(1, len(res)):
              print("the i is", i)
              print("the first ele is", res[i - 1][1])
              print("the second ele is", res[i][0])
              a, b = res[i - 1][1], res[i][0]
              inter = Interval(a, b)
              final.append(inter)
          return final
  ```

- ##### Description

  ```python
  84. Largest Rectangle in Histogram
  Hard
  
  4428
  
  93
  
  Add to List
  
  Share
  Given n non-negative integers representing the histogram's bar height where the width of each bar is 1, find the area of largest rectangle in the histogram.
  
   
  
  
  Above is a histogram where width of each bar is 1, given height = [2,1,5,6,2,3].
  
   
  
  
  The largest rectangle is shown in the shaded area, which has area = 10 unit.
  
   
  
  Example:
  
  Input: [2,1,5,6,2,3]
  Output: 10
  ```

  ##### Solution

  ```python
  '''
  Keep a ascending monotonic queue to record the previous shorter rectangle index. Whenever push a new index into the stack, we should pop out all the previous index the height of which is larger than the height of curren index. The width of the popped height is i - (previous index before the index to be popped) - 1.
  '''
  class Solution:
      def largestRectangleArea(self, heights: List[int]) -> int:
          heights.append(0)
          stack = [-1]
          res = 0
          for i in range(len(heights)):
              while heights[i] < heights[stack[-1]]:
                  h = heights[stack.pop()]
                  w = i - stack[-1] - 1
                  res = max(res, h * w)
              stack.append(i)
          return res
  ```

- ##### Description

  ```
  label system: https://leetcode.com/discuss/interview-question/893442/
  ```

  ##### Solution

  ```python
  '''
  Greedy solution: try to add the largest character, if the number of the  consecutive  current  largest character is larger than the character limit, we should find the next largest character and use it to separate the long consecutive character. For example, if the character counter of the original label string is "bbbbba" and the character limit is 2, after adding the first two alpha b to the result, the next added character shold not be b anymore, we should find the next largest character which is a to separate the consecutive character b, so the result should be "bbabb".
  '''
  from collections import Counter
  import heapq
  def label_system(original_label, char_limit):
      # the order of character 'a' is 97, 'z' is 122
      # recording the frequency of different characters
      char_counter = [0] * 26
      for ch in original_label:
          char_counter[ord(ch) - ord('a')] += 1
      #print(char_counter)
      res = []
      for i in range(25, -1, -1):
          count = 0
          while char_counter[i] > 0:
              res.append(chr(ord('a') + i))
              char_counter[i] -= 1
              count += 1
              if char_counter[i] > 0 and count == char_limit:
                  next_char = find_next_char(char_counter, i)
                  if not next_char: return ''.join(res)
                  res.append(next_char)
                  char_counter[ord(next_char) - ord('a')] -= 1
                  count = 0
      return ''.join(res)
  
  def find_next_char(char_counter, start_index):
      next_char_index = -1
      for i in range(start_index - 1, -1, -1):
          if char_counter[i] > 0:
              next_char_index = i
              break
      res = None
      if next_char_index >= 0:
          res = chr(ord('a') + i)
      return res
  
  
  if __name__ == "__main__":
      original_label = 'fjasdfjoairehqofdnvmzvnzlalurqo'
      r = label_system(original_label, 2)
      print(r)
  ```

- ##### Description

  ```python
  221. Maximal Square
  ```

  ##### Solution

  ```python
  class Solution:
      def maximalSquare(self, matrix: List[List[str]]) -> int:
              if not matrix: return 0
              m, n = len(matrix), len(matrix[0])
              dp = [[0] * (n + 1) for _ in range(m + 1)]
              longest = float('-inf')
              for i in range(1, m + 1):
                  for j in range(1, n + 1):
                      if matrix[i - 1][j - 1] == '1':
                          dp[i][j] = min(dp[i - 1][j], dp[i][j - 1], dp[i - 1][j - 1]) + 1
                          longest = max(longest, dp[i][j])
              return longest ** 2 if longest > float('-inf') else 0
  ```

- ##### Description

  ```
  85. Maximal Rectangle
  ```

  ##### Solution

  ```python
  def max_rectangle(matrix):
      if not matrix: return 0
      n = len(matrix[0])
      heights = [0] * (n + 1)
      res = 0
      for row in matrix:
          for i in range(n):
              heights[i] = heights[i] + 1 if row[i] == 1 else 0
          stack = [-1]
          for j in range(n + 1):
              while stack and heights[j] < heights[stack[-1]]:
                  h = heights[stack.pop()]
                  w = j - stack[-1] - 1
                  area = h * w
                  res = max(res, area)
              stack.append(j)
      return res
  
  if __name__ == "__main__":
      matrix = [[1, 0, 1, 0, 0], [1,0,1,1,1],[1,1,1,1,1],[1,0,0,1,0]]
      res = max_rectangle(matrix)
      print(res)
  ```

- ##### Description

  ```
  198. House Robber
  ```

  ##### Solution

  ```python
  class Solution:
      def rob(self, nums: List[int]) -> int:
          stole, not_stole = 0, 0
          for num in nums:
              temp = not_stole
              not_stole = max(stole, not_stole)
              stole = num + temp
          return max(stole, not_stole)
  ```

- ##### Description

  ```
  20. Valid Parentheses
  ```

  ##### Solution

  ```python
  class Solution:
      def isValid(self, s: str) -> bool:
          stack = []
          right_parentheses = {')', ']', '}'}
          match_dic = {')':'(', ']':'[', '}':'{'}
          for ch in s:
              if stack and ch in right_parentheses and stack[-1] == match_dic[ch]:
                  stack.pop()
                  continue
              stack.append(ch)
          return not stack
  ```

  ##### Follow up

  ```
  '*' can represent any kind of parentheses, how to solve it?
  similar to 678. Valid Parenthesis String
  ```

  ##### Solution

  ```python
  ######################### my initial tle version ##############################
  class Solution:
      def checkValidString(self, s: str) -> bool:
          stack = []
          index = 0
          return self.helper(index, stack, s)
  
      def helper(self, index, stack, s):
          if index == len(s):
              return not stack
          if s[index] == '(':
              if self.helper(index + 1, stack + ['('], s):
                  return True
          if s[index] == ')':
              if stack and stack[-1] == '(':
                  stack.pop()
                  if self.helper(index + 1, stack, s):
                      return True
                  stack.append('(')
          if s[index] == '*':
              # '*' represents the '('
              if self.helper(index + 1, stack + ['('], s): return True
              # '*' represents the empty space
              if self.helper(index + 1, stack, s): return True
              # '*' represents the ')'
              if stack and stack[-1] == '(':
                  stack.pop()
                  if self.helper(index + 1, stack, s): return True
                  stack.append('(')
          return False
  ################################ improved version #############################
  # only ()
  class Solution:
      def checkValidString(self, s: str) -> bool:
          cmin, cmax = 0, 0
          for i in s:
              if i == '(':
                  cmin += 1
                  cmax += 1
              if i == ')':
                  cmax -= 1
                  cmin = max(0, cmin - 1)
              if i == '*':
                  cmax += 1
                  cmin = max(0, cmin - 1)
              if cmax < 0: return False
          return cmin == 0
  ########################### ()[]}{} all included ###########################
  left = {'(', '[', '{'}
  right = {')', ']', '}'}
  match = {')':'(', "]":'[', '}':'{'}
  def valid_parenthesis(string):
      stack = []
      return helper(string, 0, stack)
  
  def helper(string, index, stack):
      if index == len(string):
          while stack and stack[-1] == '*':
              if len(stack) == 1: return True
              stack.pop()
              stack.pop()
          return not stack
      if string[index] in left:
          if helper(string, index + 1, stack + [string[index]]):
              return True
      if string[index] in right:
          if helper(string, index + 1, stack[:-1]):
              return True
      if string[index] == '*':
          if helper(string, index + 1, stack[:-1]):
              return True
          if helper(string, index + 1, stack + ['*']):
              return True
          if helper(string, index + 1, stack):
              return True
      return False
  if __name__ == "__main__":
      s = "***())]"
      res = valid_parenthesis(s)
      print(res)
  ```

- ##### Description

  ```
  127. Word Ladder
  ```

  ##### Solution

  ```python
  from collections import deque
  class Solution:
      def ladderLength(self, beginWord: str, endWord: str, wordList: List[str]) -> int:
          wordList = set(wordList)
          #wordList.add(endWord)
          queue = deque([[beginWord, 1]])
          while queue:
              word, length = queue.popleft()
              if word == endWord:
                  return length
              for i in range(len(word)):
                  for s in "abcdefghijklmnopqrstuvwxyz":
                      temp = word[:i] + s + word[i + 1 :]
                      if temp in wordList:
                          wordList.remove(temp)
                          queue.append([temp, length + 1])
          return 0
  ```

- ##### Description

  ```python
  87. Scramble String
  ```

  ##### Solution

  ```python
  class Solution:
      def isScramble(self, s1: str, s2: str) -> bool:
          m, n = len(s1), len(s2)
          if m != n or sorted(s1) != sorted(s2): return False
          if m < 4 or s1 == s2: return True
          f = self.isScramble
          for i in range(1, m):
              if f(s1[:i], s2[:i]) and f(s1[i:], s2[i:]) or \
                      f(s1[:i], s2[-i :]) and f(s1[i:], s2[:-i]):
                  return True
          return False
  ```

- ##### Description

  ```
  994. Rotting Oranges
  ```

  ##### Solution

  ```python
  from collections import deque
  class Solution:
      def orangesRotting(self, grid: List[List[int]]) -> int:
          if not grid: return 0
          m, n = len(grid), len(grid[0])
          queue = deque()
          for i in range(m):
              for j in range(n):
                  if grid[i][j] == 2:
                      queue.append((i, j, 0))
          res = float('-inf')
          while queue:
              x, y, time = queue.popleft()
              res = max(res, time)
              for delta_x, delta_y in [(-1, 0), (1, 0), (0, 1), (0, -1)]:
                  new_x, new_y = x + delta_x, y + delta_y
                  if 0 <= new_x < m and 0 <= new_y < n and grid[new_x][new_y] == 1:
                      grid[new_x][new_y] = 2
                      queue.append((new_x, new_y, time + 1))
          for i in range(m):
              for j in range(n):
                  if grid[i][j] == 1:
                      return -1
          return res if res > float('-inf') else 0
  ```

- ##### Description

  ```python
  692. Top K Frequent Words
  ```

  ##### Solution

  ```python
  # using python built in function, O(nlogn) time complexity
  from collections import Counter
  class Solution:
      def topKFrequent(self, words: List[str], k: int) -> List[str]:
          counter = Counter(words)
          counter = sorted(counter.items(), key = lambda x: (-x[1], x[0]))
          res = []
          return [item[0] for item in counter[:k]]
  
  # another version without the built in function, O(nlogk) time complexity
  '''
  implement a node class which has two properties word and count. Besides, we should also implement the __lt__(self, other)(I think lt means less than) and __eq__(self, other) function. We should stipulate the sorting order the self is less than the other. The heap could help us find the n largest elements.
  '''
  from collections import Counter
  import heapq
  import functools
  
  class Node:
      def __init__(self, word, count):
          self.word = word
          self.count = count
      def __lt__(self, other):
          if self.count == other.count:
              return self.word > other.word
          return self.count < other.count
      def __eq__(self, other):
          return self.count == other.count and self.word == other.word
  
  class Solution:
      def topKFrequent(self, words: List[str], k: int) -> List[str]:
          counter = Counter(words)
          res = []
          heapq.heapify(res)
          for key, val in counter.items():
              heapq.heappush(res, Node(key, val))
              if len(res) > k:
                  heapq.heappop(res)
          r = []
          for _ in range(k):
              r.append(heapq.heappop(res).word)
          return r[::-1]
  
  ```

- ##### Description

  ```
  139. Word Break
  ```

  ##### Solution

  ```python
  class Solution:
      def wordBreak(self, s: str, wordDict: List[str]) -> bool:
          if not s: return True
          if not wordDict: return False
          wordDict = set(wordDict)
          memo = dict()
          return self.helper(s, wordDict, 0, memo)
      def helper(self, s, wordDict, start, memo):
          if start == len(s): return True
          if start in memo: return memo[start]
          for end in range(start, len(s)):
              temp = s[start : end + 1]
              if temp in wordDict:
                  if self.helper(s, wordDict, end + 1, memo):
                      memo[start] = True
                      return True
          memo[start] = False
          return False
  ```

- ##### Description

  ```python
  Coding: 给一个2darray类似于[[0,1], [1,1], ..]代表locker的位置，然后再给定两个值代表一个2d matrix的大小Rows，Cols
  需要返回一个2d的matrix来计算每一个点对于给定locker的最小距离
  例子：[[1,1]], 3,3
  0 0 0     2 1 2
  0 0 0 -> 1 0 1
  0 0 0     2 1 2
  ```

  ##### Solution

  ```python
  from collections import deque
  def min_distance(row, col, lockers):
      matrix = [[0] * col for _ in range(row)]
      queue = deque()
      visited = set()
      for locker in lockers:
          queue.append(locker + [0])
          visited.add(tuple(locker))
      m, n = len(matrix), len(matrix[0])
      while queue:
          x, y, step = queue.popleft()
          matrix[x][y] = step
          for delta_x, delta_y in [(-1, 0), (1, 0), (0, -1), (0, 1)]:
              new_x, new_y = x + delta_x, y + delta_y
              if 0 <= new_x < m and 0 <= new_y < n and (new_x, new_y) not in visited:
                  visited.add((new_x, new_y))
                  queue.append([new_x, new_y, step + 1])
      return matrix
  if __name__ == "__main__":
      res = min_distance(3,3,[[1,1]])
      print(res)
  
  ```

- ##### Description

  ```
  1143. Longest Common Subsequence
  ```

  ##### Solution

  ```python
  class Solution:
      def longestCommonSubsequence(self, text1: str, text2: str) -> int:
          size_1, size_2 = len(text1), len(text2)
          dp = [[0] * (size_2 + 1) for _ in range(size_1 + 1)]
          for i in range(1, size_1 + 1):
              for j in range(1, size_2 + 1):
                  if text1[i - 1] == text2[j - 1]:
                      dp[i][j] = dp[i - 1][j - 1] + 1
                  else:
                      dp[i][j] = max(dp[i][j - 1], dp[i - 1][j])
          return dp[-1][-1]
  ```

- ##### Description

  ```python
  451. Sort Characters By Frequency
  ```

  ##### Solution

  ```python
  from collections import Counter
  class Solution:
      def frequencySort(self, s: str) -> str:
          counter = Counter(s)
          temp = sorted(counter.items(), key = lambda x: (x[1]), reverse = True)
          res = ''
          for character, frequency in temp:
              res += character * frequency
          return res
  ```

- ##### Description

  ```
  238. Product of Array Except Self
  ```

  ##### Solution

  ```python
  class Solution:
      def productExceptSelf(self, nums: List[int]) -> List[int]:
          res = [1]
          product = 1
          size = len(nums)
          for i in range(size - 1):
              product *= nums[i]
              res.append(product)
          product = 1
          for i in range(size - 2, -1, -1):
              product *= nums[i + 1]
              res[i] *= product
          return res
  ```

- ##### Description

  ```python
  207. Course Schedule
  ```

  ##### Solution

  ```python
  from collections import defaultdict
  class Solution:
      def canFinish(self, numCourses: int, prerequisites: List[List[int]]) -> bool:
          graph = defaultdict(list)
          degree = defaultdict(int)
          for second, first in prerequisites:
              degree[second] += 1
              graph[first].append(second)
          queue = deque()
          for i in range(numCourses):
              if degree[i] == 0: queue.append(i)
          count = 0
          while queue:
              node = queue.popleft()
              count += 1
              for neighbor in graph[node]:
                  degree[neighbor] -= 1
                  if degree[neighbor] == 0:
                      queue.append(neighbor)
          return count == numCourses
  ```

- ##### Description

  ```python
  285. Inorder Successor in BST
  ```

  ##### Solution

  ```python
  class Solution:
      def inorderSuccessor(self, root: 'TreeNode', p: 'TreeNode') -> 'TreeNode':
          if not root: return None
          node = root.left
          while node and node.right:
              node = node.right
          if p == node: return root
          if p == root:
              node = root.right
              while node and node.left:
                  node = node.left
              return node          
          if p.val < root.val: return self.inorderSuccessor(root.left, p)
          if p.val > root.val: return self.inorderSuccessor(root.right, p)
   ########################### a more clean version ##########################
  class Solution:
      def inorderSuccessor(self, root: 'TreeNode', p: 'TreeNode') -> 'TreeNode':
          if not root: return None
          if root.val > p.val: return self.inorderSuccessor(root.left, p) or root
          else: return self.inorderSuccessor(root.right, p)
  ```

- ##### Description

  ```
  510. Inorder Successor in BST II
  ```

  ##### Solution

  ```python
  class Solution:
      def inorderSuccessor(self, node: 'Node') -> 'Node':
          if not node: return None
          # firstly see the node as the root
          if node.right:
              temp = node.right
              while temp and temp.left:
                  temp = temp.left
              return temp
          # secondly see the node as the right most node of the left subtree
          else:
              while node.parent and node.parent.right == node:
                  node = node.parent
              if node.parent and node.parent.left == node:
                  return node.parent
              return None
  ```

- ##### Description

  ```
  449. Serialize and Deserialize BST
  ```

  ##### Solution

  ```python
  '''
  While serializing the BST, we should use a res list to record the encoded string and a queue to record the nodes.
  If the node is not None, we should add both the node.left and node.right to the queue regardless of whether the node.left or the node.right is empty. If the node is None, we do not need to add the empty node into the queue. If the popped node is None, we should add '#' to mark this empty node. 
  while deserializing the BST, we should keep a queue to record the node at the same level and install the node.left and node.right one by one from the data list and add the non-empty children node to the next level queue.
  '''
  from collections import deque
  class Codec:
  
      def serialize(self, root: TreeNode) -> str:
          """Encodes a tree to a single string.
          """
          queue = deque()
          res = []
          queue.append(root)
          while queue:
              node = queue.popleft()
              if node: res.append(str(node.val))
              else: res.append('#')
              if node:
                  queue.append(node.left)
                  queue.append(node.right)
          return ' '.join(res)        
  
      def deserialize(self, data: str) -> TreeNode:
          """Decodes your encoded data to tree.
          """
          data = data.split(' ')
          if data[0] == '#': return None
          root = TreeNode(int(data.pop(0)))
          queue = deque([root])
          while queue:
              temp = []
              for node in queue:
                  if data:
                      t = data.pop(0)
                      if t != '#':
                          n = TreeNode(t)
                          temp.append(n)
                          node.left = n
                  if data:
                      t = data.pop(0)
                      if t != '#':
                          n = TreeNode(t)
                          temp.append(n)
                          node.right = n
              queue = temp
          return root
  ```

- ##### Description

  ```
  297. Serialize and Deserialize Binary Tree
  ```

  ##### Solution

  ```python
  from collections import deque
  class Codec:
      def serialize(self, root):
          """Encodes a tree to a single string.
          
          :type root: TreeNode
          :rtype: str
          """
          queue = deque([root])
          res = []
          while queue:
              node = queue.popleft()
              if not node: res.append('#')
              else: res.append(str(node.val))
              if node:
                  queue.append(node.left)
                  queue.append(node.right)
          return ' '.join(res)
          
  
      def deserialize(self, data):
          """Decodes your encoded data to tree.
          
          :type data: str
          :rtype: TreeNode
          """
          # print(data)
          data = data.split(' ')
          temp = data.pop(0)
          root = None
          if temp == '#': return None
          else: root = TreeNode(int(temp))
          queue = [root]
          while queue:
              temp = []
              for node in queue:
                  if data:
                      t = data.pop(0)
                      if t != '#':
                          n = TreeNode(int(t))
                          node.left = n
                          temp.append(n)
                  if data:
                      t = data.pop(0)
                      if t != '#':
                          n = TreeNode(int(t))
                          node.right = n
                          temp.append(n)
              queue = temp
          return root
  ```

- ##### Description

  ```
  121. Best Time to Buy and Sell Stock
  ```

  ##### Solution

  ```python
  class Solution:
      def maxProfit(self, prices: List[int]) -> int:
          size = len(prices)
          if size < 2: return 0
          max_profit = 0
          min_price = prices[0]
          for price in prices[1:]:
              if price < min_price:
                  min_price = price
              else:
                  max_profit = max(max_profit, price - min_price)
          return max_profit
      
  ##################################################################################
  follow up：如果job都有权重，如何安排可使总权重最大????????????? how to?
  ```

- ##### Description

  ```python
  算组合数，给定n, r，求C(n, r)，我当时忘了C(n, r) = C(n - 1, r) + C(n - 1, r - 1)这个公式
  ```

  ##### Solution

  ```
  Dynamic programming: dp[n][r] = dp[n - 1][r] + dp[n - 1][r - 1]
  ```

- ##### Description

  ```python
  341. Flatten Nested List Iterator
  ```

  ##### Solution

  ```python
  # """
  # This is the interface that allows for creating nested lists.
  # You should not implement it, or speculate about its implementation
  # """
  #class NestedInteger:
  #    def isInteger(self) -> bool:
  #        """
  #        @return True if this NestedInteger holds a single integer, rather than a nested list.
  #        """
  #
  #    def getInteger(self) -> int:
  #        """
  #        @return the single integer that this NestedInteger holds, if it holds a single integer
  #        Return None if this NestedInteger holds a nested list
  #        """
  #
  #    def getList(self) -> [NestedInteger]:
  #        """
  #        @return the nested list that this NestedInteger holds, if it holds a nested list
  #        Return None if this NestedInteger holds a single integer
  #        """
  
  class NestedIterator:
      def __init__(self, nestedList: [NestedInteger]):
          self.res = []
          self.prepare(nestedList)
          
      def next(self) -> int:
          if not self.hasNext(): return None
          top = self.res.pop()
          return top.getInteger()
          
          
          
      
      def hasNext(self) -> bool:
          while self.res and not self.res[-1].isInteger():
              top = self.res.pop()
              arr = top.getList()
              self.prepare(arr)
          return len(self.res) > 0
              
          
      
      def prepare(self, nestedList):
          for i in range(len(nestedList) - 1, -1, -1):
              self.res.append(nestedList[i])
  ```

- ##### Description

  ```python
  ‘5，3，+’-> '5+3'; '4,5,*,+,3,4'-> '(4+5)*（3+4）'
  ?? What's this?
  ```

- ##### Description

  ```python
  第一轮：给一个正整数N，求任意一个长度为 2*N 且满足以下条件的array：
  * 对于数字1 到 N，每个数出现两次，并且满足相同数字i之间有i个item。
  比如N = 3， 一个valid的array为：231213。 1和1之间有一个item（2），2和2之间有两个item（3，1）， 3和3之间有三个item（1，2，1
  ```

  ##### Solution

  ```python
  class Solution:
      def __init__(self, N):
          self.path = [-1] * 2 * N
  
      def generate(self, N):
          self.backtrack(1, N)
          return self.path
  
      def backtrack(self, num, N):
          if num == N + 1:
              return True
          for i in range(N):
              if self.path[i] == -1 and i + num + 1 < N and self.path[i + num + 1] == -1:
                  self.path[i] = num
                  self.path[i + num + 1] = num
                  if self.backtrack(num + 1, N): return True
                  self.path[i] = -1
                  self.path[i + num + 1] = -1
          return False
  
  if __name__ == "__main__":
      s = Solution(1)
      r = s.generate(1)
      print(r)
  ```

- ##### Description

  ```
  380. Insert Delete GetRandom O(1)
  ```

  ##### Solution

  ```python
  '''
  The most tricky part is the remove function:
  1. find the index of the given value in the res list: index = self.dic[value]
  2. replace the number at the index to the final number: self.res[index] = self.res[-1]
  3. chage the key value in the dictionary: self.dic[self.res.pop()] = index
  4. delete the given value from the dictionary: del self.dic[value]
  '''
  class RandomizedSet:
  
      def __init__(self):
          """
          Initialize your data structure here.
          """
          self.res = []
          self.dic = dict()
          
  
      def insert(self, val: int) -> bool:
          """
          Inserts a value to the set. Returns true if the set did not already contain the specified element.
          """
          if val not in self.dic:
              self.dic[val] = len(self.res)
              self.res.append(val)
              return True
          return False
          
  
      def remove(self, val: int) -> bool:
          """
          Removes a value from the set. Returns true if the set contained the specified element.
          """
          if val in self.dic:
              index = self.dic[val]
              self.res[index]  = self.res[-1]
              self.dic[self.res.pop()] = index
              del self.dic[val]
              return True
          return False
              
          
  
      def getRandom(self) -> int:
          """
          Get a random element from the set.
          """
          return self.res[random.randint(0, len(self.res) - 1)]
          
  
  
  # Your RandomizedSet object will be instantiated and called as such:
  # obj = RandomizedSet()
  # param_1 = obj.insert(val)
  # param_2 = obj.remove(val)
  # param_3 = obj.getRandom()
  ```

- ##### Description

  ```python
  200. Number of Islands
  Follow up: count the number of islands of differet shape???????
  ```

- ##### Description

  ```
  reverse the linked list
  ```

  ##### Solution

  ```python
  # recursive version
  class Solution:
      def reverseList(self, head: ListNode) -> ListNode:
          if not head: return None
          if not head.next: return head
          last = self.reverseList(head.next)
          head.next.next = head
          head.next = None
          return last
   # iterative version
   class Solution:
      def reverseList(self, head: ListNode) -> ListNode:
          pre, cur, nxt = None, head, head
          while cur:
              nxt = cur.next
              cur.next = pre
              pre = cur
              cur = nxt
          return pre
   
  ```

- ##### Description

  ```
  94. Binary Tree Inorder Traversal
  ```

  ##### Solution

  ```python
  # recursive version
  class Solution:
      def inorderTraversal(self, root: TreeNode) -> List[int]:
          res = []
          self.helper(root, res)
          return res
      def helper(self, root, res):
          if root:
              if root.left:
                  self.helper(root.left, res)
              res.append(root.val)
              if root.right:
                  self.helper(root.right, res)
  
  # iterative version
  class Solution:
      def inorderTraversal(self, root: TreeNode) -> List[int]:
          stack, res = [], []
          cur = root
          while stack or cur:
              while cur:
                  stack.append(cur)
                  cur = cur.left
              cur = stack.pop()
              res.append(cur.val)
              cur = cur.right
          return res
   # Morris traverse
  
  ```

- ##### Description

  ```
  140. Word Break II
  ```

  ##### Solution

  ```python
  # tle version
  class Solution:
      
      def __init__(self):
          self.trie = {}
          
      def construct(self, wordDict):
          for word in wordDict:
              t = self.trie
              for w in word:
                  t = t.setdefault(w, {})
              t['#'] = {}
          
      def wordBreak(self, s: str, wordDict: List[str]) -> List[str]:
          self.construct(wordDict)
          self.res = []
          self.dfs(s, [], 0, 0, self.trie)
          r = []
          for t in self.res:
              temp = ' '.join(t)
              r.append(temp)
          return r
          
      def dfs(self, s, path, start, end, trie):
          if end == len(s):
              if '#' in trie:
                  path.append(s[start : end])
                  self.res.append(path)
              return 
          
          if '#' in trie:
              self.dfs(s, path + [s[start : end]], end, end, self.trie)
              
          if s[end] in trie:
              self.dfs(s, path, start, end + 1, trie[s[end]])
              
              
  # backtrack version
  class Solution:
      def wordBreak(self, s: str, wordDict: List[str]) -> List[str]:
          wordDict = set(wordDict)
          memo = {}
          return self.backtrack(s, 0, memo, wordDict)
      
      def backtrack(self, s, start, memo, wordDict):
          if start == len(s): return ['']
          if start in memo: return memo[start]
          res = []
          for end in range(start, len(s)):
              temp = s[start : end + 1]
              if temp in wordDict:
                  left = self.backtrack(s, end + 1, memo, wordDict)
                  for item in left:
                      if item:
                          res.append(temp + ' ' + item)
                      else:
                          res.append(temp)
          memo[start] = res
          return res
  ```

  



