





# robinhood oa

1. > <img src="C:\Users\gcy\AppData\Roaming\Typora\typora-user-images\image-20200906131255127.png" alt="image-20200906131255127" style="zoom:50%;" />
   >
   > ```python
   > import heapq
   > def find(nums):
   >     size = len(nums)
   >     nums.append(float('-inf'))
   >     prev = [size] + list(range(size))
   >     next = list(range(1, size + 1)) + [0]
   >     peaks = []
   >     def __check_peak(i):
   >         if nums[prev[i]] < nums[i] > nums[next[i]]:
   >             heapq.heappush(peaks, (nums[i], i))
   >     for i in range(size):
   >         __check_peak(i)
   >     res = []
   >     while peaks:
   >         val, index = heapq.heappop(peaks)
   >         res.append(val)
   >         pre_ele, next_ele = prev[index], next[index]
   >         prev[next_ele] = pre_ele
   >         next[pre_ele] = next_ele
   >         __check_peak(pre_ele)
   >         __check_peak(next_ele)
   >     return res
   > if __name__ == "__main__":
   >     nums = [2,7,8,5,1,6,3,9,4]
   >     r = find(nums)
   >     print(r)
   > ```

2. > \121. Best Time to Buy and Sell Stock
   >
   > Easy
   >
   > 5863253Add to ListShare
   >
   > Say you have an array for which the *i*th element is the price of a given stock on day *i*.
   >
   > If you were only permitted to complete at most one transaction (i.e., buy one and sell one share of the stock), design an algorithm to find the maximum profit.
   >
   > Note that you cannot sell a stock before you buy one.
   >
   > **Example 1:**
   >
   > ```
   > Input: [7,1,5,3,6,4]
   > Output: 5
   > Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
   >              Not 7-1 = 6, as selling price needs to be larger than buying price.
   > ```
   >
   > **Example 2:**
   >
   > ```python
   > Input: [7,6,4,3,1]
   > Output: 0
   > Explanation: In this case, no transaction is done, i.e. max profit = 0.
   > ```
   >
   > Solution
   >
   > ```python
   > class Solution:
   >     def maxProfit(self, prices: List[int]) -> int:
   >         size = len(prices)
   >         if size < 2: return 0
   >         max_profit = 0
   >         min_price = prices[0]
   >         for price in prices[1:]:
   >             if price < min_price:
   >                 min_price = price
   >             else:
   >                 max_profit = max(max_profit, price - min_price)
   >         return max_profit
   > ```

3. 

   > 1. Best Time to Buy and Sell Stock II
   >
   >    Say you have an array `prices` for which the *i*th element is the price of a given stock on day *i*.
   >
   >    Design an algorithm to find the maximum profit. You may complete as many transactions as you like (i.e., buy one and sell one share of the stock multiple times).
   >
   >    **Note:** You may not engage in multiple transactions at the same time (i.e., you must sell the stock before you buy again).
   >
   >    **Example 1:**
   >
   >    ```
   >    Input: [7,1,5,3,6,4]
   >    Output: 7
   >    Explanation: Buy on day 2 (price = 1) and sell on day 3 (price = 5), profit = 5-1 = 4.
   >                 Then buy on day 4 (price = 3) and sell on day 5 (price = 6), profit = 6-3 = 3.
   >    ```
   >
   >    **Example 2:**
   >
   >    ```
   >    Input: [1,2,3,4,5]
   >    Output: 4
   >    Explanation: Buy on day 1 (price = 1) and sell on day 5 (price = 5), profit = 5-1 = 4.
   >                 Note that you cannot buy on day 1, buy on day 2 and sell them later, as you are
   >                 engaging multiple transactions at the same time. You must sell before buying again.
   >    ```
   >
   >    **Example 3:**
   >
   >    ```
   >    Input: [7,6,4,3,1]
   >    Output: 0
   >    Explanation: In this case, no transaction is done, i.e. max profit = 0.
   >    ```
   >
   >     
   >
   >    **Constraints:**
   >
   >    - `1 <= prices.length <= 3 * 10 ^ 4`
   >    - `0 <= prices[i] <= 10 ^ 4`
   >
   >    Solution: grab all the increasing trends
   >
   >    ```python
   >    class Solution:
   >        def maxProfit(self, prices: List[int]) -> int:
   >            max_profit = 0
   >            size = len(prices)
   >            if size < 2: return 0
   >            for i in range(1, size):
   >                if prices[i] > prices[i - 1]:
   >                    max_profit += prices[i] - prices[i - 1]
   >            return max_profit
   >    ```

4. > \123. Best Time to Buy and Sell Stock III
   >
   > Hard
   >
   > 258179Add to ListShare
   >
   > Say you have an array for which the *i*th element is the price of a given stock on day *i*.
   >
   > Design an algorithm to find the maximum profit. You may complete at most *two* transactions.
   >
   > **Note:** You may not engage in multiple transactions at the same time (i.e., you must sell the stock before you buy again).
   >
   >  
   >
   > **Example 1:**
   >
   > ```
   > Input: prices = [3,3,5,0,0,3,1,4]
   > Output: 6
   > Explanation: Buy on day 4 (price = 0) and sell on day 6 (price = 3), profit = 3-0 = 3.
   > Then buy on day 7 (price = 1) and sell on day 8 (price = 4), profit = 4-1 = 3.
   > ```
   >
   > **Example 2:**
   >
   > ```
   > Input: prices = [1,2,3,4,5]
   > Output: 4
   > Explanation: Buy on day 1 (price = 1) and sell on day 5 (price = 5), profit = 5-1 = 4.
   > Note that you cannot buy on day 1, buy on day 2 and sell them later, as you are engaging multiple transactions at the same time. You must sell before buying again.
   > ```
   >
   > **Example 3:**
   >
   > ```
   > Input: prices = [7,6,4,3,1]
   > Output: 0
   > Explanation: In this case, no transaction is done, i.e. max profit = 0.
   > ```
   >
   > **Example 4:**
   >
   > ```
   > Input: prices = [1]
   > Output: 0
   > ```
   >
   >  
   >
   > **Constraints:**
   >
   > - `1 <= prices.length <= 105`
   > - `0 <= prices[i] <= 105`
   >
   > Solution: dp
   >
   > ```python
   > class Solution:
   >     def maxProfit(self, prices: List[int]) -> int:
   >         dp_i_1_0 = 0
   >         dp_i_1_1 = float('-inf')
   >         dp_i_2_0 = 0
   >         dp_i_2_1 = float('-inf')
   >         for price in prices:
   >             dp_i_2_0 = max(dp_i_2_0, dp_i_2_1 + price)
   >             dp_i_2_1 = max(dp_i_2_1, dp_i_1_0 - price)
   >             dp_i_1_0 = max(dp_i_1_0, dp_i_1_1 + price)
   >             dp_i_1_1 = max(dp_i_1_1, -price)
   >         return dp_i_2_0
   > ```

5. > \188. Best Time to Buy and Sell Stock IV
   >
   > Hard
   >
   > 1685104Add to ListShare
   >
   > Say you have an array for which the *i-*th element is the price of a given stock on day *i*.
   >
   > Design an algorithm to find the maximum profit. You may complete at most **k** transactions.
   >
   > **Note:**
   > You may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).
   >
   > **Example 1:**
   >
   > ```
   > Input: [2,4,1], k = 2
   > Output: 2
   > Explanation: Buy on day 1 (price = 2) and sell on day 2 (price = 4), profit = 4-2 = 2.
   > ```
   >
   > **Example 2:**
   >
   > ```python
   > Input: [3,2,6,5,0,3], k = 2
   > Output: 7
   > Explanation: Buy on day 2 (price = 2) and sell on day 3 (price = 6), profit = 6-2 = 4.
   >              Then buy on day 5 (price = 0) and sell on day 6 (price = 3), profit = 3-0 = 3.
   > ```
   >
   > Solution: 
   >
   > ```python
   > class Solution:
   >     def helper(self, prices):
   >         size = len(prices)
   >         max_profit = 0
   >         for i in range(1, size):
   >             if prices[i] > prices[i - 1]:
   >                 max_profit += (prices[i] - prices[i - 1])
   >         return max_profit
   >                 
   >     def maxProfit(self, k: int, prices: List[int]) -> int:
   >         size = len(prices)
   >         if k >= size // 2:
   >             return self.helper(prices)
   >         dp = [[[0 for _ in range(2)] for _ in range(k + 1)] for _ in range(size)]
   >         for i in range(size):
   >             for j in range(1, k + 1):
   >                 if i == 0:
   >                     dp[0][j][0] = 0
   >                     dp[0][j][1] = -prices[i]
   >                     continue
   >                 dp[i][j][0] = max(dp[i - 1][j][0], dp[i - 1][j][1] + prices[i])
   >                 dp[i][j][1] = max(dp[i - 1][j][1], dp[i - 1][j - 1][0] - prices[i])
   >         return dp[size - 1][k][0]
   > ```

6. > \309. Best Time to Buy and Sell Stock with Cooldown
   >
   > Medium
   >
   > 286090Add to ListShare
   >
   > Say you have an array for which the *i*th element is the price of a given stock on day *i*.
   >
   > Design an algorithm to find the maximum profit. You may complete as many transactions as you like (ie, buy one and sell one share of the stock multiple times) with the following restrictions:
   >
   > - You may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).
   > - After you sell your stock, you cannot buy stock on next day. (ie, cooldown 1 day)
   >
   > **Example:**
   >
   > ```python
   > Input: [1,2,3,0,2]
   > Output: 3 
   > Explanation: transactions = [buy, sell, cooldown, buy, sell]
   > ```
   >
   > Solution
   >
   > ```python
   > class Solution:
   >     def maxProfit(self, prices: List[int]) -> int:
   >         dp_i_k_0 = 0
   >         dp_i_k_1 = float('-inf')
   >         dp_i_pre_0 = 0
   >         for price in prices:
   >             temp = dp_i_k_0
   >             dp_i_k_0 = max(dp_i_k_0, dp_i_k_1 + price)
   >             dp_i_k_1 = max(dp_i_k_1, dp_i_pre_0 - price)
   >             dp_i_pre_0 = temp
   >         return dp_i_k_0
   > ```

7. > \714. Best Time to Buy and Sell Stock with Transaction Fee
   >
   > Medium
   >
   > 170450Add to ListShare
   >
   > Your are given an array of integers `prices`, for which the `i`-th element is the price of a given stock on day `i`; and a non-negative integer `fee` representing a transaction fee.
   >
   > You may complete as many transactions as you like, but you need to pay the transaction fee for each transaction. You may not buy more than 1 share of a stock at a time (ie. you must sell the stock share before you buy again.)
   >
   > Return the maximum profit you can make.
   >
   > **Example 1:**
   >
   > ```
   > Input: prices = [1, 3, 2, 8, 4, 9], fee = 2
   > Output: 8
   > Explanation: The maximum profit can be achieved by:
   > Buying at prices[0] = 1Selling at prices[3] = 8Buying at prices[4] = 4Selling at prices[5] = 9The total profit is ((8 - 1) - 2) + ((9 - 4) - 2) = 8.
   > ```
   >
   > 
   >
   > **Note:**
   >
   > `0 < prices.length <= 50000`.
   >
   > `0 < prices[i] < 50000`.
   >
   > `0 <= fee < 50000`.
   >
   > Solution
   >
   > ```python
   > class Solution:
   >     def maxProfit(self, prices: List[int], fee: int) -> int:
   >         dp_i_0 = 0
   >         dp_i_1 = float('-inf')
   >         for price in prices:
   >             dp_i_0 = max(dp_i_0, dp_i_1 + price)
   >             dp_i_1 = max(dp_i_1, dp_i_0 - price - fee)
   >         return dp_i_0
   > ```

8. > <img src="C:\Users\gcy\AppData\Roaming\Typora\typora-user-images\image-20200906161931702.png" alt="image-20200906161931702" style="zoom:50%;" />
   >
   > ```python
   > def helper(prices, algo, k):
   >     cur_sum, size = 0, len(prices)
   >     for i in range(size):
   >         if algo[i] == 0:
   >             cur_sum -= prices[i]
   >         else:
   >             cur_sum += prices[i]
   >     print(cur_sum)
   >     left = 0
   >     while algo[left] == 1:
   >         left += 1
   >     right = left
   >     increase = 0
   >     max_inc = 0
   >     while right < size:
   >         if algo[right] == 0:
   >             increase += 2 * prices[right]
   >         if right - left + 1 == k:
   >             max_inc = max(max_inc, increase)
   >             if algo[left] == 0:
   >                 increase -= 2 * prices[left]
   >             left += 1
   >             while algo[left] == 1 and left <= right:
   >                 left += 1
   >         elif right == size - 1 and right - left + 1 < k:
   >             max_inc = max(max_inc, increase)
   >         right += 1
   >     print(max_inc)
   >     return cur_sum + max_inc
   > 
   > if __name__ == "__main__":
   >     prices = [2,4,1,5,2,6,7]
   >     algo = [0,1,0,0,1,0,0]
   >     r = helper(prices, algo, 4)
   >     print(r)
   > 
   > ```

9. > ![image-20200906175135084](C:\Users\gcy\AppData\Roaming\Typora\typora-user-images\image-20200906175135084.png)
   >
   > ```python
   > def rev(num):
   >     res = 0
   >     while num:
   >         res = res * 10 + num % 10
   >         num //= 10
   >     return res
   > if __name__ == '__main__':
   >     r = rev(123344536)
   >     print(r)
   > ```
   >
   > 

10. > ![image-20200906182147542](C:\Users\gcy\AppData\Roaming\Typora\typora-user-images\image-20200906182147542.png)
    >
    > ```python
    > from collections import defaultdict
    > def reduction(array):
    >     m = len(array)
    >     counter, graph = defaultdict(int), defaultdict(list)
    >     for a, b in array:
    >         counter[a] += 1
    >         counter[b] += 1
    >         graph[a].append(b)
    >         graph[b].append(a)
    >     for num, times in counter.items():
    >         if times == 1:
    >             break
    >     res = []
    >     stack = [num]
    >     visit = {num}
    >     while stack:
    >         n = stack.pop()
    >         res.append(n)
    >         for adj in graph[n]:
    >             if adj not in visit:
    >                 visit.add(adj)
    >                 stack.append(adj)
    >     return res
    > ```

11. > ![image-20200906194027056](C:\Users\gcy\AppData\Roaming\Typora\typora-user-images\image-20200906194027056.png)
    >
    > maintain three stuff: the copy board, last_operations only including the insert, paste and delete, deleted texts.
    >
    > ```python
    > def helper(operations):
    >     res = ''
    >     previous_operations_apart_from_undo_and_undo_related = []
    >     deleted_texts = []
    >     copy_board = ""
    >     for operation in operations:
    >         op_split = operation.split(' ')
    >         op = op_split[0]
    >         if op == 'INSERT':
    >             if len(op_split) == 2:
    >                 val = op_split[1]
    >                 previous_operations_apart_from_undo_and_undo_related.append((op, len(res)))
    >                 res += val
    > 
    >         if op == 'COPY':
    >             if len(op_split) == 2:
    >                 index = int(op_split[1])
    >                 if index < len(res):
    >                     copy_board = res[index :]
    > 
    >         if op == 'DELETE':
    >             len_op = len(previous_operations_apart_from_undo_and_undo_related)
    >             for j in range(len_op - 1, -1, -1):
    >                 if previous_operations_apart_from_undo_and_undo_related[j][0] in {'INSERT', 'PASTE'}:
    >                     last_end = previous_operations_apart_from_undo_and_undo_related[j][1]
    >                     deleted_texts.append(res[last_end:])
    >                     res = res[:last_end]
    >                     break
    >             previous_operations_apart_from_undo_and_undo_related.append((op, len(res)))
    > 
    >         if op == 'PASTE':
    >             if copy_board:
    >                 previous_operations_apart_from_undo_and_undo_related.append((op, len(res)))
    >                 res += copy_board
    > 
    >         if op == 'UNDO':
    >             if previous_operations_apart_from_undo_and_undo_related:
    >                 pre_op, start_index = previous_operations_apart_from_undo_and_undo_related.pop()
    >                 if pre_op == 'DELETE':
    >                     res += deleted_texts.pop()
    >                 if pre_op == 'INSERT' or pre_op == 'PASTE':
    >                     res = res[:start_index]
    >     return res
    > 
    > if __name__ == '__main__':
    >     operations = ["INSERT Da", "COPY 0", "UNDO", "PASTE", "PASTE", "COPY 2", "PASTE", "PASTE", "DELETE", "UNDO", "INSERT aaan"]
    >     r = helper(operations)
    >     print(r)
    > 
    > ```

12. > ![image-20200906194940675](C:\Users\gcy\AppData\Roaming\Typora\typora-user-images\image-20200906194940675.png)
    >
    > ```python
    > def backtrack(arr, pieces):
    >     if not arr: return True
    >     for i, piece in enumerate(pieces):
    >         size = len(piece)
    >         if arr[:size] == piece:
    >             if backtrack(arr[size:], pieces[:i] + pieces[i + 1:]):
    >                 return True
    >     return False
    > if __name__ == "__main__":
    >     arr = [1,2,5,3,6]
    >     pieces = [[5], [1,2], [3]]
    >     print(backtrack(arr, pieces))
    > ```

13. > ![image-20200906213034013](C:\Users\gcy\AppData\Roaming\Typora\typora-user-images\image-20200906213034013.png)
    >
    > ```python
    > from collections import Counter
    > def helper(a, b, queries):
    >     res = []
    >     counter_a = Counter(a)
    >     counter_b = Counter(b)
    >     for query in queries:
    >         if len(query) == 2:
    >             target = query[1]
    >             counter_a = Counter(a)
    >             counter_b = Counter(b)
    >             pair_count = 0
    >             for key, val in counter_a.items():
    >                 if target - key in counter_b:
    >                     pair_count += val * counter_b[target - key]
    >             res.append(pair_count)
    >         else:
    >             index, tar = query[1:]
    >             counter_b[b[index]] -= 1
    >             counter_b[target] = counter_b.setdefault(tar, 0) + 1
    >             b[index] = tar
    >     return res
    > if __name__ == "__main__":
    >     a = [1,2,3]
    >     b = [3,4]
    >     query = [[1,5], [0,0,1], [1,5]]
    >     r = helper(a, b, query)
    >     print(r)
    > ```

14. > ![image-20200906213400568](C:\Users\gcy\AppData\Roaming\Typora\typora-user-images\image-20200906213400568.png)
    >
    > 



15. > ![image-20200906220727829](C:\Users\gcy\AppData\Roaming\Typora\typora-user-images\image-20200906220727829.png)
    >
    > ```python
    > def tri(s):
    >     res = []
    >     size = len(s)
    >     for i in range(size - 2):
    >         temp = s[i : i + 3]
    >         if is_distinct(temp):
    >             res.append(temp)
    >     return res
    > def is_distinct(temp):
    >     a, b, c = temp[0], temp[1], temp[2]
    >     return a != b and a != c and b != c
    > if __name__  == "__main__":
    >     s = "abcabcabcccc"
    >     print(tri(s))
    > ```

16. > ![image-20200906221355150](C:\Users\gcy\AppData\Roaming\Typora\typora-user-images\image-20200906221355150.png)
    >
    > ```python
    > def add_str(a, b):
    >     if len(a) > len(b):
    >         a, b = b, a
    >     min_size = len(a)
    >     res = ''
    >     for j in range(-1, - min_size - 1, -1):
    >         s_a = int(a[j])
    >         s_b = int(b[j])
    >         r = str(s_a + s_b)
    >         res = r + res
    >     size_b = len(b)
    >     res = b[-size_b : -min_size] + res
    >     return res
    > if __name__ == "__main__":
    >     a = '123'
    >     b = '9999999'
    >     r = add_str(a, b)
    >     print(r)
    > ```

17. > ![image-20200907000609379](C:\Users\gcy\AppData\Roaming\Typora\typora-user-images\image-20200907000609379.png)
    >
    > ```python
    > def rotate(matrix, k):
    >     size = len(matrix)
    >     vertexes = [[0,0], [0, size - 1], [size - 1, size - 1], [size - 1, 0]]
    >     for i in range(size // 2):
    >         start = vertexes[0][0]
    >         end = vertexes[1][1]
    >         indexes = []
    >         res = []
    >         for j in range(start + 1, end):
    >             indexes.append([start, j])
    >             res.append(matrix[start][j])
    >         for j in range(start + 1, end):
    >             indexes.append([j, end])
    >             res.append(matrix[j][end])
    >         for j in range(end - 1, start, -1):
    >             indexes.append([end, j])
    >             res.append(matrix[end][j])
    >         for j in range(end - 1, start, -1):
    >             indexes.append([j, start])
    >             res.append(matrix[j][start])
    >         size = len(indexes)
    >         len_per_part = size // 4
    >         left_part = len_per_part * (4 - k)
    >         res = res[left_part:] + res[:left_part]
    >         while indexes:
    >             x, y = indexes.pop()
    >             val = res.pop()
    >             matrix[x][y] = val
    >         vertexes = [[start + 1, start + 1], [start + 1, end - 1], [end - 1, end - 1],[end - 1, start + 1]]
    >     return matrix
    > 
    > if __name__ == '__main__':
    >     matrix = [[1,2,3,4,5],\
    >               [6,7,8,9,10],\
    >               [11,12,13,14,15],\
    >               [16,17,18,19,20],\
    >               [21,22,23,24,25]]
    >     k = 1
    >     r = rotate(matrix, k)
    >     print(r)
    > ```

    18. 

    > ![image-20200907003305306](C:\Users\gcy\AppData\Roaming\Typora\typora-user-images\image-20200907003305306.png)
    >
    > ```
    > 
    > ```
    >
    > 