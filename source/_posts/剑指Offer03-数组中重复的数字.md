title: 剑指Offer03 数组中重复的数字
author: andyhui
tags:
  - algorithms
categories:
  - 剑指Offer
date: 2019-03-07 23:55:00
---
## [数组中重复的数字](https://www.nowcoder.com/practice/623a5ac0ea5b4e5f95552655361ae0a8?tpId=0&tqId=0&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)

### 题目描述

> 在一个长度为n的数组里的所有数字都在0到n-1的范围内。 数组中某些数字是重复的，但不知道有几个数字是重复的。也不知道每个数字重复几次。请找出数组中任意一个重复的数字。 例如，如果输入长度为7的数组{2,3,1,0,2,5,3}，那么对应的输出是第一个重复的数字2。

<!-- more -->

### 思路

> 排序后两两比较需要$$O(nlogn)$$时间，哈希表存储可以$$O(1)$$ 查找，整体时间复杂度$$O(n)$$ ，同时空间复杂度也为$$O(n)$$，若允许修改原数组，可以用原数组数的值和下标的对应关系来解，扫描到下标为i的数字m，若该m与i不同，则找数组中m位置对应的数字，若该数字与m相同，则重复，若不同则交换两数字位置，这种解法时间复杂度$$O(n)$$，空间复杂度$$O(1)$$。

### 代码

```python
# -*- coding:utf-8 -*-
class Solution:
    # 这里要特别注意~找到任意重复的一个值并赋值到duplication[0]
    # 函数返回True/False
    def duplicate(self, numbers, duplication):
        # 允许修改数组 不允许额外空间
        n = len(numbers)
        if n == 0:
            return False
        for i in range(n):
            if numbers[i] < 0 or numbers[i] > n - 1:
                return False
        for i in range(n):
            if numbers[i] != i:
                if numbers[numbers[i]] == numbers[i]:
                    duplication[0] = numbers[i]
                    return True
                tmp = numbers[numbers[i]]
                numbers[numbers[i]] = numbers[i]
                numbers[i] = tmp
        return False

s = Solution()
x = [0]
print(s.duplicate([2,3,1,0,2,5,3],x))
print(x)
```

## 数组中重复数字2

### 题目描述

> 在一个长度为n+1的数组里的所有数字都在1~n的范围内，所以数组中至少有一个数字是重复的。请找出数组中任意一个重复的数字，但**不能修改输入的数组**。例如，如果输入长度为8的数组{2, 3, 5, 4, 3, 2, 6, 7}，那么对应的输出是重复的数字2或者3。

### 思路

> 不修改数组，可以开一个大小为n的数组，与上题思路一致，若不适用额外空间，可采取二分统计数字，若一个s到e的范围内数字超过e-s + 1，则该范围内可能有重复的数字，采取二分查找即可。n个数字`count_range`被调用$$O(log(n))$$次，每次需$$O(n)$$时间，所以时间复杂度为$$O(nlogn)$$，空间复杂度为$$O(1)$$

### 注意

> 本题数组限制为**长度为n+1的数组里的所有数字都在1~n的范围内**，若没有这个条件可能解答会不成立

### 代码

```python
 # -*- coding:utf-8 -*-
class Solution:
    # 函数返回True/False
     def duplicate(self, numbers, duplication):
            # 不允许修改数组
            n = len(numbers)
            if n == 0:
                return -1
            start, end = 1, n - 1
            while start <= end:
                mid =  start + ((end-start)>>1)
                print(start,mid,end)
                count = self.count_range(numbers, start, mid)
                if start == end:
                    if count > 1:
                        return start
                    else:
                        break
                if count > mid - start + 1:
                    end = mid
                else:
                    start = mid + 1
            return -1

        def count_range(self, numbers, start, end):
            if len(numbers) == 0:
                return 0
            count = 0
            for i in numbers:
                if i >= start and i <= end:
                    count += 1
            return count
```

