## 060.Permutation Sequence

### 题目描述

给出集合 `[1,2,3,…,*n*]`，其所有元素共有 *n*! 种排列。

按大小顺序列出所有排列情况，并一一标记，当 *n* = 3 时, 所有排列如下：

1. `"123"`
2. `"132"`
3. `"213"`
4. `"231"`
5. `"312"`
6. `"321"`

给定 *n* 和 *k*，返回第 *k* 个排列。

**说明：**

- 给定 *n* 的范围是 [1, 9]。
- 给定 *k* 的范围是[1,  *n*!]。

**示例 1:**

```
输入: n = 3, k = 3
输出: "213"
```

**示例 2:**

```
输入: n = 4, k = 9
输出: "2314"
```

### 解答

​	这道题的话其实网上有很多种解法，可以使用全排列，但是时间上可能会难以AC，所以得想其它的方法，仔细观察一下题目，从一个[1，n]的区间内挑数字（也就是代码中的nums)加入答案（直到全挑光)，按顺序去挑数字就行了。首先确定第一个数字，假如第一个数字已经确定，则会有(n-1)!种情况，那么我们可以用k//(n-1)!来确定第一个数字，假如结果为0，那就是1，以此类推。然后用k%(n-1)!来循环剩下的数字。

```python
class Solution:
    def getPermutation(self, n, k):
        """
        :type n: int
        :type k: int
        :rtype: str
        """
        # 从0到9的阶乘
        fac = [1, 1, 2, 6, 24, 120, 720, 5040, 40320, 362880]
        
        i = n - 1
        num = list(range(1,n+1))
        res = ''
        while i>=0:
            # a 确定了第一位数字
            a,b = k // fac[i], k % fac[i]
            if b == 0:
                a-=1
            if a>=0:
                res+=str(num[a])
                del num[a]
                i-=1
            k = b
            if b == 0:
                for i in reversed(num):
                    res+=str(i)
                break
        return res
```



- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$ 

