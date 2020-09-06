1. > ![img](https://oss.1point3acres.cn/forum/202008/24/002848ug4ykuyz1vqgq1uq.png)

2. >  第一题是两个list，A和B，长度分别为n和m，对于B中所有数，返回A中小于等于该数的数字个数，返回长度为m的列表。m和n的上限都是10^5，一下子想到的是O((m+n)logn)的算法，所以上限是10^6。

3. > 684. Redundant Connection
   >
   > In this problem, a tree is an **undirected** graph that is connected and has no cycles.
   >
   > The given input is a graph that started as a tree with N nodes (with distinct values 1, 2, ..., N), with one additional edge added. The added edge has two different vertices chosen from 1 to N, and was not an edge that already existed.
   >
   > The resulting graph is given as a 2D-array of `edges`. Each element of `edges` is a pair `[u, v]` with `u < v`, that represents an **undirected** edge connecting nodes `u` and `v`.
   >
   > Return an edge that can be removed so that the resulting graph is a tree of N nodes. If there are multiple answers, return the answer that occurs last in the given 2D-array. The answer edge `[u, v]` should be in the same format, with `u < v`.
   >
   > **Example 1:**
   >
   > ```
   > Input: [[1,2], [1,3], [2,3]]
   > Output: [2,3]
   > Explanation: The given undirected graph will be like this:
   > 1
   > / \
   > 2 - 3
   > ```
   >
   > 
   >
   > **Example 2:**
   >
   > ```
   > Input: [[1,2], [2,3], [3,4], [1,4], [1,5]]
   > Output: [1,4]
   > Explanation: The given undirected graph will be like this:
   > 5 - 1 - 2
   >  |   |
   >  4 - 3
   > ```
   >
   > 
   >
   > **Note:**
   >
   > The size of the input 2D-array will be between 3 and 1000.
   >
   > Every integer represented in the 2D-array will be between 1 and N, where N is the size of the input array.
   >
   > 
   >
   > 
   >
   > **Update (2017-09-26):**
   > We have overhauled the problem description + test cases and specified clearly the graph is an ***undirected\*** graph. For the ***direc**
   >
   > 
   >
   > **ted\*** graph follow up please see **[Redundant Connection II](https://leetcode.com/problems/redundant-connection-ii/description/)**). We apologize for any inconvenience caused.

4. > ![img](https://oss.1point3acres.cn/forum/202008/24/002956a4axdtdwidiuxjca.jpeg)

5. > 第一道题是validate word。给你一个正确单词的list和一个input的list.要求你判断每一个input word 是不是valid，return bool[]。valid的criteria 是 长度得一样，不一样的字母<=1。tricky的地方在于有runtime 限制。一个8个testcases，

6. > 实现一个加密、解密的类。明文的每一个字符映射到密文的两个字符。不同明文可能映射到同一密文。 比如: 'z' --> 'aw', 'r' -->'wo', 't' --> 'wo'.
   > 实现加密功能: 'zr' --> 'awwo'
   > 实现解密功能，揭秘需要输出所有的可能性: 'wowo' --> ['rr', 'rt', 'tt', 'tr']
   >
   > 进阶问题：
   > \1. 写测试
   > \2. 算复杂度
   > \3. 若解密时提供一个英语字典，要求输出的词必须是英语词的话，如何优化

7. > ![image-20200904012003671](C:\Users\gcy\AppData\Roaming\Typora\typora-user-images\image-20200904012003671.png)

8. > ![image-20200904013158835](C:\Users\gcy\AppData\Roaming\Typora\typora-user-images\image-20200904013158835.png)

9. > - 一个买本子题，大概描述如下：
   >
   > ​    比如有三家店第一家：一梱本子20元，30个本子一捆，第二家：一梱本子25元，40个本子一梱，第三家：一梱本子3元，2本一梱，问给100元最多能买多少本。

10. > \697. Degree of an Array
    >
    > Given a non-empty array of non-negative integers `nums`, the **degree** of this array is defined as the maximum frequency of any one of its elements.
    >
    > Your task is to find the smallest possible length of a (contiguous) subarray of `nums`, that has the same degree as `nums`.

11. > \264. Ugly Number II
    >
    > Medium
    >
    > 2062127Add to ListShare
    >
    > Write a program to find the `n`-th ugly number.
    >
    > Ugly numbers are **positive numbers** whose prime factors only include `2, 3, 5`. 

12. > 313. Super Ugly Number
    >
    > Write a program to find the `nth` super ugly number.
    >
    > Super ugly numbers are positive numbers whose all prime factors are in the given prime list `primes` of size `k`.

13. > https://oss.1point3acres.cn/forum/201910/07/031723r695ifoa95tx0u0t.png



