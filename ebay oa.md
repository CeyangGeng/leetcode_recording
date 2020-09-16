# ebay oa

1. ![image-20200916120338049](C:\Users\gcy\AppData\Roaming\Typora\typora-user-images\image-20200916120338049.png)

```python
def merge(s, t):
    size_s, size_t = len(s), len(t)
    res = ''
    i, j = 0, 0
    while i < size_s and j < size_t:
        res += s[i] + t[j]
        i, j = i + 1, j + 1
    if i < size_s:
        res += s[i:]
    if j < size_t:
        res += t[j:]
    return res
if __name__ == "__main__":
    s = "aaa"
    t = "bbbbbbb"
    r = merge(s, t)
    print(r)
```

2. ![image-20200916122539859](C:\Users\gcy\AppData\Roaming\Typora\typora-user-images\image-20200916122539859.png)

```python
def helper(number, i, k):
    temp = ''
    if i + k <= len(number):
        temp = number[i : i + k]
    else:
        temp = number[i:]
    total = 0
    for n in temp:
        total += int(n)
    return str(total)

def reduce_number(number, k):
    while len(number) > k:
        total = ''
        for i in range(0, len(number), k):
            total += helper(number, i, k)
        number = total
    return number

if __name__ == "__main__":
    r = reduce_number("11111222222", 3)
    print(r)
```

3. ![image-20200916130929943](C:\Users\gcy\AppData\Roaming\Typora\typora-user-images\image-20200916130929943.png)

```python
def text_simulator(operations):
    previous_operation_can_be_undone = []
    copy_board = ''
    res = ''
    for operation_val in operations:
        operation_split = operation_val.split(' ')
        operation = operation[0]
        if operation == 'INSERT':
            if len(operation_split) == 2:
                val = operation_split[1]
                previous_operation_can_be_undone.append((operation, len(res), val))
                res += val
        if operation == 'COPY':
            if len(operation_split) == 2:
                index = operation_split[1]
                if index < len(res):
                    copy_board = res[index :]
        if operation == 'PASTE':
            previous_operation_can_be_undone.append((operation, len(res), copy_board))
            res += copy_board
        if operation == 'UNDO':
            if previous_operation_can_be_undone:
                last_operation, end_index, text = previous_operation_can_be_undone.pop()
                if last_operation == 'PASTE' or last_operation == 'INSERT':
                    res = res[:end_index]
                if last_operation == 'DELETE':
                    res += text
    return res
```

4. ![image-20200916135841666](C:\Users\gcy\AppData\Roaming\Typora\typora-user-images\image-20200916135841666.png)

```python
def is_anagram(a, b):
    if a == b: return True
    a = str(a)
    b = str(b)
    size_a, size_b = len(a), len(b)
    if size_a != size_b:
        return False
    return sorted(list(a)) == sorted(list(b))
def find(nums):
    count = 0
    size = len(nums)
    res = []
    for i in range(size - 1):
        for j in range(i + 1, size):
            if is_anagram(nums[i], nums[j]):
                count += 1
                res.append((i, j))
    return count, res
if __name__ == "__main__":
    nums = [25,35,872,228,53,278,872]
    r , res= find(nums)
    print(r, res)
```

5.  给一个正整数n，问从0到n这n+1个整数里面，digit’0’,’2’,’4’共出现多少次，返回count

```python
from collections import Counter
def times(nums):
    count = 0
    for num in range(nums + 1):
        dic = Counter(str(num))
        count += dic['0'] + dic['2'] + dic['4']
    return count
if __name__ == "__main__":
    r = times(2)
    print(r)
```

6. 给一个string类型的number，找能被3整除的substring所代表的整数的个数，返回count。这个整数不能有leading zeros。单独的0可以。
     如：”456”：4，5，6，45，56，456，一共有3个能被3整除；”303”:3,0,3,30,03(不算),303，一共有5个。

```python
def find(number):
    num_str = str(number)
    size = len(num_str)
    count = 0
    for i in range(size):
        if num_str[i] == '0':
            count += 1
            continue
        for j in range(i + 1, size + 1):
            sub_str = num_str[i:j]
            sub_int = int(sub_str)
            if sub_int % 3 == 0:
                count += 1
    return count
if __name__ == "__main__":
    a = "303"
    r = find(a)
    print(r)
```

7. 俄罗斯方块题类似俄罗斯方块，给了一个matrix，'f‘ 表示俄罗斯方块，’#‘表示障碍，求该俄罗斯方块接触障碍或者接触地面的时候matrix的样子.

```python
def helper(matrix):
    if not matrix: return matrix
    m, n = len(matrix), len(matrix[0])
    min_dis = float('inf')
    for j in range(n):
        last_obstacle_index = -1
        for i in range(m - 1, -1, -1):
            if matrix[i][j] == '#':
                last_obstacle_index = i
            if matrix[i][j] == 'F':
                if last_obstacle_index != -1:
                    min_dis = min(last_obstacle_index - i - 1, min_dis)
                else:
                    min_dis = min(m - 1 - i, min_dis)
    for j in range(n):
        for i in range(m - 1, -1, -1):
            if matrix[i][j] == '.' and matrix[i - min_dis][j] == 'F':
                matrix[i][j] = 'F'
                matrix[i - min_dis][j] = '.'
    return matrix
```

4. 给一串正整数，找两个数arr与arr[j]，可以满足：arr+rev(arr[j]) = arr[j]+rev(arr)。主要是实现一个rev()功能，如345->543,240->42,10600->601。最后问有多少种情况，返回count。

```python
def reverse(num):
    ret = 0
    while num:
        ret = ret * 10 + num % 10
    return ret
def helper(arr):
    dic = defaultdict(int)
    for num in arr:
        num_rev = reverse(num)
        diff = num - num_rev
        dic[diff] += 1
    res = 0
    for v in dic.values():
        res += v * v
    return res
```

5. Given a string containing digits from `2-9` inclusive, return all possible letter combinations that the number could represent.

   A mapping of digit to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.

   ![img](https://upload.wikimedia.org/wikipedia/commons/thumb/7/73/Telephone-keypad2.svg/200px-Telephone-keypad2.svg.png)

   **Example:**

   ```
   Input: "23"
   Output: ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].
   ```

   **Note:**

   Although the above answer is in lexicographical order, your answer could be in any order you want.

   ```python
   class Solution:
       def letterCombinations(self, digits: str) -> List[str]:
           if not digits: return []
           dic = {'2':'abc', '3':'def', '4':'ghi', '5':'jkl', '6':'mno', '7':'pqrs', '8':'tuv', '9':'wxyz'}
           res = ['']
           for num in digits:
               temp = []
               for alpha in dic[num]:
                   for cur in res:
                       temp.append(cur + alpha)
               res = temp
           return res
   ```

   