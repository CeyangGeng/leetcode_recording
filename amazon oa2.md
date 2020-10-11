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

  