# Union-Find template

> ```python
> class union_find:
>     def __init__(self, n):
>         self.count = n
>         self.parent = [i for i in range(n)]
>         self.size = [1 for _ in range(n)]
>     def union(self, p, q):
>         root_p = self.find(p)
>         root_q = self.find(q)
>         if root_p == root_q: return
>         if self.size[root_p] > self.size[root_q]: # to keep balanced tree
>             self.parent[root_q] = root_p
>             self.size[root_p] += self.size[root_q]
>         else:
>             self.parent[root_p] = root_q
>             self.size[root_q] += self.size[root_p]
>         self.count -= 1
>     def find(self, x):# path compression
>         while self.parent[x] != x:
>             self.parent[x] = self.parent[self.parent[x]]
>             x = self.parent[x]
>         return x
>     def connected(self, p, q):
>         return self.find(p) == self.find(q)
> ```
>
> 

