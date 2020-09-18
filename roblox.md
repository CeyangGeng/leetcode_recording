 

# roblox

1. # [[LeetCode\] 256. Paint House 粉刷房子](https://www.cnblogs.com/grandyang/p/5319384.html)

    

   There are a row of *n* houses, each house can be painted with one of the three colors: red, blue or green. The cost of painting each house with a certain color is different. You have to paint all the houses such that no two adjacent houses have the same color.

   The cost of painting each house with a certain color is represented by a `*n* x *3*` cost matrix. For example, `costs[0][0]` is the cost of painting house 0 with color red; `costs[1][2]` is the cost of painting house 1 with color green, and so on... Find the minimum cost to paint all houses.

   Note:
   All costs are positive integers.

   Example:

   ```
   Input: [[17,2,17],[16,16,5],[14,3,19]]
   Output: 10
   Explanation: Paint house 0 into blue, paint house 1 into green, paint house 2 into blue. 
                Minimum cost: 2 + 5 + 3 = 10.
   ```

   ```python
   def paint(costs):
       if not costs: return 0
       dp = costs
       size = len(dp)
       for i in range(1, size):
           for j in range(3):
               dp[i][j] += min(dp[i - 1][(j + 1) % 3]， dp[i - 1][(j + 2) % 3])
       return min(dp[size - 1][0], dp[size - 1][1], dp[size - 1][2])
   ```

2. ### Leetcode: Paint House II

   There are a row of *n* houses, each house can be painted with one of the *k* colors. The cost of painting each house with a certain color is different. You have to paint all the houses such that no two adjacent houses have the same color.

   The cost of painting each house with a certain color is represented by a `*n* x *k*` cost matrix. For example, `costs[0][0]` is the cost of painting house 0 with color 0; `costs[1][2]` is the cost of painting house 1 with color 2, and so on... Find the minimum cost to paint all houses.

   ```python
   def paint(costs):
       if not costs: return 0
       m, n = len(costs), len(costs[0])
       dp_1, dp_2 = costs[0], [float('inf') for _ in range(n)]
       for i in range(1, m):
           for j in range(n):
               for k in range(n):
                   if k != j:
                       dp_2[j] = min(dp_2[j], dp_1[k] + costs[i][j])
               dp_1 = dp_2
               dp_2 = [float('inf') for _ in range(n)]
       return min(dp_1)        
   
   ```

3. \1473. Paint House III

   Hard

   27010Add to ListShare

   There is a row of `m` houses in a small city, each house must be painted with one of the `n` colors (labeled from 1 to `n`), some houses that has been painted last summer should not be painted again.

   A neighborhood is a maximal group of continuous houses that are painted with the same color. (For example: houses = [1,2,2,3,3,2,1,1] contains 5 neighborhoods [{1}, {2,2}, {3,3}, {2}, {1,1}]).

   Given an array `houses`, an `m * n` matrix `cost` and an integer `target` where:

   - `houses[i]`: is the color of the house `i`, **0** if the house is not painted yet.
   - `cost[i][j]`: is the cost of paint the house `i` with the color `j+1`.

   Return the minimum cost of painting all the remaining houses in such a way that there are exactly `target` neighborhoods, if not possible return **-1**.

    

   **Example 1:**

   ```
   Input: houses = [0,0,0,0,0], cost = [[1,10],[10,1],[10,1],[1,10],[5,1]], m = 5, n = 2, target = 3
   Output: 9
   Explanation: Paint houses of this way [1,2,2,1,1]
   This array contains target = 3 neighborhoods, [{1}, {2,2}, {1,1}].
   Cost of paint all houses (1 + 1 + 1 + 1 + 5) = 9.
   ```

   **Example 2:**

   ```
   Input: houses = [0,2,1,2,0], cost = [[1,10],[10,1],[10,1],[1,10],[5,1]], m = 5, n = 2, target = 3
   Output: 11
   Explanation: Some houses are already painted, Paint the houses of this way [2,2,1,2,2]
   This array contains target = 3 neighborhoods, [{2,2}, {1}, {2,2}]. 
   Cost of paint the first and last house (10 + 1) = 11.
   ```

   **Example 3:**

   ```
   Input: houses = [0,0,0,0,0], cost = [[1,10],[10,1],[1,10],[10,1],[1,10]], m = 5, n = 2, target = 5
   Output: 5
   ```

   **Example 4:**

   ```
   Input: houses = [3,1,2,3], cost = [[1,1,1],[1,1,1],[1,1,1],[1,1,1]], m = 4, n = 3, target = 3
   Output: -1
   Explanation: Houses are already painted with a total of 4 neighborhoods [{3},{1},{2},{3}] different of target = 3.
   ```

    

   **Constraints:**

   - `m == houses.length == cost.length`
   - `n == cost[i].length`
   - `1 <= m <= 100`
   - `1 <= n <= 20`
   - `1 <= target <= m`
   - `0 <= houses[i] <= n`
   - `1 <= cost[i][j] <= 10^4`

   ```python
   1473. Paint House III
   Hard
   
   270
   
   10
   
   Add to List
   
   Share
   There is a row of m houses in a small city, each house must be painted with one of the n colors (labeled from 1 to n), some houses that has been painted last summer should not be painted again.
   
   A neighborhood is a maximal group of continuous houses that are painted with the same color. (For example: houses = [1,2,2,3,3,2,1,1] contains 5 neighborhoods  [{1}, {2,2}, {3,3}, {2}, {1,1}]).
   
   Given an array houses, an m * n matrix cost and an integer target where:
   
   houses[i]: is the color of the house i, 0 if the house is not painted yet.
   cost[i][j]: is the cost of paint the house i with the color j+1.
   Return the minimum cost of painting all the remaining houses in such a way that there are exactly target neighborhoods, if not possible return -1.
   
    
   
   Example 1:
   
   Input: houses = [0,0,0,0,0], cost = [[1,10],[10,1],[10,1],[1,10],[5,1]], m = 5, n = 2, target = 3
   Output: 9
   Explanation: Paint houses of this way [1,2,2,1,1]
   This array contains target = 3 neighborhoods, [{1}, {2,2}, {1,1}].
   Cost of paint all houses (1 + 1 + 1 + 1 + 5) = 9.
   Example 2:
   
   Input: houses = [0,2,1,2,0], cost = [[1,10],[10,1],[10,1],[1,10],[5,1]], m = 5, n = 2, target = 3
   Output: 11
   Explanation: Some houses are already painted, Paint the houses of this way [2,2,1,2,2]
   This array contains target = 3 neighborhoods, [{2,2}, {1}, {2,2}]. 
   Cost of paint the first and last house (10 + 1) = 11.
   Example 3:
   
   Input: houses = [0,0,0,0,0], cost = [[1,10],[10,1],[1,10],[10,1],[1,10]], m = 5, n = 2, target = 5
   Output: 5
   Example 4:
   
   Input: houses = [3,1,2,3], cost = [[1,1,1],[1,1,1],[1,1,1],[1,1,1]], m = 4, n = 3, target = 3
   Output: -1
   Explanation: Houses are already painted with a total of 4 neighborhoods [{3},{1},{2},{3}] different of target = 3.
    
   
   Constraints:
   
   m == houses.length == cost.length
   n == cost[i].length
   1 <= m <= 100
   1 <= n <= 20
   1 <= target <= m
   0 <= houses[i] <= n
   1 <= cost[i][j] <= 10^4
   ```

4.  String Compression

   Medium

   8892671Add to ListShare

   Given an array of characters `chars`, compress it using the following algorithm:

   Begin with an empty string `s`. For each group of **consecutive repeating characters** in `chars`:

   - If the group's length is 1, append the character to `s`.
   - Otherwise, append the character followed by the group's length.

   The compressed string `s` **should not be returned separately**, but instead be stored **in the input character array `chars`**. Note that group lengths that are 10 or longer will be split into multiple characters in `chars`.

   After you are done **modifying the input array**, return *the new length of the array*.

   **Follow up:**
   Could you solve it using only `O(1)` extra space?

    

   **Example 1:**

   ```
   Input: chars = ["a","a","b","b","c","c","c"]
   Output: Return 6, and the first 6 characters of the input array should be: ["a","2","b","2","c","3"]
   Explanation: The groups are "aa", "bb", and "ccc". This compresses to "a2b2c3".
   ```

   **Example 2:**

   ```
   Input: chars = ["a"]
   Output: Return 1, and the first character of the input array should be: ["a"]
   Explanation: The only group is "a", which remains uncompressed since it's a single character.
   ```

   **Example 3:**

   ```
   Input: chars = ["a","b","b","b","b","b","b","b","b","b","b","b","b"]
   Output: Return 4, and the first 4 characters of the input array should be: ["a","b","1","2"].
   Explanation: The groups are "a" and "bbbbbbbbbbbb". This compresses to "ab12".
   ```

   **Example 4:**

   ```
   Input: chars = ["a","a","a","b","b","a","a"]
   Output: Return 6, and the first 6 characters of the input array should be: ["a","3","b","2","a","2"].
   Explanation: The groups are "aaa", "bb", and "aa". This compresses to "a3b2a2". Note that each group is independent even if two groups have the same character.
   ```

    

   **Constraints:**

   - `1 <= chars.length <= 2000`
   - `chars[i]` is a lower-case English letter, upper-case English letter, digit, or symbol.

   ```python
   class Solution:
       def compress(self, chars: List[str]) -> int:
           i, j, k, size = 0, 0, 0, len(chars)
           while j < size:
               if chars[j] == chars[i]:
                   j += 1
               else:
                   if j - i == 1:
                       chars[k] = chars[i]
                       k += 1
                   else:
                       chars[k] = chars[i]
                       length = str(j - i)
                       for s in length:
                           k += 1
                           chars[k] = s
                       k += 1
                   i = j
           if i < size:
               if i == size - 1:
                   chars[k] = chars[i]
                   k += 1
               else:
                   chars[k] = chars[i]
                   l = str(j - i)
                   for ll in l:
                       k += 1
                       chars[k] = ll
                   k += 1
           return k 
   ```

5. Piles of Boxes
   题干： 给一堆高度不同的箱子堆 每一step可以把最高的那堆减到第二高的高度 问要多少steps可以让所有箱子堆一样高度
   example： [3,2,1] -> [2,2,1] -> [2,1,1] -> [1,1,1] 3 steps
   解法： python用collections.Coutner 其他语言可以直接hashmap计数不同的高度 然后把unique的高度排序 求 count*index的和就行
   [5,5,2,1] -> 计数{5:2, 2:1, 1:1} -> 排序[1,2,5] -> 求和 0 * 1 + 1 * 1 + 2 * 2 = 5steps

   ```python
   from collections import Counter
   def helper(piles):
       dic = Counter(piles)
       height = sorted(dic.keys())
       res = 0
       for i, h in enumerate(height):
           res += i * dic[h]
       return res
   if __name__ == "__main__":
       piles = [5,5,2,1]
       r = helper(piles)
       print(r)
   ```

6. University Career Fair

   ```python
   def arrange(arrival, duration):
       size = len(arrival)
       intervals = []
       for i in range(size):
           intervals.append([arrival[i], arrival[i] + duration[i]])
       intervals.sort(key = lambda i: i[1])
       count = 0
       end_time = intervals[0][1]
       for i in range(1, size):
           if intervals[i][0] < end_time:
               continue
           else:
               count += 1
               end_time = intervals[i][1]
       return count
   ```

7. ![img](https://oss.1point3acres.cn/forum/202009/16/235600usin1181r2cjzqq1.png)

```python
def helper(scores, k):
    scores.sort(reverse = True)
    j = k
    res, size = k, len(scores)
    while j < size and scores[j] == scores[j - 1]:
        res += 1
        j += 1
    return res
if __name__ == "__main__":
    scores = [2,2,3,4,5]
    k = 4
    r = helper(scores, k)
    print(r)
```

8. ![image-20200917194140640](C:\Users\gcy\AppData\Roaming\Typora\typora-user-images\image-20200917194140640.png)

```python
def ship(boxes, unitsperbox, trucksize):
    size, dic = len(boxes), {}
    for i in range(size):
        dic[unitsperbox[i]] = boxes[i]
    units = sorted(dic.keys(), reverse = True)
    count = 0
    for unit in units:
        number = dic[unit]
        if trucksize < number:
            count += trucksize * unit
            break
        count += unit * dic[unit]
        trucksize -= dic[unit]
    return count
if __name__ == "__main__":
    boxes = [1,2,3]
    unitsperbox = [3,2,1]
    trucksize = 3
    r = ship(boxes, unitsperbox, trucksize)
    print(r)
```

9. ![image-20200917195745443](C:\Users\gcy\AppData\Roaming\Typora\typora-user-images\image-20200917195745443.png)

```python
def ancestral_names(names):
    dic = {"I":1, "II":2, "III":3, "IV":4, "V":5, "VI":6, "VII":7, "VIII":8, "IX":9, "X":10, "L":50, "XL":40, "XXX":30, "XX":20}
    prefix = ["L", "XL", "XXX", "XX", "X"]
    for i, name in enumerate(names):
        first, second = name.split(" ")
        found = False
        for pre in prefix:
            if second.startswith(pre):
                found = True
                break
        if found:
            length = len(pre)
            left_number = 0
            if len(second) > length:
                left_number = dic[second[length:]]
            number = dic[pre] + left_number
        else:
            number = dic[second]
        new_name = first + str(number)
        names[i] = new_name

    names.sort()
    return names
```

10. ![image-20200917203310276](C:\Users\gcy\AppData\Roaming\Typora\typora-user-images\image-20200917203310276.png)

```python
def common_prefix_length(s):
    size = len(s)
    total = 0
    for i in range(size):
        right = s[i:]
        min_len = size - i
        count = 0
        for j in range(min_len):
            if s[j] == right[j]:
                count += 1
            else:
                break
        total += count
    return total
if __name__ == "__main__":
    r = common_prefix_length("abcabcd")
    print(r)
```

11. 

![img](https://oss.1point3acres.cn/forum/202009/15/123720ugnillkvv2aagvsw.jpg)

```python
def word_compress(word, k):
    if k == 1: return word[-1]
    stack = []
    for w in word:
        if not stack or stack[-1][0] != w:
            stack.append((w, 1))
        elif w == stack[-1][0]:
            if stack[-1][1] + 1 < k:
                stack.append((w, stack[-1][1] + 1))
            else:
                count = k - 1
                while count > 0:
                    stack.pop()
                    count -= 1
    return stack
if __name__ == "__main__":
    word = "abbcccb"
    r = word_compress(word, 3)
    res = ''.join([x[0] for x in r])
    print(res)
```

12. ![img](https://oss.1point3acres.cn/forum/202009/15/123709fhsmscbiiptyiigy.jpg)

```python
def slowest_key(key_times):
    start_time = 0
    max_time = float('-inf')
    max_key = -1
    for key, time in key_times:
        time_interval = time - start_time
        if time_interval > max_time:
            max_time = time_interval
            max_key = key
        start_time = time
    return max_time, max_key
```

13.

