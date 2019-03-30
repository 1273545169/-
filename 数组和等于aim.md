### 题目描述

给你一个数组arr， 和一个整数aim。 如果可以任意选择arr中的数字， 能不能累加得到aim， 返回true或者false

### 思路解析

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
