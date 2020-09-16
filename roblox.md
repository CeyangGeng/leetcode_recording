 

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

4. 