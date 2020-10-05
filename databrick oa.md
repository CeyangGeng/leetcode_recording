# databrick oa

1. \1. goodTuples: 给一个数组nums，返回满足特定条件的sublist个数：sublist长度为3，其中unique number个数为2

   ```python
   def is_unique(arr):
       return len(set(arr)) == 2
   def find_unique(nums):
       size = len(nums)
       count = 0
       for i in range(size - 2):
           if is_unique(nums[i : i + 3]):
               count += 1
       return count
   if __name__ == "__main__":
       nums = [1,2,3,4,4,5,6,7,7]
       r = find_unique(nums)
       print(r)
   ```

2. reduceTheNumber: input( string表示一个int， int k) 将string尽量分割成多个大小为k模块（若剩余部分长度小于k，单独做一个模块），每个模块中数字想加后拼接起来得到新的str数字。
   若str长度仍大于k，重复上述过程。返回处理完的str

   ```python
   def compute(arr):
       num = int(arr)
       total = 0
       while num:
           total += num % 10
           num //= 10
       return str(total)
   def reduce_number(s, k):
       while len(s) > k:
           res = ''
           for i in range(0, len(s), k):
               temp = ''
               if i + k > len(s):
                   temp = s[i:]
               else:
                   temp = s[i : i + k]
               res += compute(temp)
           s = res
       return s
   if __name__ == "__main__":
       s = "101212678"
       k = 3
       r = reduce_number(s, k)
       print(r)
   ```

3. sortChessSubsquares: 一个matrix，黑白相间。 一行query，每个query（x,y,m），(x,y)代表submatrix左上角坐标，m代表submatrix边长
   submatrix中所有黑色块上int从小到大排序重新放置到submatrix上，要求所有黑色块排序后还是处在限定submatrix中黑色块上（白色同理排序+重新放置）

   ```python
   def helper(nums, query):
       x, y, length = query
       even_numbers, even_index, odd_numbers, odd_index = [], [], [], []
       for i in range(x, x + length):
           for j in range(y, y + length):
               if (i + j) & 1:
                   odd_numbers.append(nums[i][j])
                   odd_index.append((i, j))
               else:
                   even_numbers.append(nums[i][j])
                   even_index.append((i, j))
       odd_numbers.sort()
       even_numbers.sort()
       size_odd, size_even = len(odd_numbers), len(even_numbers)
       for i in range(size_odd):
           nums[odd_index[i]] = odd_numbers[i]
       for j in range(size_even):
           nums[even_index[j]] = even_numbers[j]
   ```

4. maxArithmeticLength: 两个nums 数组a 和b。能从b中拿出任意数量int放置到数组a任意位置上，求能组成最长等差数列的长度。不能组成返回-1。

   ```
   
   ```

5. 第三题是MutateMatrix，一个矩阵，一些query，0是顺时针转90度，1是关于主对角线对称，2是关于副对角线对称，输出所有操作完成之后的矩阵。
    最好可以对query做一些处理，不过我时间不够了就写的最简单的。

   ```python
   # rotate 90 degree = up-down reverse and main diagonal reverse
   def swap(nums, index_1, index_2):
       x_1, y_1 = index_1
       x_2, y_2 = index_2
       nums[x_1][y_1], nums[x_2][y_2] = nums[x_2][y_2], nums[x_1][y_1]
   
   def reverse_main_dignose(nums):
       m, n = len(nums), len(nums[0])
       for i in range(m):
           for j in range(i):
               swap(nums, (i, j), (j, i))
       return nums
   def up_down_reverse(nums):
       m, n = len(nums), len(nums[0])
       for i in range(m // 2):
           for j in range(n):
               swap(nums, (i, j), (m - i, j))
       return nums
   def reverse_second_dignose(nums):
       m, n = len(nums), len(nums[0])
       for i in range(m):
           for j in range(n - i):
               swap(nums, (i, j), (m - i, m - j))
   ```

6.  removePairsGame
   题干：Alice和Bob玩游戏，给出一个数组例如 [3,4,1,1,4,5]，每次可以从数组中移除2个连续且相等的数字，比如 [3,4,1,1,4,5] -> [3,4,4,5] -> [3,5]，游戏进行直到无法移除更多的数字。谁动不了谁就输。Alice先行。

   ```python
   def remove_pairs(nums):
       stack = []
       count = 0
       for num in nums:
           if not stack or stack[-1] != num:
               stack.append(num)
           else:
               count += 1
               stack.pop()
       return count & 1
   ```

7. 第四题是ShuffleThePieces，一个数组arr，一个二维数组pieces，问是否能把pieces拼成原来的数组。
    例如arr是[1, 2, 5, 3]，pieces是[[1, 2], [3], [5]]，输出true。
    再比如arr是[1, 2, 5, 3, 6]，pieces是[[1, 2], [5], [6, 3]]，输出false。
    我用map存了arr每个数的index，然后开始查看pieces，一旦出现index断开、乱序，或者map找不到return false，最后再比较下长度.

   ```
   
   ```

8. 给一个 n * n matrix, 每一行从最左面的cell开始，向右上角走，直到到了boundary，然后继续向右下角走，该path 上面的所有cell数值的总和，是该left_most cell 的weight。
           最终返回一个长度为n的list 包含所有的left_most cell, 先根据weight 排序(ascending)，如果存在tie, 就按cell的大小排序(ascending)。
           例如：input = [[2, 3, 2], [0, 2, 5], [1, 0, 1]], output = [1, 2, 0],
           解释：row0 left most: 2, weight = 2 + 2 + 1 = 5; row1 left_most:0, wieght = 0 + 3 + 5 = 8; row2 left_most: 1, weight = 1 + 2 + 2 = 5.

   ```python
   def find(matrix):
       m = len(matrix)
       res = []
       for i in range(m):
           total = 0
           count = 0
           k = 1
           x, y = i, 0
           while count < m:
               total += matrix[x][y]
               if x == 0:
                   k = -1
               if k == 1:
                   x -= 1
                   y += 1
               if k == -1:
                   x += 1
                   y += 1
               count += 1
           res.append(total)
       return res
   
   if __name__ == "__main__":
       matrix = [[2,3,2],[0,2,5],[1,0,1]]
       r = find(matrix)
       print(r)
   ```

9. maxArithmeticLength: 两个nums 数组a 和b。能从b中拿出任意数量int放置到数组a任意位置上，求能组成最长等差数列的长度。不能组成返回-1。

   ```python
   class Solution(object):
       def longestArithSeqLength(self, A):
           """
           :type A: List[int]
           :rtype: int
           """
           dp = {}
           for i in xrange(len(A)):
               for j in xrange(i + 1, len(A)):
                   dp[j, A[j] - A[i]] = dp.get((i, A[j] - A[i]), 1) + 1
           return max(dp.values())
   ```

10. ![image-20200921183130769](C:\Users\gcy\AppData\Roaming\Typora\typora-user-images\image-20200921183130769.png)

       

```python
def beauty_number(matrix, k):
    m = len(matrix)
    dic = dict()
    for i in range(0, m, k):
        for j in range(0, m, k):
            temp = set()
            for x in range(i, i + k):
                for y in range(j, j + k):
                    temp.add(matrix[x][y])
            min_num = 1
            while True:
                if min_num not in temp:
                    dic[min_num] = (i, j)
                    break
                min_num += 1
    new_matrix = [[0 for _ in range(m)] for _ in range(m)]
    for i, num in enumerate(sorted(dic.keys())):
        row, col = i // m, i % m
        r, c = row * k, col * k
        rr, rc = dic[num]
        for t in range(k):
            for s in range(k):
                new_matrix[rr + t][rc + s] = matrix[r + t][c + s]
    return new_matrix
```

11. <img src="C:\Users\gcy\AppData\Roaming\Typora\typora-user-images\image-20200921185558070.png" alt="image-20200921185558070" style="zoom:50%;" />

    ```python
    def construct(n):
        res = ['' for _ in range(n)]
        res[0] = '*' * n
        res[-1] = '*' * n
        for i in range(1, n - 1):
            res[i] = '*' + ' ' * (n - 2) + '*'
        return res
    ```

12. <img src="C:\Users\gcy\AppData\Roaming\Typora\typora-user-images\image-20200921193953925.png" alt="image-20200921193953925" style="zoom:50%;" />

```python
def find(arr):
    contain, res = set(), []
    for i in range(3):
        for j in range(3):
            contain.add(arr[i][j])
    res.append(len(contain) == 9)
    n = len(arr[0])
    for j in range(3, n - 2):
        for i in range(3):
            contain.remove(arr[i][j - 3])
            contain.add(arr[i][j])
        res.append(len(contain) == 9)
    return res
```

13.<img src="C:\Users\gcy\AppData\Roaming\Typora\typora-user-images\image-20200921204626841.png" alt="image-20200921204626841" style="zoom:50%;" />

```python
from collections import Counter, defaultdict
def find(a):
    res = []
    dic = defaultdict(int)
    for num in a:
        temp = Counter(str(num))
        if temp in res:
            dic[res.index(temp)] += 1
        else:
            dic[len(res)] += 1
            res.append(temp)
    total = 0
    for val in dic.values():
        total += val * (val - 1) // 2
    return total
if __name__ == "__main__":
    a = [25, 35, 872, 228, 53, 278, 872]
    r = find(a)
    print(r)
```





