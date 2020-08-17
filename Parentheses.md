# Parentheses

> I use the same thought to solve these two parentheses problem. 
>
> - Traverse in the normal order and reverse order.  When traverse in the normal order, the parse should be ("(", ")"). After reversing the string, the parse should be ("(", ")").
> - The most common two methods for resolving parentheses problems are stack and counter.  For the stack method, whenever meet with the open parentheses, we should push the previous string into the stack; whenever meet with the closed parentheses, the stack should pop out string in the stack. For the counter method, we increase the counter when come across with the open parentheses and decrease the counter when meet with the close parentheses.
> - Whenever the counter becomes negative, we should remove the extra close parentheses. To avoid repeat consequence, for example, for the string "())", the consequence is the same when we remove the s[1] or s[2], we can stipulate that we should remove the first of the contiguous close parentheses(j = last_j or (j > last_j and s[j - 1]!= parse[1]))
> - Besides,  there exists another kind of repeat consequence, for example, "())())", we could remove s[1]  first and then s[4], or we could remove s[4] first and then s[1]. To avoid this kind of repeat, we can use last_j to mark the last removal position and next time we can only remove characters after this position. 

## 301 remove invalid parentheses

Remove the minimum number of invalid parentheses in order to make the input string valid. Return all possible results.

**Note:** The input string may contain letters other than the parentheses `(` and `)`.

**Example 1:**

```
Input: "()())()"
Output: ["()()()", "(())()"]
```

**Example 2:**

```
Input: "(a)())()"
Output: ["(a)()()", "(a())()"]
```

**Example 3:**

```
Input: ")("
Output: [""]
```

Solution:

```python
class Solution:
    def removeInvalidParentheses(self, s: str) -> List[str]:
        ans = []
        self.remove(s, ans, 0, 0, ('(', ')'))
        return ans
    def remove(self, s, ans, last_i, last_j, par):
        count = 0
        for i in range(last_i, len(s)):
            if s[i] == par[0]: count += 1
            if s[i] == par[1]: count -= 1
            if count >= 0: continue
            for j in range(last_j, i + 1):
                if (s[j] == par[1]) and ((j == last_j) or (j > last_j and  s[j - 1] != par[1])):
                    self.remove(s[:j] + s[j + 1:], ans, i, j, par)
            return
        reverse = s[::-1]
        if par[0] == '(':
            self.remove(reverse, ans, 0, 0, (')', '('))
        else:
            ans.append(reverse)
            
  
```



##  1249. Minimum Remove to Make Valid Parentheses

Given a string s of `'('` , `')'` and lowercase English characters. 

Your task is to remove the minimum number of parentheses ( `'('` or `')'`, in any positions ) so that the resulting *parentheses string* is valid and return **any** valid string.

Formally, a *parentheses string* is valid if and only if:

- It is the empty string, contains only lowercase characters, or
- It can be written as `AB` (`A` concatenated with `B`), where `A` and `B` are valid strings, or
- It can be written as `(A)`, where `A` is a valid string.

 

**Example 1:**

```
Input: s = "lee(t(c)o)de)"
Output: "lee(t(c)o)de"
Explanation: "lee(t(co)de)" , "lee(t(c)ode)" would also be accepted.
```

**Example 2:**

```
Input: s = "a)b(c)d"
Output: "ab(c)d"
```

**Example 3:**

```
Input: s = "))(("
Output: ""
Explanation: An empty string is also valid.
```

**Example 4:**

```
Input: s = "(a(b(c)d)"
Output: "a(b(c)d)"
```

 

**Constraints:**

- `1 <= s.length <= 10^5`
- `s[i]` is one of `'('` , `')'` and lowercase English letters`.`

```python
###########################the counter method##################################
class Solution:
    def minRemoveToMakeValid(self, s: str) -> str:
        res = []
        last_i, last_j = 0, 0
        self.helper(s, res, last_i, last_j, ('(', ')'))
        return res[0] if res else ''
    def helper(self, s, res, last_i, last_j, parse):
        count = 0
        for i in range(last_i, len(s)):
            if s[i] == parse[0]: count += 1
            if s[i] == parse[1]: count -= 1
            if count >= 0: continue
            for j in range(last_j, len(s)):
                if (s[j] == parse[1]) and (j == last_j or (j > last_j and s[j - 1] != parse[1])):
                    if self.helper(s[:j] + s[j + 1:], res, i, j, parse): return True
        reverse = s[::-1]
        if parse[0] == '(':
            if self.helper(reverse, res, 0, 0, (')', '(')):
                return True
        else:
            res.append(reverse)
            return True
        return False
    
    
    #####################the stack method######################################
  class Solution:
    def minRemoveToMakeValid(self, s: str) -> str:
        stack, cur = [], ''
        for ch in s:
            if ch == '(':
                stack.append(cur)
                cur = ''
            elif ch == ')':
                if stack: 
                    cur = stack.pop() + '(' + cur + ')'
            else:
                cur += ch
        while stack:
            cur = stack.pop() + cur
        return cur
    #I think this method explains perfectly the stack usage in the parentheses problems. Whenever meet with the open parentheses, we should push the previous string into the stack. whenever meet with the close parentheses, we should pop out the string that has been pushed into the stack.
    
 
```

