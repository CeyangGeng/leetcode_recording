# amazon oa2

- <img src="https://oss.1point3acres.cn/forum/202009/30/181755dle0x8wblk09j01w.png" alt="img" style="zoom:50%;" />

  ```python
  def construct(s, k):
      s_list = list(s)
      s_list.sort(reverse = True)
      print(s_list)
      size = len(s_list)
      i, j, m = 0, 0, 0
      while j < size:
          if s_list[j] != s_list[i]:
              alpha = s_list[i]
              consecutive_len = min(k, j - i)
              for ii in range(m, m + consecutive_len):
                  s_list[ii] = alpha
              m += consecutive_len
              i = j
          j += 1
      consecutive_len = min(k, j - i + 1)
      s_list[m : m + consecutive_len] = s_list[i]
      m += consecutive_len
      return s_list[:m]
  ```

- ![img](https://oss.1point3acres.cn/forum/202009/30/181757xckkhvtvwug3bbwc.png)

  ![img](https://oss.1point3acres.cn/forum/202009/30/181758lvov8f85ww8mlbv7.png)

  ```python
  from collections import Counter,defaultdict
  def droppedRequest(requestTime):
      requestTime.sort()
      try:
          counter = Counter(requestTime)
          lookup = defaultdict(int)
          size = len(requestTime)
          for i in range(requestTime[0], requestTime[-1] + 1):
              lookup[i] = lookup[i - 1] + counter[i]
          for i in range(3, size):
              temp1 = lookup[requestTime[i] - 10]
              temp2 = lookup[requestTime[i] - 60]
              if requestTime[i] == requestTime[i - 3]:
                  requestTime[i - 3] = '$'
              elif i + 1 - temp1 > 20:
                  requestTime[i] = '$'
              elif i + 1 - temp2 > 60:
                  requestTime[i] = '$'
          return requestTime.count('$')
      except:
          return 0
  if __name__ == "__main__":
      a = [1,1,1,1,2,2,2,3,3,3,4,4,4,5,5,5,6,6,6,7,7,7,7,11,11,11,11]
      res = droppedRequest(a)
      print(res)
  ```

- \1328. Break a Palindrome

  161173Add to ListShare

  Given a palindromic string `palindrome`, replace **exactly one** character by any lowercase English letter so that the string becomes the lexicographically smallest possible string that **isn't** a palindrome.

  After doing so, return the final string. If there is no way to do so, return the empty string.

   

  **Example 1:**

  ```
  Input: palindrome = "abccba"
  Output: "aaccba"
  ```

  **Example 2:**

  ```
  Input: palindrome = "a"
  Output: ""
  ```

   

  **Constraints:**

  - `1 <= palindrome.length <= 1000`
  - `palindrome` consists of only lowercase English letters.

  ```python
  class Solution:
      def breakPalindrome(self, palindrome: str) -> str:
          size = len(palindrome)
          for i in range(size // 2):
              if palindrome[i] != 'a':
                  return palindrome[:i] + 'a' + palindrome[i + 1:]
          return palindrome[:-1] + 'b' if palindrome[:-1] else ''
  ```

- \472. Concatenated Words

  Hard

  877117Add to ListShare

  Given a list of words (**without duplicates**), please write a program that returns all concatenated words in the given list of words.

  A concatenated word is defined as a string that is comprised entirely of at least two shorter words in the given array.

  **Example:**

  ```
  Input: ["cat","cats","catsdogcats","dog","dogcatsdog","hippopotamuses","rat","ratcatdogcat"]
  
  Output: ["catsdogcats","dogcatsdog","ratcatdogcat"]
  
  Explanation: "catsdogcats" can be concatenated by "cats", "dog" and "cats";  "dogcatsdog" can be concatenated by "dog", "cats" and "dog"; "ratcatdogcat" can be concatenated by "rat", "cat", "dog" and "cat".
  ```

  

  **Note:**

  1. The number of elements of the given array will not exceed `10,000`
  2. The length sum of elements in the given array will not exceed `600,000`.
  3. All the input string will only include lower case letters.
  4. The returned elements order does not matter.

  ```
  class Solution:
      def __init__(self):
          self.trie = {}
  
      def construct(self, words):
          for word in words:
              t = self.trie
              for w in word:
                  t = t.setdefault(w, {})
              t['#'] = {}
  
      def find(self, words):
          res = []
          self.construct(words)
          for word in words:
              self.dfs(word, self.trie, 0, 0, [], res, 0)
          return res
  
      def dfs(self, word, trie, start, end, path, res, count):
          if end == len(word):
              if '#' in trie:
                  path.append(word[start : end])
                  count += 1
                  if count >= 2:
                      res.append(path)
                      return True
              return False
          if '#' in trie:
              path.append(word[start : end])
              if self.dfs(word, self.trie, end, end, path, res, count + 1): return True
              path.pop()
  
          if word[end] not in trie: return False
          elif self.dfs(word, trie[word[end]], start, end + 1, path, res, count): return True
          return False
  
  if __name__ == '__main__':
      s = Solution()
      words = ["cat","cats","catsdogcats","dog","dogcatsdog","hippopotamuses","rat","ratcatdogcat"]
      res = s.find(words)
      print(res)
  ```

- Amazon Fresh is running a promotion in which customers receive prizes for purchasing a secret combination of fruits. The combination will change each day, and the team running the promotion wants to use a code list to make it easy to change the combination. The code list contains groups of fruits. Both the order of the groups within the code list and the order of the fruits within the groups matter. However, between the groups of fruits, any number, and type of fruit is allowable. The term "anything" is used to allow for any type of fruit to appear in that location within the group.
  Consider the following secret code list: [[apple, apple], [banana, anything, banana]]
  Based on the above secret code list, a customer who made either of the following purchases would win the prize:
  orange, apple, apple, banana, orange, banana
  apple, apple, orange, orange, banana, apple, banana, banana
  Write an algorithm to output 1 if the customer is a winner else output 0.

  

  **Input**
  The input to the function/method consists of two arguments:
  codeList, a list of lists of strings representing the order and grouping of specific fruits that must be purchased in order to win the prize for the day.
  shoppingCart, a list of strings representing the order in which a customer purchases fruit.
  **Output**
  Return an integer 1 if the customer is a winner else return 0.
  **Note**
  'anything' in the codeList represents that any fruit can be ordered in place of 'anything' in the group. 'anything' has to be something, it cannot be "nothing."
  'anything' must represent one and only one fruit.
  If secret code list is empty then it is assumed that the customer is a winner.

  

  **Example 1:**

  

  ```
  Input: codeList = [[apple, apple], [banana, anything, banana]] shoppingCart = [orange, apple, apple, banana, orange, banana]
  Output: 1
  Explanation:
  codeList contains two groups - [apple, apple] and [banana, anything, banana].
  The second group contains 'anything' so any fruit can be ordered in place of 'anything' in the shoppingCart. The customer is a winner as the customer has added fruits in the order of fruits in the groups and the order of groups in the codeList is also maintained in the shoppingCart.
  ```

  

  **Example 2:**

  

  ```
  Input: codeList = [[apple, apple], [banana, anything, banana]]
  shoppingCart = [banana, orange, banana, apple, apple]
  Output: 0
  Explanation:
  The customer is not a winner as the customer has added the fruits in order of groups but group [banana, orange, banana] is not following the group [apple, apple] in the codeList.
  ```

  

  **Example 3:**

  

  ```
  Input: codeList = [[apple, apple], [banana, anything, banana]] shoppingCart = [apple, banana, apple, banana, orange, banana]
  Output: 0
  Explanation:
  The customer is not a winner as the customer has added the fruits in an order which is not following the order of fruit names in the first group.
  ```

  

  **Example 4:**

  

  ```
  Input: codeList = [[apple, apple], [apple, apple, banana]] shoppingCart = [apple, apple, apple, banana]
  Output: 0
  Explanation:
  The customer is not a winner as the first 2 fruits form group 1, all three fruits would form group 2, but can't because it would contain all fruits of group 1.
  ```

  Solution

  ```python
  #####################my won solution###########################################
  #deal the codeList line by line
  def winPrize(codeList, shoppingCart):
      if not codeList: return 1
      m, size = len(codeList), len(shoppingCart)
      index = -1
      for i in range(m):
          index = helper(codeList, shoppingCart, i, index + 1)
          if index == float('inf'):
              return 0
      return 1
  
  def helper(codeList, shoppingCart, rowNumber, index):
      row_len = len(codeList[rowNumber])
      size = len(shoppingCart)
      end_index = float('inf')
      found = False
      for i in range(index, size - row_len + 1):
          found = False
          if shoppingCart[i] == codeList[rowNumber][0]:
              found = True
              for j in range(row_len):
                  if codeList[rowNumber][j] == shoppingCart[i + j] or \
                      codeList[rowNumber][j] == "anything":
                      continue
                  else:
                      found = False
                      break
              if found:
                  end_index = i + row_len - 1
                  break
      return end_index
  
  if __name__ == "__main__":
      codeList = [["apple", "apple"], ["banana", "anything", "banana"]]
      #shoppingCart = ["orange", "apple", "apple", "banana", "orange", "banana"]
      #shoppingCart = ["banana", "orange", "banana", "apple", "apple"]
      #shoppingCart = ["apple", "banana", "apple", "banana", "orange", "banana"]
      shoppingCart = ["apple", "apple", "apple", "banana"]
      res = winPrize(codeList, shoppingCart)
      print(res)
  
  ####################################two pointers##################################
  def winPrize(codeList, shoppingCart):
      if not codeList: return 1
      if not shoppingCart: return 0
      i, j = 0, 0
      while i < len(codeList) and j + len(codeList[i]) < len(shoppingCart):
          match = True
          for k in range(len(codeList[i])):
              if codeList[i][k] != 'anything' and codeList[i][k] != shoppingCart[j + k]:
                  match = False
                  break
          if match:
              j += len(codeList[i])
              i += 1
          else:
              j += 1
      return i == len(codeList)
  
  ```

- **Amazon Music Pairs**

  

  Amazon Music is working on a new "community radio station" feature which will allow users to iteratively populate
  the playlist with their desired songs. Considering this radio station will also have other scheduled shows to be
  aired, and to make sure the community soundtrack will not run over other scheduled shows, the user-submitted songs
  will be organized in full-minute blocks. Users can choose any songs they want to add to the community list, but
  only in pairs of songs with durations that add up to a multiple of 60 seconds (e.g. 60, 120, 180).

  

  As an attempt to insist on the highest standards and avoid this additional burden on users, Amazon will let them
  submit any number of songs they want, with any duration, and will handle this 60-second matching internally. Once
  the user submits their list, given a list of song durations, calculate the total number of distinct song pairs that
  can be chosen by Amazon Music.

  

  **Example**

  

  ```
  n = 3
  
  songs = [37, 23, 60]
  One pair of songs can be chosen whose combined duration is a multiple of a whole minute (37 + 23 = 60) and the
  return value would be 1. While the third song is a single minute long, songs must be chosen in pairs.
  ```

  

  **Function Description**

  

  Complete the function getSongPairCount in the editor below.

  

  getSongPairCount has the following parameter:

  

  int songs[n]: array of integers representing song durations in seconds

  

  Returns:

  

  long: the total number of songs pairs that add up to a multiple of 60 seconds. If there are no suitable pairs,
  return 0.

  

  **Constraints**

  

  1 ≤ n ≤ 105
  1 ≤ songs[i] ≤ 1000, where 0 ≤ i < n

  

  **Input Format For Custom Testing**
  Input from stdin will be processed as follows and passed to the function.

  

  The first line contains an integer, n, that denotes the number of elements in songs.

  

  The next n lines each contain an integer that describes songs[i] and denotes the duration of the ith song
  (in seconds).

  

  **Sample Case 0
  Sample Input For Custom Testing**

  

  STDIN Function

  

  ------

  

  4 -> songs[] size n = 4
  10 -> songs = [10, 50, 90, 30]
  50
  90
  30
  **Sample Output**

  

  2
  **Explanation**

  

  The first and second songs pair to 60 seconds. The third and fourth songs pair to 120 seconds. No other pairs
  will satisfy the requirement.

  

  **Sample Case 1
  Sample Input For Custom Testing**

  

  STDIN Function

  

  ------

  

  5 -> songs[] size n = 5
  30 -> songs = [30, 20, 150, 100, 40]
  20
  150
  100
  40
  **Sample Output**

  

  3
  **Explanation**

  

  There are three pairs of songs whose whole duration is a multiple of a whole minute. They are 20 + 100, 30 + 150,
  and 20 + 40 corresponding to (1, 3), (0, 2) and (1, 4).

  

  **Sample Case 2
  Sample Input For Custom Testing**

  

  STDIN Function

  

  ------

  

  3 -> songs[] size n = 3
  60 -> songs = [60, 60, 60]
  60
  60
  **Sample Output*

  3
  **Explanation**

  

  There are three pairs of songs that end in whole minutes. They are (0, 1), (1, 2) and (0, 2).

  Solution:

  ```python
  from collections import defaultdict
  def find(songs):
      memo = defaultdict(int)
      count = 0
      for song in songs:
          count += memo[60 - (song % 60)]
          memo[song % 60] += 1
      return count
  ```

- **Items in Containers**

  

  Amazon would like to know how much inventory exists in their closed inventory compartments. Given a string s
  consisting of items as "*" and closed compartments as an open and close "|", an array of starting indices
  startIndices, and an array of ending indices endIndices, determine the number of items in closed compartments
  within the substring between the two indices, inclusive.

  

  An item is represented as an asterisk ('*' = ascii decimal 42)
  A compartment is represented as a pair of pipes that may or may not have items between them ('|' = ascii decimal 124).

  

  **Example**

  

  ```
  s = '|**|*|*'
  ```

  

  startIndices = [1, 1]

  

  endIndices = [5, 6]

  

  The string has a total of 2 closed compartments, one with 2 items and one with 1 item. For the first pair of
  indices, (1, 5), the substring is '|**|*'. There are 2 items in a compartment.

  

  For the second pair of indices, (1, 6), the substring is '|**|*|' and there are 2 + 1 = 3 items in compartments.

  

  Both of the answers are returned in an array, [2, 3].

  

  **Function Description .**

  

  Complete the numberOfItems function in the editor below. The function must return an integer array that contains
  the results for each of the startIndices[i] and endIndices[i] pairs.

  

  numberOfItems has three parameters:

  

  - 

    s: A string to evaluate

    

  - 

    startIndices: An integer array, the starting indices.

    

  - 

    endIndices: An integer array, the ending indices.

    

  

  **Constraints**

  

  1 ≤ m, n ≤ 105
  1 ≤ startIndices[i] ≤ endIndices[i] ≤ n
  Each character of s is either '*' or '|'

  

  **Input Format For Custom Testing**

  

  The first line contains a string, S.
  The next line contains an integer, n, the number of elements in startIndices.
  Each line i of the n subsequent lines (where 1 ≤ i ≤ n) contains an integer, startIndices[i].
  The next line repeats the integer, n, the number of elements in endIndices.
  Each line i of the n subsequent lines (where 1 ≤ i ≤ n) contains an integer, endIndices[i]

  **Sample Case 0
  Sample Input For Custom Testing**

  

  Solution:

  ```
  def count_items(s, start_indices, end_indices):
      size = len(start_indices)
      left, right, count = [0] * size, [0] * size, [0] * size
      pre_left, post_right, total = -1, -1, 0
      for i in range(size):
          if s[i] == '|':
              pre_left = i
          left[i] = pre_left
      for j in range(size - 1, -1, -1):
          if s[j] == '|':
              post_right = j
          right[j] = post_right
      for k in range(size):
          if s[k] == '*':
              total += 1
          count[k] = total
      res = [0] * size
      for i in range(size):
          start, end = start_indices[i] - 1, end_indices[i] - 1
          a, b = count[start], count[end]
          if (a >= b): res[i] = 0
          else: res[i] = count[b] - count[a]
      return res
  ```

- ![image-20201012142520988](C:\Users\gcy\AppData\Roaming\Typora\typora-user-images\image-20201012142520988.png)

  ```python
  #dfs/bfs
  # general solution is to construct the graph first
  # keep a visited set and to avoid repeated search,the node should be added to the visited set and stack at the same time
  # for each independent searching path, keep a current path to record all the node at this path. adding node to the path at the pop line.
  from collections import defaultdict
  def find(item_association):
      memo = defaultdict(list)
      for first, second in item_association:
          memo[first].append(second)
          memo[second].append(first)
      largest_group, visited = [], set()
      for key, val in memo.items():
          if key not in visited:
              visited.add(key)
              stack = [key]
              cur_group = []
              while stack:
                  node = stack.pop()
                  cur_group.append(node)
                  for neighbor in memo[node]:
                      if neighbor not in visited:
                          visited.add(neighbor)
                          stack.append(neighbor)
              if len(cur_group) > len(largest_group):
                  largest_group = cur_group
      largest_group.sort()
      return largest_group
  if __name__ == "__main__":
      #item_association = [['item1', 'item2'], ['item3', 'item4'], ['item4', 'item5']]
      item_association = [['item1', 'item2'], ['item4', 'item5'], ['item3', 'item4'], ["item1","item4"]]
      res = find(item_association)
      print(res)
  ```

- Imagine a small Amazon Go store that has exactly one turnstile. It can be used by customers either as an entrance or an exit. Sometimes multiple customers want to pass through the turnstile and their directions can be different. The ith customer comes to the turnstile at time[i] and wants to either exit the store if direction [i] = 1 or enter the store if direction[i] = 0. Customers form 2 queues, one to exit and one to enter. They are ordered by the time when they came to the turnstile and, if the times are equal, by their indices.

  

  If one customer wants to enter the store and another customer wants to exit at the same moment, there are three cases:

  

  If in the previous second the turnstile was not used (maybe it was used before, but not at the previous second), then the customer who wants to exit goes first.
  If in the previous second the turnstile was used as an exit, then the customer who wants to leave goes first.
  If in the previous second the turnstile was used as an entrance, then the customer who wants to enter goes first.
  Passing through the turnstile takes 1 second.

  

  Write an algorithm to find the time for each customer when they will pass through the turnstile.

  

  Input

  

  The function/method consists of three arguments:

  

  numcustomers, an integer representing the number of customers (n);
  arrTime, a list of integers where the value at indexi is the time in seconds when the ith customer will come to the turnstile;
  direction, a list of integers where the value at indexi is the direction of the ith customer.

  

  Output

  

  Return a list of integers where the value at index i is the time when the ith customer will pass the turnstile.

  

  Constraints

  

  1 <= numCustomers <= 10^5
  0 <= arrTime[i] <= arrTime[i + 1] <= 10^9
  0 <= i <= numCustomers - 2
  0 <= direction[i] <= 1
  0 <= j <= numCustomers - 1

  

  Examples

  

  Example 1:

  

  Input:
  numCustomers = 4
  arrTime = [0, 0, 1,5]
  direction = [0, 1, 1, 0]
  Output:
  [2,0,1,5]

  

  Explanation:
  At time 0, customer 0 and 1 want to pass through the turnstile. Customer 0 wants to enter the store and customer 1 wants to leave the store. The turnstile was not used in the previous second, so the priority is on the side of the customer 1
  At time 1, customers 0 and 2 want to pass through the turnstile. Customer 2 wants to leave the store and at the previous second the turnstile was used as an exit, so the customer 2 passes through the turnstile.
  At time 2, customer 0 passes through the turnstile.
  At time 5, customer 3 passes through the turnstile.

  

  Example 2

  

  Input:
  numCustomers = 5
  arrTime = [0,1,1,3,3]
  direction = [0, 1, 0, 0, 1]
  Output: [0, 2, 1, 4, 3]

  

  Explanation:

  

  At time 0, customer 0 passes through the turnstile (enters).
  At time 1, customers 1 (exit) and 2 (enter) want to pass through the turnstile, and customer 2 passes through the turnstile because their direction is equal to the direction at the previous second.
  At time 2. customer 1 passes through the turnstile (exit).
  At time 3, customers 3 (enter) and 4 (exit) want to pass through the turnstile. Customer 4 passes through the turnstile because at the previous second the turnstile was used to exit.
  At time 4, customer 3 passes through the turnstile.

  Solution:

  ```python
  # deal with the queue one second by one second
  from collections import deque
  def customers(numCustomers, arrTime, direction):
      exit, enter = deque(), deque()
      time, status = 0, True
      i = 0
      res = [-1] * numCustomers
      while i < numCustomers or exit or enter:
          while i < numCustomers and arrTime[i] <= time:
              if direction[i] == 1: exit.append(i)
              else: enter.append(i)
              i += 1
          if exit or enter:
              if exit and status:
                  res[exit.popleft()] = time
              elif enter and not status:
                  res[enter.popleft()] = time
              elif exit:
                  res[exit.popleft()] = time
                  status = True
              elif enter:
                  res[enter.popleft()] = time
                  status = False
          else:
              status = True
              time = arrTime[i] - 1
          time += 1
      return res
  
  if __name__  == "__main__":
      numCustomers = 5
      arrTime = [0, 1, 1, 3, 3]
      direction = [0, 1, 0, 0, 1]
      res = customers(numCustomers, arrTime, direction)
      print(res)
  ```

- Given the number of five-star and total reviews for each product a company sells, as well as the threshold percentage, what is the minimum number of additional five-star reviews the company needs to become five star seller.
  For ex, there are 3 products (n=3) with productRatings =[[4,4],[1,2],[3,6]], percentage rating threshold = 77.
  [1,2] indicates => [1 (five star reviews) ,2 (total reviews)].
  We need to get the seller reach the threshold with minimum number of additional five star reviews.

  

  Before we add more five star reviews, the percentage for this seller is ((4/4) + (1/2) + (3/6))/3 = 66.66%
  If we add a five star review to 2nd product, ((4/4) + (2/3) + (3/6))/3 = 72.22%
  If we add another five star review to 2nd product, ((4/4) + (3/4) + (3/6))/3 = 75%
  If we add a five star review to 3rd product, ((4/4) + (3/4) + (4/7))/3 = 77.38%
  At this point, 77% (threshold) is met. Therefore, answer is 3 (because that is the minimum five star reviews we need to add, to get the seller reach the threshold).

  ```python
  import heapq
  def five_start(productRatings, threshold):
      n = len(productRatings)
      cur_rating = (sum(p0 / p1 for p0, p1 in productRatings) / n) * 100
      def diff(p):
          return (p[0] + 1) / (p[1] + 1) - p[0] / p[1]
      heap = [[-diff(p)] + p for p in productRatings]
      heapq.heapify(heap)
      count = 0
      while cur_rating < threshold:
          d, p0, p1 = heapq.heappop(heap)
          cur_rating = (cur_rating * n - d * 100) / n
          heapq.heappush(heap, [-diff([p0 + 1, p1 + 1]), p0 + 1, p1 + 1])
          count += 1
      return count
  if __name__ == "__main__":
      productRatings = [[4,4],[1,2],[3,6]]
      threshold = 77
      res = five_start(productRatings, threshold)
      print(res)
  ```

- \1335. Minimum Difficulty of a Job Schedule

  Hard

  2448Add to ListShare

  You want to schedule a list of jobs in `d` days. Jobs are dependent (i.e To work on the `i-th` job, you have to finish all the jobs `j` where `0 <= j < i`).

  You have to finish **at least** one task every day. The difficulty of a job schedule is the sum of difficulties of each day of the `d` days. The difficulty of a day is the maximum difficulty of a job done in that day.

  Given an array of integers `jobDifficulty` and an integer `d`. The difficulty of the `i-th` job is `jobDifficulty[i]`.

  Return *the minimum difficulty* of a job schedule. If you cannot find a schedule for the jobs return **-1**.

   

  **Example 1:**

  ![img](https://assets.leetcode.com/uploads/2020/01/16/untitled.png)

  ```
  Input: jobDifficulty = [6,5,4,3,2,1], d = 2
  Output: 7
  Explanation: First day you can finish the first 5 jobs, total difficulty = 6.
  Second day you can finish the last job, total difficulty = 1.
  The difficulty of the schedule = 6 + 1 = 7 
  ```

  **Example 2:**

  ```
  Input: jobDifficulty = [9,9,9], d = 4
  Output: -1
  Explanation: If you finish a job per day you will still have a free day. you cannot find a schedule for the given jobs.
  ```

  **Example 3:**

  ```
  Input: jobDifficulty = [1,1,1], d = 3
  Output: 3
  Explanation: The schedule is one job per day. total difficulty will be 3.
  ```

  **Example 4:**

  ```
  Input: jobDifficulty = [7,1,7,1,7,1], d = 3
  Output: 15
  ```

  **Example 5:**

  ```
  Input: jobDifficulty = [11,111,22,222,33,333,44,444], d = 6
  Output: 843
  ```

   

  **Constraints:**

  - `1 <= jobDifficulty.length <= 300`
  - `0 <= jobDifficulty[i] <= 1000`
  - `1 <= d <= 10`

  Solution:

  ```python
  class Solution:
      def minDifficulty(self, jobDifficulty: List[int], d: int) -> int:
          size = len(jobDifficulty)
          if size < d: return -1
          if size == d: return sum(jobDifficulty)
          dp = [[-1] * (size + 1) for _ in range(d + 1)]
          return self.helper(dp, d, 0, jobDifficulty)
      def helper(self, dp, day, index, jobDifficulty):
          size = len(jobDifficulty)
          if day == 0 and index == size: return 0
          if day == 0 or index == size: return float('inf')
          cur_max = jobDifficulty[index]
          if dp[day][index] != -1: return dp[day][index]
          res = float('inf')
          for j in range(index, size):
              cur_max = max(cur_max, jobDifficulty[j])
              left = self.helper(dp, day - 1, j + 1, jobDifficulty)
              res = min(res, cur_max + left)
          dp[day][index] = res
          return res
  ```

- Given a list of `reviews`, a list of `keywords` and an integer `k`. Find the most popular `k` keywords in order of most to least frequently mentioned.

  

  The comparison of strings is case-insensitive.
  Multiple occurances of a keyword in a review should be considred as a single mention.
  If keywords are mentioned an equal number of times in reviews, sort alphabetically.

  ```python
  from collections import defaultdict
  def find(k, keywords, reviews):
      keywords = set([kw.lower() for kw in keywords])
      dic = defaultdict(int)
      for review in reviews:
          review = review.lower()
          words = review.split(' ')
          seen = set()
          for word in words:
              if word in keywords and word not in seen:
                  dic[word] += 1
                  seen.add(word)
      temp = sorted(dic.items(), key = lambda x: (-x[1], x[0]))
      return [x[0] for x in temp[:k]]
  ```

- Amazon parses logs of user transactions/activity to flag fraudulent activity. The log file is represented as an Array of arrays. The arrays consist of the following data:

  

  ```
  [  <# of transactions>]
  ```

  

  For example:

  

  `[345366 89921 45]`
  Note the data is space delimited

  

  So, the log data will look like:

  

  ```
  [
  [345366 89921 45],
  [029323 38239 23]
  ...
  ]
  ```

  

  Write a function to parse the log data to find distinct user count that meets or crosses a certain threshold. The function will take in 2 inputs:

  

  **Input 1:** Log data in form an array of arrays
  **Input 2:** threshold as an integer

  

  Output should be an array of userids that are sorted.

  

  If same userid appears in the transaction as userid1 and userid2, it should count as one occurence, not two.

  

  Example:
  **Input 1:**

  

  ```
  [
  [345366 89921 45],
  [029323 38239 23],
  [38239 345366 15],
  [029323 38239 77],
  [345366 38239 23],
  [029323 345366 13],
  [38239 38239 23]
  ...
  ]
  ```

  

  **Input 2**: `3`

  

  **Ouput:** `[345366 , 38239, 029323]`

  

  Explanation:
  Given the following counts of userids, there are only 3 userids that meet or exceed the threshold of 3.
  `345366 -4 , 38239 -5, 029323-3, 89921-1`

  Solution:

  ```python
  from collections import defaultdict
  def find(logs, threshold):
      dic = defaultdict(int)
      for log in logs:
          for user_id in set(log[:2]):
              dic[user_id] += 1
      res = [user_id for user_id in dic if dic[user_id] >= threshold]
      return sorted(res, reverse = True)
  ```

- As part of Day 1 challenge, your manager has created a word game for you and your teammates to play.
  The word game begins with your manager writing a string, and a number K on the board.
  You and your teammates must find a substring of size K such that there is exactly one character that is repeated once.
  In other words, there should be K - 1 distinct characters in the substring.

  

  Write an algorithm to help your teammates find the correct answer. If no such substring can be found, return an empty list;
  If multiple such substrings exit, return all of them, without repetitions. The order in which the substrings are returned does not matter.

  

  Input: it has two arguments:

  

  ```
  inputString: representing the string written by the manager.
  num: an integer representing the number K, written by the manager on the board.
  ```

  

  Output:

  

  ```
  Return a list of all substrings of inputString with K characters, that have K - 1 distinct character, i.e. exactly one character is repeated,
  or an empty list if no such substring exists in inputString. The order in which the substrings are returned does not matter.
  ```

  

  Constraints:

  

  ```
  The input integer can only be greater than or equal to 0 and less than or equal to 26 (0 <= num <= 26).
  The input string consists of only lowercase alphabetic characters.
  ```

  

  Example 1:

  

  ```
  Input: 
  inputString = awaglk
  num = 4
  
  Output:
  [awag]
  
  Explanation:
  The substrings are {awag, wagl, aglk}
  The answer is awag as it has 3 distinct characters in a string of size 4, and only one character is repeated twice.
  ```

  

  Example 2:

  

  ```python
  Input: 
  inputString = democracy
  num = 5
  
  Output:
  [ocrac, cracy]
  ```

  Solution:

  ```python
  from collections import defaultdict
  def search(string, num):
      i, j, count, size = 0, 0, 0, len(string)
      dic = defaultdict(int)
      res = set()
      while j < size:
          alpha = string[j]
          dic[alpha] += 1
          if dic[alpha] == 2:
              count += 1
          if j - i + 1 == num:
              if count == 1: res.add(string[i : j + 1])
              beta = string[i]
              dic[beta] -= 1
              if dic[beta] == 1: count -= 1
              i += 1
          j += 1
      return res
  
  if __name__ == "__main__":
      string = "wawaglknagagwunagkwkwagl"
      res = search(string, 4)
      print(list(res))
  ```

- \200. Number of Islands

  Medium

  6602214Add to ListShare

  Given a 2d grid map of `'1'`s (land) and `'0'`s (water), count the number of islands. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

   

  **Example 1:**

  ```
  Input: grid = [
    ["1","1","1","1","0"],
    ["1","1","0","1","0"],
    ["1","1","0","0","0"],
    ["0","0","0","0","0"]
  ]
  Output: 1
  ```

  **Example 2:**

  ```python
  Input: grid = [
    ["1","1","0","0","0"],
    ["1","1","0","0","0"],
    ["0","0","1","0","0"],
    ["0","0","0","1","1"]
  ]
  Output: 3
  ```

  Solution:

  ```python
  class Solution:
      def numIslands(self, grid: List[List[str]]) -> int:
              if not grid: return 0
              count, m, n = 0, len(grid), len(grid[0])
              for i in range(m):
                  for j in range(n):
                      if grid[i][j] == '1':
                          count += 1
                          stack = [(i, j)]
                          grid[i][j] = '0'
                          while stack:
                              x, y = stack.pop()
                              for delta_x, delta_y in [(-1, 0), (1, 0), (0, 1), (0, -1)]:
                                  new_x, new_y = x + delta_x, y + delta_y
                                  if 0 <= new_x < m and 0 <= new_y < n and grid[new_x][new_y] == '1':
                                      stack.append((new_x, new_y))
                                      grid[new_x][new_y] = '0'
              return count
  ```

- \819. Most Common Word

  Easy

  7681785Add to ListShare

  Given a paragraph and a list of banned words, return the most frequent word that is not in the list of banned words. It is guaranteed there is at least one word that isn't banned, and that the answer is unique.

  Words in the list of banned words are given in lowercase, and free of punctuation. Words in the paragraph are not case sensitive. The answer is in lowercase.

  ```python
  from collections import Counter
  class Solution:
      def mostCommonWord(self, paragraph: str, banned: List[str]) -> str:
          words = re.findall(r'\w+', paragraph.lower())
          print(words)
          banned = set(banned)
          return Counter([w for w in words if w not in banned]).most_common(1)[0][0]
  ```

- 



