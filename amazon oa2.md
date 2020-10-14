# amazon oa2

here is the link of review of oa2: https://leetcode.com/discuss/interview-question/344650/Amazon-Online-Assessment-Questions

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

  ```python
  def item_in_containers(s, start_indices, end_indices):
      size_s = len(s)
      star, left, right = [0] * size_s, [0] * size_s, [0] * size_s
      count, pre_left, post_right = 0, -1, -1
      for i in range(size_s):
          if s[i] == '*': count += 1
          star[i] = count
      for i in range(size_s):
          if s[i] == '|': pre_left = i
          left[i] = pre_left
      for i in range(size_s - 1, -1, -1):
          if s[i] == '|': post_right = i
          right[i] = post_right
      size = len(start_indices)
      res = []
      for i in range(size):
          s, e = start_indices[i] - 1, end_indices[i] - 1
          ss, ee = right[s], left[e]
          if ss >= ee: return 0
          res.append(star[ee] - star[ss])
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
      res = set()A new team at Amazon is doing an internal beta test 
      while j < size:
          alpha = string[j]
          dic[alpha] += 1
          if dic[alpha] == 2:
              count += 1
          if dic[string[j]] > 2:
              i = j
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

- <img src="C:\Users\gcy\AppData\Roaming\Typora\typora-user-images\image-20201013092726230.png" alt="image-20201013092726230" style="zoom:50%;" />





<img src="C:\Users\gcy\AppData\Roaming\Typora\typora-user-images\image-20201013092736728.png" alt="image-20201013092736728" style="zoom:50%;" />

```python
#Sort the box mainly according to the unitSize.
import heapq
def pack(num, boxes, unitSize, unitPerBox, truckSize):
    size = len(unitPerBox)
    for i in range(size):
        unitPerBox[i] *= -1
    combine = list(zip(unitPerBox, boxes))
    heapq.heapify(combine)
    res = 0
    while truckSize > 0 and combine:
        a, b = heapq.heappop(combine)
        a *= -1
        count = min(truckSize, b)
        truckSize -= count
        res += count * a
    return res

```



- Amazon is performing an analysis on the computers at one of its offices.

  

  The computers are spaced along a single row. The analysis is performed in the following way:
  Choose a contiguous segment of a certain number of computers, starting from the beginning of the row.

  

  Analyze the available hard disk space on each of the computers. Determine the minimum available disk space within this segment. After performing these steps for the first segment, it is then repeated for the next segment, continuing this procedure until the end of the row (i.e. if the segment size is 4, computers 1 to 4 would be analyzed, then 2 to 5, etc.)

  

  ***Given this analysis procedure, write an algorithm to find the maximum available disk space among all the minima that are found during the analysis.***

  

  ##### Input:

  

  The input to the function/method consists of 3 arguments:
  ***numComputer***, an integer representing the number of computers;
  ***hardDiskSpace***, a list of integers representing the hard disk space of the computers;
  ***segmentLength***, an integer representing the length of the contiguous segment of computers to
  be consider in each iterations.

  

  ##### Output:

  

  Return an integer representing the maximum available disk space among all the minima that are found during the analysis.

  

  ##### Constraints:

  

  1 ≤ numComputer ≤ 10^6
  1 ≤ segmentLength ≤ numComputer
  1 ≤ hardDiskSpace[i] ≤ 10^9
  0 ≤ i < numComputer

  

  #### Example:

  ##### Input:

  

  numComputer = 3
  hardDiskSpace = [8,2,4]
  segmentLength = 2

  

  ##### Output:

  

  2

  

  ##### Explanation:

  

  In this array of computers, the subarrays of size 2 are [8,2] and [2,4].
  Thus, the initial analysis returns 2 and 2 because those are the minima for the segmenets.
  Finally the maximum of these values is 2.
  Therefore, the answer is 2.

  ###### Solution

  ```python
  #find consecutive smallest using monotonic queue
  from collections import deque
  def disk_space(numComputer, hardDiskSpace, segmentLength):
      max_min_space = min(hardDiskSpace[:segmentLength])
      dq = deque()
      for i in range(numComputer):
          if dq and dq[0] < i - segmentLength + 1:
              dq.popleft()
          while dq and hardDiskSpace[dq[-1]] > hardDiskSpace[i]:
              dq.pop()
          dq.append(i)
          if i >= segmentLength - 1:
              max_min_space = max(max_min_space, dq[0])
      return max_min_space
  ```

- Amazon has Fulfillment Centers in multiple cities within a large geographic region. The cities are arranged on a group that has been divided up like an ordinary Cartesian plane. Each city is located at an integral(x,y) coordinate intersection. City names and locations are given in the form of three arrays: c,x, and y, which are aligned by the index to provide the city name (c[i]), and its coordinates, (x[i],y[i]).

  

  **Write an algorithm to determine the name of the nearest city that shares an x or a y coordinate with the queried city. If no cities share an x or y coordinate, return none. If two cities have the same distance to the queried city, q[i], consider the one with an alphabetically smaller name (e.e 'ab' < 'aba' < 'abb') as the closest choice.**

  

  The distance is denoted on a Euclidean plan: the difference in x plus the difference in y.

  

  **Input**
  the input to the function/method consists of six arguments:
  ***numOfCities***, an integer representing the number of cities;
  ***cities***, a list of strings representing the names of each city[i];
  ***xCoordinates***, a list of integers representing the X-coordinates of each city[i];
  ***yCoordinates***, a list of integers representing the Y-coordinates of each city[i];
  ***numOfQueries***, an integer representing the number of queries;
  ***queries***, a list of strings representing the names of the queried cities.

  

  **Output**
  Return a list of strings representing the name of the nearest city that shares either an x or a y coordinate with the queried city.

  

  **Constraints**
  1 ≤ numOfCities, numOfQueries ≤ 10^5
  1 ≤ xCoordinates[i], yCoordinates[i] <= 10^9
  1 ≤ length of queries[i] and cities[i] ≤ 10

  

  **Note**
  Each character of all c[i] and q[i] is in the range ascii[a-z, 0-9,-]
  All city name values, c[i] are unique. All cities have unique coordinates.

  

  **Example:**

  

  **Input:**

  

  numOfCities = 3
  cities = ["c1", "c2", "c3"]
  xCoordinates = [3,2,1]
  yCoordinates = [3,2,3]
  numOfQueries = 3
  queries = ["c1", "c2", "c3"]

  ##### Solution

  ```python
  #time complexity: O(nq)
  def get_distance(x, y, new_x, new_y):
      return abs(x - new_x) + abs(y - new_y)
  def search(numOfCities, cities, xCoordinates, yCoordinates, numOfQueries, queries):
      if not queries: return []
      res = []
      for query in queries:
          index = cities.index(query)
          x, y = xCoordinates[index], yCoordinates[index]
          nearest_city = None
          min_dis = float('inf')
          for i in range(numOfCities):
              new_x, new_y = xCoordinates[i], yCoordinates[i]
              if i != index and (new_x == x or new_y == y):
                  cur_distance = get_distance(x, y, new_x, new_y)
                  if cur_distance < min_dis:
                      min_dis = cur_distance
                      nearest_city = cities[i]
                  elif cur_distance == min_dis:
                      nearest_city = min(nearest_city, cities[i])
          res.append(nearest_city)
      return res
  if __name__ == "__main__":
      numOfCities = 3
      cities = ["c1", "c2", "c3"]
      xCoordinates = [3, 2, 1]
      yCoordinates = [3, 2, 3]
      numOfQueries = 3
      queries = ["c1", "c2", "c3"]
      res = search(numOfCities, cities, xCoordinates, yCoordinates, numOfQueries, queries)
      print(res)
      
  ############################## time complexity qnlog(n), using heap###############
  from collections import defaultdict
  import heapq
  def nearest_city(numOfCities, cities, xCoordinates, yCoordinates, numOfQueries, queries):
      dic_x = defaultdict(list)
      dic_y = defaultdict(list)
      city_index_memo = dict()
      for i, city in enumerate(cities):
          city_index_memo[city] = i
      for i in range(numOfCities):
          x, y, city = xCoordinates[i], yCoordinates[i], cities[i]
          dic_x[x].append((y, city))
          dic_y[y].append((x, city))
      res = []
      for query in queries:
          index = city_index_memo[query]
          x, y = xCoordinates[index], yCoordinates[index]
          x_same_neighbors = dic_x[x]
          y_same_neighbors = dic_y[y]
          if len(x_same_neighbors) == 1 and len(y_same_neighbors) == 1:
              res.append(None)
              continue
          diff_x_same_neighbors = [(abs(x_same_neighbor - y), city) for x_same_neighbor, city in x_same_neighbors if x_same_neighbor != y]
          diff_y_same_neighbors = [(abs(y_same_neighbor - x), city) for y_same_neighbor, city in y_same_neighbors if y_same_neighbor != x]
          x_diff, y_diff = float('inf'), float('inf')
          if diff_x_same_neighbors:
              x_diff, city_x = heapq.heappop(diff_x_same_neighbors)
          if diff_y_same_neighbors:
              y_diff, city_y = heapq.heappop(diff_y_same_neighbors)
          if x_diff < y_diff:
              res.append(city_x)
          elif x_diff > y_diff:
              res.append(city_y)
          else:
              res.append(min(city_x, city_y))
      return res
  ```

- Given an N-ary tree, find the subtree with the maximum average. Return the root of the subtree.
  A subtree of a tree is the node which have **at least 1 child** plus all its descendants. The average value of a subtree is the sum of its values, divided by the number of nodes.

  

  **Example 1:**

  

  ```python
  Input:
  		 20
  	   /   \
  	 12     18
    /  |  \   / \
  11   2   3 15  8
  
  Output: 18
  Explanation:
  There are 3 nodes which have children in this tree:
  12 => (11 + 2 + 3 + 12) / 4 = 7
  18 => (18 + 15 + 8) / 3 = 13.67
  20 => (12 + 11 + 2 + 3 + 18 + 15 + 8 + 20) / 8 = 11.125
  
  18 has the maximum average so output 18.
  ```

  ##### Solution

  ```python
  # dfs, the return value of helper function or the dfs function is a list including the sum of the subtree and the node count of the subtree
  class TreeNode:
      def __init__(self, val):
          self.val = val
          self.children = []
  class Solution:
      def MaxAverageSubTree(self, root):
          if not root or not roo.children: return None
          self.average = float('inf')
          self.res = None
          self.helper(root)
          return self.res
      def helper(self, node):
          if not node.children: return [node.val, 1]
          total, count = node.val, 1
          for child in node.children:
              cur_total, cur_count = self.helper(child)
              total += cur_total
              count += cur_count
          if total / count > self.average:
              self.res = node
          return [total, count]
  ```

- \1328. Break a Palindrome

  Medium

  164177Add to ListShare

  Given a palindromic string `palindrome`, replace **exactly one** character by any lowercase English letter so that the string becomes the lexicographically smallest possible string that **isn't** a palindrome.

  After doing so, return the final string. If there is no way to do so, return the empty string.

   

  **Example 1:**

  ```
  Input: palindrome = "abccba"
  Output: "aaccba"
  ```

  **Example 2:**

  ```python
  Input: palindrome = "a"
  Output: ""
  ```

  ##### Solution

  ```python
  class Solution:
      def breakPalindrome(self, palindrome: str) -> str:
          size = len(palindrome)
          for i in range(size // 2):
              if palindrome[i] != 'a':
                  return palindrome[:i] + 'a' + palindrome[i + 1:]
          return palindrome[:-1] + 'b' if palindrome[:-1] else ''
  ```

- Amazon is working on a new application for recording internal debts across teams.
  This program can be used to create groups that show all records of debts between the group members.
  Given the group debt records observed for this team (including the borrower name, lender name, and debt amount),
  **who in the group has the smallest negative balance**?

  

  ##### Notes:

  

  -10 is smaller than -1
  If multiple people have the smallest negative balance, return the list in alphabetical order.
  If nobody has a negative balance, return the list consisting of string "Nobody has a negative balance".

  

  ***Write an algorithm to find who in the group has the smallest negative balance.***

  

  ##### Input:

  

  The input to the function/method consists of three arguments:
  numRows, an integer representing the number of debt records.
  numCols, an integer representing th enumber of elements in debt records. It is always 3.
  debts, a list of triplet representing debtRecord consisting of a string borrower, a string lender, and an integer
  amount, representing the debt record.

  

  ##### Output:

  

  Return a list of strings representing an alphabetically ordered list of members with the smallest negative balance.
  If no team member has a negative balance then return a list containing the string "Nobody has a negative balance".

  

  ##### Constraints:

  

  1 ≤ numRows ≤ 2*10^5
  1 ≤ amount in debts ≤ 1000
  1 ≤ length of borrower and lender in debts ≤ 20

  

  **Example:**
  Input:

  

  | borrower | lender | amount |
  | :------: | :----: | :----: |
  |   Alex   | Blake  |   2    |
  |  Blake   |  Alex  |   2    |
  |  Casey   |  Alex  |   5    |
  |  Blake   | Casey  |   7    |
  |   Alex   | Blake  |   4    |
  |   Alex   | Casey  |   4    |

  

  Output:
  ["Alex", "Blake"]

  

  Explanation:
  The first, fifth, and sixth entries decrease Alex's balance because Alex is a borrower.
  The second and third entries increase because Alex is a lender. So, Alex's balance is (2+5) - (2+4+4) = 7 - 10 = -3. Blake is lender in first and fifth entries and a borrower in the second and fourth entries. Thus, Blake's balance is (2+4) - (2+7) = 6 - 9 = -3. Casey is a borrower in the third entry and a lender in the fourth and sixth entries. Thus, Casey's balance is (7 + 4) - 5 = 11 - 6 = 5. Here Alex and Blake both have the balance of -3, which is the minimum amoung all members.

        ##### Solution

```python
import heapq
from collections import defaultdict
def min_debt(debt):
    dic = defaultdict(int)
    for borrower, lender, amount in debt:
        dic[borrower] -= amount
        dic[lender] += amount
    sorted_debt = sorted(dic.items(), key = lambda x: (x[1], x[0]))
    res = []
    heapq.heapify(sorted_debt)
    name, money = sorted_debt[0]
    while sorted_debt and sorted_debt[0][1] == money:
        res.append(heapq.heappop(sorted_debt)[0])
    return res
if __name__ == "__main__":
    '''
    debt = [['Alex','Blake',2],
            ['Blake','Alex',2],
            ['Casey','Alex',5],
            ['Blake','Casey',7],
            ['Alex','Blake',4],
            ['Alex','Casey',4]]
    '''
    debt = [['clex', 'Blake', 2],
            ['Blake', 'clex', 2],
            ]
    res = min_debt(debt)
    print(res)
```



- Amazon Basics has several suppliers for its products. For each of the products, the stock is represented by a list of a number of items for each supplier. As items are purchased, the supplier raises the price by 1 per item purchased. Let's assume Amazon's profit on any single item is the same as the number of items the supplier has left. For example, if a supplier has 4 items, Amazon's profit on the first item sold is 4, then 3, then 2 and the profit of the last one is 1.

  

  Given a list where each value in the list is the number of the item at a given supplier and also given the number of items to be ordered, write an algorithm to find the highest profit that can be generated for the given product.

  

  Input
  The input to the function/method consists on three arguments:

  

  numSuppliers, an integer representing the number of suppliers;

  

  inventory, a list of long integers representing the value of the item at a given supplier;

  

  order, a long integer representing the number of items to be ordered.

  

  Output

  

  Return a long integer representing the highest profit that can be generated for the given product.

  

  Constraints

  

  1 <= numSuppliers <= 10^5

  

  1 <= inventory[i] <= 10 ^ 5

  

  0 <= i < numSuppliers

  

  1 <= orders <= sum of inventory

  

  Example1

  

  Input:

  

  numSuppliers = 2

  

  inventory = [3,5]

  

  order = 6

  

  Output:

  

  19

  ##### Solution

  ```python
  from collections import defaultdict
  def highest_profit(numSuppliers, inventory, order):
      dic = defaultdict(int)
      for price in inventory:
          dic[price] += 1
      cur_max_price = max(dic.keys())
      res = 0
      while order > 0:
          max_price_count = min(order, dic[cur_max_price])
          res += max_price_count * cur_max_price
          order -= max_price_count
          dic[cur_max_price] -= max_price_count
          dic[cur_max_price - 1] += max_price_count
          if dic[cur_max_price] == 0:
              cur_max_price -= 1
      return res
  ```

- <img src="C:\Users\gcy\AppData\Roaming\Typora\typora-user-images\image-20201013172258630.png" alt="image-20201013172258630" style="zoom:50%;" />

  

<img src="C:\Users\gcy\AppData\Roaming\Typora\typora-user-images\image-20201013172322664.png" alt="image-20201013172322664" style="zoom:50%;" />

```python
# my original solution, using backtrack
from math import sqrt
def split_prime(string):
    if not string: return 0
    memo = dict()

    def is_prime(str):
        num = int(str)
        if num > 1:
            if num == 2: return True
            if num % 2 == 0: return False
            for i in range(3, int(sqrt(num)) + 1, 2):
                if num % i == 0: return False
            return True
        return False

    def backtrack(index):
        if index == len(string): return []
        if index in memo: return memo[index]
        res = []
        for i in range(index, len(string)):
            if string[index] == '0': continue
            temp = string[index : i + 1]
            left = backtrack(i + 1)
            if not left:
                if is_prime(temp):
                    res.append([int(temp)])
            else:
                for l in left:
                    if is_prime(temp):
                        res.append([int(temp)] + l)
                    # if is_prime(temp + str(l[0])):
                    #     res.append([int(temp + str(l[0]))] + l[1:])
        memo[index] = res
        return res
    r = backtrack(0)
    print(r)
    return len(r) % 100000007

if __name__ == "__main__":
    res = split_prime("11373")
    print(res)

######################there is no need to generate all the substrings################
from math import sqrt
def split_prime(string):
    is_prime_dp = dict()
    memo = dict()
    def is_prime(s):
        num = int(s)
        if num in is_prime_dp: return is_prime_dp[num]
        if num > 1:
            if num == 2: return True
            if num % 2 == 0: return False
            ceil = int(sqrt(num)) + 1
            for i in range(3, ceil, 2):
                if num % i == 0: return False
            return True
        return False
    def backtrack(index):
        if index == len(string):
            return 1
        if index in memo: return memo[index]
        res = 0
        if string[index] == '0': return 0
        for i in range(index, len(string)):
            temp = string[index : i + 1]
            if is_prime(temp):
                res += backtrack(i + 1)
        memo[index] = res
        return res
    return backtrack(0)
```



- A virtual memory management system in an operating system at Amazon can use LeastRecently-Used (LRU) cache. When a requested memory page is not in the cache and the cache is full, the page that was least-recently-used should be removed from the cache to make room for the requested page. If the cache is not full, the requested page can simply be added to the cache and considered the most-recently-used page in the cache. A given page should occur at most once in the cache.

  

  Given the maximum size of the cache and a list of page requests, write an algorithm to calculate the number of cache misses. A cache miss occurs when a page is requested and isn't found in the cache.

  

  **Input**

  

  The input to the function/method consists of three arguments:

  

  num, an integer representing the number of pages;

  

  pages, a list of integers representing the pages requested;

  

  maxCacheSize, an integer representing the size of the cache.

  

  **Output**

  

  Return an integer representing the number of cache misses.

  

  **Note**

  

  The cache is initially empty and the list contains pages numbered in the range 1-50. A page at index "i" in the list is requested before a page at index "i+1".

  

  **Constraints**

  

  0 <= i < num

  

  **Example**

  

  **Input:**

  

  num = 6

  

  pages = [1,2,1,3,1,2]

  

  maxCacheSize = 2

  

  **Output:**

  

  4

  

  **Explanation:**

  

  Cache state as requests come in ordered longest-time-in-cache to shortest-time-in-cache:

  

  1*

  

  1,2*

  

  2,1

  

  1,3*

  

  3,1

  

  1,2*

  ##### Solution

  ```python
  from collections import OrderedDict
  def cache_page(num, pages, maxCacheSize):
      cache = OrderedDict()
      capacity = 0
      miss = 0
      for page in pages:
          if page in cache:
              cache.move_to_end(page, last = True)
          else:
              miss += 1
              cache[page] = None
              capacity += 1
              if capacity > maxCacheSize:
                  cache.popitem(last = False)
                  capacity -= 1
      return miss
  if __name__ == "__main__":
      num = 6
      pages = [1,2,1,3,1,2]
      maxCacheSize = 2
      res = cache_page(num, pages, maxCacheSize)
      print(res)
  
  ```

- ![image-20201013204143761](C:\Users\gcy\AppData\Roaming\Typora\typora-user-images\image-20201013204143761.png)

![image-20201013204208820](C:\Users\gcy\AppData\Roaming\Typora\typora-user-images\image-20201013204208820.png)

```python
# greedy 
#sort the offloading time decending and sort the buildingopentime ascending
def earliest_time(numOfBuildings, buildingOpenTime, offLoadTime):
    buildingOpenTime.sort()
    offLoadTime.sort(reverse = True)
    res = float('-inf')
    for i in range(numOfBuildings):
        a, b = buildingOpenTime[i], offLoadTime[i * 4]
        res = max(res, a + b)
    return res
if __name__ == "__main__":
    a,b,c = 2, [8, 10], [2,2,3,1,8,7,4,5]
    res = earliest_time(a,b,c)
    print(res)
```



- **Shopping Patterns**

  

  Amazon is trying to understand customer shopping patterns and offer items that are regularly bought together to new customers. Each item that has been bought together can be represented as an undirected graph where edges join often bundled products. A group of *n* products is uniquely numbered from 1 of *product_nodes*. A *trio* is defined as a group of three related products that all connected by an edge. Trios are scored by counting the number of related products outside of the trio, this is referred as a *product sum*.

  

  Given product relation data, determine the minimum product sum for all trios of related products in the group. If no such trio exists, return -1.

  

  **Example**
  *products_nodes = 6*
  *products_edges = 6*
  *products_from = [1,2,2,3,4,5]*
  *products_to = [2,4,5,5,5,6]*

  

  | Product | Related Products |
  | :-----: | :--------------: |
  |    1    |        2         |
  |    2    |     1, 4, 5      |
  |    3    |        5         |
  |    4    |       2, 5       |
  |    5    |    2, 3, 4, 6    |
  |    6    |        5         |

  

  ![image](https://assets.leetcode.com/users/images/9d9e18e9-c480-4012-9083-8e20170153d3_1601446461.5111852.png)

  

  *A graph of n = 6 products where the only trip of related products is {2, 4, 5}*

  

  The product scores based on the graph above are :

  

  | Product | Outside Products | Which Products Are Outside |
  | :-----: | :--------------: | :------------------------: |
  |    2    |        1         |             1              |
  |    4    |        0         |                            |
  |    5    |        2         |            3, 6            |

  

  In the diagram above, the total product score is *1 + 0 + 2 = 3* for the trio *{2, 4, 5}.*

  

```python
from collections import defaultdict
def shopping_patterns(product_nodes, products_edges, products_from, products_to):
    graph = defaultdict(set)
    for i in range(products_edges):
        from_node, to_node = products_from[i], products_to[i]
        graph[from_node].add(to_node)
        graph[to_node].add(from_node)
    print(graph)
    res = float('inf')
    for i in range(products_edges):
        a, b = products_from[i], products_to[i]
        for c in graph[a] & graph[b]:
            res = min(res, len(graph[a]) - 2 + len(graph[b]) - 2 + len(graph[c]) - 2)
    return res
if __name__ == "__main__":
    a,b,c,d = 6, 6,  [1,2,2,3,4,5], [2,4,5,5,5,6]
    res = shopping_patterns(a,b,c,d)
    print(res)
```

- \236. Lowest Common Ancestor of a Binary Tree

  Medium

  4395184Add to ListShare

  Given a binary tree, find the lowest common ancestor (LCA) of two given nodes in the tree.

  According to the [definition of LCA on Wikipedia](https://en.wikipedia.org/wiki/Lowest_common_ancestor): “The lowest common ancestor is defined between two nodes p and q as the lowest node in T that has both p and q as descendants (where we allow **a node to be a descendant of itself**).”

   

  **Example 1:**

  ![img](https://assets.leetcode.com/uploads/2018/12/14/binarytree.png)

  ```
  Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 1
  Output: 3
  Explanation: The LCA of nodes 5 and 1 is 3.
  ```

  **Example 2:**

  ![img](https://assets.leetcode.com/uploads/2018/12/14/binarytree.png)

  ```
  Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 4
  Output: 5
  Explanation: The LCA of nodes 5 and 4 is 5, since a node can be a descendant of itself according to the LCA definition.
  ```

  **Example 3:**

  ```python
  Input: root = [1,2], p = 1, q = 2
  Output: 1
  ```

  ##### Solution

  ```python
  class Solution:
      def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode':
          if not root: return None
          if p == root or q == root: return root
          left = self.lowestCommonAncestor(root.left, p, q)
          right = self.lowestCommonAncestor(root.right, p, q)
          if not left: return right
          elif not right: return left
          else: return root
  ```

- Given a binary tree and its two nodes.
  Find the **number of turns** needed to reach from one node to other node.

  

  Examples:

  

  Consider the binary tree as shown below :

  

  ```
                     1
                  /     \
                 2        3
               /   \    /   \
              4     5   6     7
  ```

  - 

    Input : Above Binary tree and two nodes [5] & [6]
    Output: 3

    

  - 

    Input : Above Binary tree and two nodes [1] & [7]
    Output: 0

  ##### Solution

  ```python
  # Find the lowest common ancestor first and then from the LCA to find the turns. If the previous node is a left child and current child is a right node, one turn appears. Vice versa. If the current node is one of the current target node, count the turns into final result.
  from collections import deque
  def findLowestCommonAncestor(root, p, q):
      if not root: return None
      if root == p or root == q: return root
      left = findLowestCommonAncestor(root.left, p, q)
      right = findLowestCommonAncestor(root.right, p, q)
      if not left: return right
      if not right: return left
      return root
  def countTurns(root, p, q):
      lca = findLowestCommonAncestor(root, p, q)
      turns = 0
      queue = deque()
      queue.append((lca, None, 0))
      while queue:
          node, stateFlag, count = queue.popleft()
          if node.left:
              queue.append((node.left, 'l', count + 1 if stateFlag == 'r' else count))
          if node.left == p or node.left == q:
              turns += queue[-1][2]
          if node.right:
              queue.append((node.right, 'r', count + 1 if stateFlag == 'l' else count))
          if node.right == p or node.left == q:
              turns += queue[-1][2]
      if lca in {p, q}: return turns
      else: return turns + 1
  ```

- \937. Reorder Data in Log Files

  Easy

  7922371Add to ListShare

  You have an array of `logs`. Each log is a space delimited string of words.

  For each log, the first word in each log is an alphanumeric *identifier*. Then, either:

  - Each word after the identifier will consist only of lowercase letters, or;
  - Each word after the identifier will consist only of digits.

  We will call these two varieties of logs *letter-logs* and *digit-logs*. It is guaranteed that each log has at least one word after its identifier.

  Reorder the logs so that all of the letter-logs come before any digit-log. The letter-logs are ordered lexicographically ignoring identifier, with the identifier used in case of ties. The digit-logs should be put in their original order.

  Return the final order of the logs.

   

  **Example 1:**

  ```python
  Input: logs = ["dig1 8 1 5 1","let1 art can","dig2 3 6","let2 own kit dig","let3 art zero"]
  Output: ["let1 art can","let3 art zero","let2 own kit dig","dig1 8 1 5 1","dig2 3 6"]
  ```

  ##### Solution

  ```python
  class Solution:
      def reorderLogFiles(self, logs: List[str]) -> List[str]:
          alpha, digit = [], []
          for i, log in enumerate(logs):
              log = log.split(' ')
              if log[1].isnumeric():
                  digit.append(log)
              else:
                  alpha.append(log)
          alpha.sort(key = lambda x: (x[1:], x[0]))
          res_temp = alpha + digit
          return [' '.join(i) for i in res_temp]
  ```

- Given 2 lists `a` and `b`. Each element is a pair of integers where the first integer represents the unique id and the second integer represents a value. Your task is to find an element from `a` and an element form `b` such that the sum of their values is less or equal to `target` and as close to `target` as possible. Return a list of ids of selected elements. If no pair is possible, return an empty list.

  

  **Example 1:**

  

  ```
  Input:
  a = [[1, 2], [2, 4], [3, 6]]
  b = [[1, 2]]
  target = 7
  
  Output: [[2, 1]]
  
  Explanation:
  There are only three combinations [1, 1], [2, 1], and [3, 1], which have a total sum of 4, 6 and 8, respectively.
  Since 6 is the largest sum that does not exceed 7, [2, 1] is the optimal pair.
  ```

  

  **Example 2:**

  

  ```
  Input:
  a = [[1, 3], [2, 5], [3, 7], [4, 10]]
  b = [[1, 2], [2, 3], [3, 4], [4, 5]]
  target = 10
  
  Output: [[2, 4], [3, 2]]
  
  Explanation:
  There are two pairs possible. Element with id = 2 from the list `a` has a value 5, and element with id = 4 from the list `b` also has a value 5.
  Combined, they add up to 10. Similarily, element with id = 3 from `a` has a value 7, and element with id = 2 from `b` has a value 3.
  These also add up to 10. Therefore, the optimal pairs are [2, 4] and [3, 2].
  ```

  

  **Example 3:**

  

  ```
  Input:
  a = [[1, 8], [2, 7], [3, 14]]
  b = [[1, 5], [2, 10], [3, 14]]
  target = 20
  
  Output: [[3, 1]]
  ```

  

  **Example 4:**

  

  ```python
  Input:
  a = [[1, 8], [2, 15], [3, 9]]
  b = [[1, 8], [2, 11], [3, 12]]
  target = 20
  
  Output: [[1, 3], [3, 2]]
  ```

  ##### Solution

  ```python
  def optimizeUtilization(a, b, target):
      a.sort(key = lambda x : x[1])
      b.sort(key = lambda x : x[1])
      size_a, size_b = len(a), len(b)
      res = []
      diff = float('inf')
      i, j = 0, size_b - 1
      while i < size_a and j >= 0:
          value_a, value_b = a[i][1], b[j][1]
          cur_sum = value_a + value_b
          cur_diff = - cur_sum + target
          if 0 <= cur_diff < diff:
              diff = cur_diff
              res.clear()
              res.append([a[i][0], b[j][0]])
          elif cur_diff == diff:
              res.append([a[i][0], b[j][0]])
          if cur_diff <= 0:
              j -= 1
          else: i += 1
      return res
  if __name__ == "__main__":
      a = [[1, 8], [2, 15], [3, 9]]
      b = [[1, 8], [2, 11], [3, 12]]
      target = 20
      res = optimizeUtilization(a,b,target)
      print(res)
  
  
  ```

- Given:

  

  ```python
    5
   /  \ 
  3   7
    9
   / \
  5   12
    \
     7
  Returns:
  7
  ```

  ##### Solution

  ```python
  def put_into_stack(stack, root):
      while root:
          stack.append(root)
          root = root.right
  def largest_common_number(root_1, root_2):
      stack_1, stack_2 = [], []
      put_into_stack(stack_1, root_1)
      put_into_stack(stack_2, root_2)
      while stack_1 and stack_2:
          val_1, val_2 = stack_1[-1].val, stack_2[-1].val
          if val_1 == val_2: return val_1
          if val_1 < val_2: 
              node = stack_2.pop()
              put_into_stack(stack_2, node.left)
          else:
              node = stack_1.pop()
              put_into_stack(stack_1, node.left)
      return -1
  ```

- Given a map `Map> userSongs` with user names as keys and a list of all the songs that the user has listened to as values.

  

  Also given a map `Map> songGenres`, with song genre as keys and a list of all the songs within that genre as values. The song can only belong to only one genre.

  

  The task is to return a map `Map>`, where the key is a user name and the value is a list of the user's favorite genre(s). Favorite genre is the most listened to genre. A user can have more than one favorite genre if he/she has listened to the same number of songs per each of the genres.

  

  **Example 1:**

  

  ```
  Input:
  userSongs = {  
     "David": ["song1", "song2", "song3", "song4", "song8"],
     "Emma":  ["song5", "song6", "song7"]
  },
  songGenres = {  
     "Rock":    ["song1", "song3"],
     "Dubstep": ["song7"],
     "Techno":  ["song2", "song4"],
     "Pop":     ["song5", "song6"],
     "Jazz":    ["song8", "song9"]
  }
  
  Output: {  
     "David": ["Rock", "Techno"],
     "Emma":  ["Pop"]
  }
  
  Explanation:
  David has 2 Rock, 2 Techno and 1 Jazz song. So he has 2 favorite genres.
  Emma has 2 Pop and 1 Dubstep song. Pop is Emma's favorite genre.
  ```

  

  **Example 2:**

  

  ```python
  Input:
  userSongs = {  
     "David": ["song1", "song2"],
     "Emma":  ["song3", "song4"]
  },
  songGenres = {}
  
  Output: {  
     "David": [],
     "Emma":  []
  }
  ```

  ##### Solution

  ```python
  from collections import defaultdict
  def favorite_song(user_songs, song_generes):
      print(user_songs)
      song_gener_dic = dict()
      for gener, song_list in song_generes.items():
          for song in song_list:
              song_gener_dic[song] = gener
      res = defaultdict(list)
      print(song_gener_dic)
  
      for user, songs in user_songs.items():
          max_frequency = 0
          gen_frequency_dic = defaultdict(int)
          for song in songs:
              if song in song_gener_dic:
                  gen = song_gener_dic[song]
                  gen_frequency_dic[gen] += 1
                  if gen_frequency_dic[gen] > max_frequency:
                      res[user].clear()
                      res[user].append(gen)
                      max_frequency = gen_frequency_dic[gen]
                  elif gen_frequency_dic[gen] == max_frequency:
                      res[user].append(gen)
      return res
  if __name__ == "__main__":
      userSongs = dict()
      userSongs["David"] = ["song1", "song2"]
      userSongs["Emma"] = ["song5", "song6"]
      songGenres = {
      }
      r = favorite_song(userSongs, songGenres)
      print(r)
  
  ```

- https://assets.leetcode.com/users/images/d290f3fb-fde2-4e1e-9c5d-a7f74b111812_1600553631.8503802.png

  ##### Solution

  ```python
  def data_center(size_0, n, mult, offset, mod_val, max_area):
      wall_lengths = list()
      possible_combinations = 1 if size_0 * size_0 <= max_area else 0
      wall_lengths.append(size_0)
      previous_len = size_0
      while len(wall_lengths) <= n:
          cur_count = 0
          cur_len = ((mult * previous_len + offset) % mod_val) + 1 + previous_len
          previous_len = cur_len
          if cur_len * cur_len <= max_area:
              cur_count += 2 * len(wall_lengths) + 1
          else:
              cur_count += 2 * (binary_search(wall_lengths, cur_len, max_area) + 1)
          wall_lengths.append(cur_len)
          possible_combinations += cur_count
          if cur_count == 0: break
      return possible_combinations
  def binary_search(arr, cur_length, max_area):
      left, right = 0, len(arr) - 1
      while left <= right:
          mid = left + (right - left) // 2
          if cur_length * arr[mid] < max_area:
              left += 1
          elif cur_length * arr[mid] > max_area:
              right -= 1
          else:
              return mid
      return left - 1
  if __name__ == "__main__":
      r = data_center(2,3,3,3,2,15)
      print(r)
  
  
  
  
  ```

- **Input**
  The input to the function/method consists of five arguments - **numCompetitors**, an integer representing the number of competitors for the Echo device;
  **topNCompetitors**, is an integer representing the maximum number of competitors that Amazon wants to identify;
  **competitors**, a list of strings representing the competitors;
  **numReviews**, an integer representing the number of reviews from different websites that are identified by the automated webcrawler;
  **reviews**, a list of string where each element is a string that consists of space-separated words representing user reviews.

  

  **Output**
  Return a list of strings representing Amazon's top N competitors in order of most frequently mentioned to least frequent.

  

  **Note**
  The comparison of strings is case-insensitive. If the value of topNCompetitors is more than the number of competitors discussed in the reviews then output the names of only the competitors mention.
  If competitors have the same count (e.g. newshop=2, shopnow=2, mymarket=4), sort alphabetically. topNCompetitors=2, Output=[mymarket, newshop]

  

  **Example**
  Input:
  numCompetitors=6
  topNCompetitors = 2
  competitors = [newshop, shopnow, afashion, fashionbeats, mymarket, tcellular]
  numReviews = 6
  reviews = [
  "newshop is providing good services in the city; everyone should use newshop",
  "best services by newshop",
  "fashionbeats has great services in the city",
  "I am proud to have fashionbeats",
  "mymarket has awesome services",
  "Thanks Newshop for the quick delivery"]

  

  **Output**
  ["newshop", "fashionbeats"]

  

  **Explanation**
  "newshop" is occurring in 3 different reviews. "fashionbeats" is occuring in 2 different user reviews and "mymarket" is occurring in only 1 review.

  

  ```python
  public List<string> TopNumCompetitors(int numCompetitors,
                                          int topNCompetitors,
                                          List<string> competitors,
                                          int numReviews, List<string> reviews)
  {
  	// Your code here
  }
  ```

  ##### Solution

  ```python
  from collections import defaultdict
  def num_of_competitors(numCompetitors, topNCompetitors, competitors, numReviews, reviews):
      competitors = set(competitors)
      dic = defaultdict(int)
      for review in reviews:
          review = review.lower()
          words = review.split(' ')
          visited = set()
          for word in words:
              if word in competitors and word not in visited:
                  visited.add(word)
                  dic[word] += 1
      temp = sorted(dic.items(), key = lambda x: (x[1], x[0]), reverse = True)
      return [t[0] for t in temp[:topNCompetitors]]
  ```

- Given a series of child-parent relations like
  ['dog', 'mammal'],
  ["shark, fish"],
  ["cat", "mammal"],
  ["mammal", "animal"],
  ['fish', 'animal']

  

  capture the relationship of these entities so you can print the
  relationships in a *nested format* at any point.

  

  Notes:

  

  - Siblings may be returned in any order.
  - Your add function will be called multiple times to add relationships

  

  Example Outputs (any are valid):

  

  ```python
  Option 1:
  animal
    fish
      shark
    mammal
      dog
      cat
  
  Option 2:
  {
    "value": "animal",
    "children": [
      {
        "value": "fish",
        "children": [
          {
            "value": "shark",
            "children": []
          }
        ]
      },
      {
        "value": "mammal",
        "children": [
          {
            "value": "dog",
            "children": []
          },
          {
            "value": "cat",
            "children": []
          }
        ]
      }
    ]
  }
  
  Option 3:
  {
    "animal": {
      "fish": {
        "shark": {}
      },
      "mammal": {
        "cat": {},
        "dog": {}
      }
    }
  }
  ```

  ##### Solution

  ```python
  from collections import defaultdict
  def child_parent_relations(relations):
      degree_dic = defaultdict(int)
      parent_child_dic = defaultdict(list)
      node_set = set()
      for relation in relations:
          print(relation)
          child, parent = relation
          node_set.add(child)
          node_set.add(parent)
          degree_dic[child] += 1
          parent_child_dic[parent].append(child)
      root = None
      for node in node_set:
          if degree_dic[node] == 0:
              root = node
      def dfs(root, ti):
          if not root: return
          t = ti.setdefault(root, {})
          for neighbor in parent_child_dic[root]:
              degree_dic[neighbor] -= 1
              if degree_dic[neighbor] == 0:
                  dfs(neighbor, t)
      trie = {}
      dfs(root, trie)
      return trie
  ```

- 