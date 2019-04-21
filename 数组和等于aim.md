### 题目描述

给你一个数组arr， 和一个整数aim。 如果可以任意选择arr中的数字， 能不能累加得到aim， 返回true或者false

### 思路解析

##### 递归

与字符的组合类似，一个位置的可以选择，也可以不选择
```python

class Solution:
    def isExitsHelper(self, array, cur, sum, aim):
        if cur == len(array):
            return sum == aim

        return self.isExitsHelper(array, cur + 1, sum, aim) or \
               self.isExitsHelper(array, cur + 1, sum + array[cur], aim)


print(Solution().isExitsHelper([2, 7, 10], 0, 0, 13))

```

[3,2,5]

第一个位置选择3，第二个位置选择5，到第三个位置时累加和为5 $f(3,5)$

第一二个位置都不选择，第三个位置选择5，到第三个位置累加和也为5 $f(3,5)$



##### 递归改动态规划

```python

class Solution1:
    def isExits(self, array, aim):
        length = len(array)
        dp = [[False for i in range(aim + 1)] for j in range(length + 1)]
        dp[length][aim] = True

        for i in range(length - 1, -1, -1):
            for j in range(aim, -1, -1):
                dp[i][j] = dp[i + 1][j]
                if j + array[i] <= aim:
                    dp[i][j] = dp[i][j] or dp[i + 1][j + array[i]]
        return dp[0][0]


```

```python

class Solution:
    def isExits(self, array, aim):
        length = len(array)
        dp = [[False for i in range(aim + 1)] for j in range(length + 1)]
        dp[0][0] = True

        for i in range(1, len(array) + 1):
            for j in range(aim + 1):
                dp[i][j] = dp[i - 1][j]
                if j - array[i - 1] >= 0:
                    dp[i][j] |= dp[i - 1][j - array[i - 1]]
        return dp[-1][-1]


```
