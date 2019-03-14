title: 剑指Offer39 数组中出现次数超过一半的数字
author: andyhui
tags:

- algorithms
categories:
- 剑指Offer
date: 2019-03-14 23:22:00

---

## [数组中出现次数超过一半的数字](https://www.nowcoder.com/practice/e8a1b01a2df14cb2b228b30ee6a92163?tpId=13&tqId=11181&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)

### 题目描述

> 数组中有一个数字出现的次数超过数组长度的一半，请找出这个数字。例如输入一个长度为9的数组{1,2,3,2,2,2,5,4,2}。由于数字2在数组中出现了5次，超过数组长度的一半，因此输出2。如果不存在则输出0。

<!-- more -->

### 思路与代码

> 最基本思路可以用`哈希表`或者`dict`，数组中的数作为`key`, 值做为`value`，时间复杂度与空间复杂度均为$$O(n)$$

```python
# -*- coding:utf-8 -*-
class Solution:
    def MoreThanHalfNum_Solution(self, numbers):
        dic = {}
        for i in numbers:
            dic[i] = dic.get(i,0) + 1
        major = max(dic,key=dic.get)
        return major if numbers.count(major) > len(numbers)//2 else 0
```

```python
import collections
class Solution:
    def MoreThanHalfNum_Solution(self, numbers):
        counts = collections.Counter(numbers)
        major = max(counts.keys(), key=counts.get) 
        return major if numbers.count(major) > len(numbers)//2 else 0
```



> 稍作思考可得，数组排序，若存在最多的数字，其位置必然在中间，此算法时间复杂度$$O(nlog(n))$$，空间复杂度$$O(1)$$

 ```python
    def MoreThanHalfNum_Solution(self, numbers):
        major = sorted(numbers)[len(numbers)/2]
        return major if numbers.count(major) > len(numbers)//2 else 0
 ```
>位运算解决，对于32二进制数的每一位，所有数字若该位置1的数目大于一半，则取1，否则取0，时间复杂度$$O(n)$$，空间复杂度$$O(1)​$$

```python
    def MoreThanHalfNum_Solution(self, numbers):
        major = 0
        for i in range(31,-1,-1):
            pos = 0
            for n in numbers:
                pos += (n>>i) & 1
            pos = 1 if pos > len(numbers) // 2 else 0
            major |= pos << i
        return major if numbers.count(major) > len(numbers)//2 else 0
```



>多数投票问题(Boyer-Moore Majority Vote)
>
>比较直观的解释：在数组中找到两个不相同的元素并删除它们，不断重复此过程，直到数组中元素都相同，那么剩下的元素就是主要元素。
>
>这里不用删除元素，用一个计数器cnt统计一个元素出现次数，若遍历到元素与cnt对应元素相同，cnt += 1， 否则 cnt -=1 ，若cnt为0，则下一个元素为计数器统计元素，cnt重新置1。
>
>最后要加一个判断，数组是否存在主要元素。

```python
    def MoreThanHalfNum_Solution2(self, numbers):
        major, cnt= 0, 0
        for num in numbers:
            if cnt == 0:
                major = num
            cnt += (1 if num == major else -1)
        return major if numbers.count(major) > len(numbers)//2 else 0
```

## 拓展

### [LeetCode 229. 求众数 II](<https://leetcode-cn.com/problems/majority-element-ii/>)

> 给定一个大小为 *n* 的数组，找出其中所有出现超过 `⌊ n/3 ⌋` 次的元素。
>
> **说明:** 要求算法的时间复杂度为 O(n)，空间复杂度为 O(1)。
>
```shell
 输入: [1,1,1,3,3,2,2,2]
 输出: [1,2]
```



### 思路及代码

> 对于这样的数字，可能存在个数有0，1，2，这里依然可以使用`多数投票算法`，只是多一计数器。
>
> 时间复杂度$$O(n)$$，空间复杂度$$O(1)$$

​```python
class Solution:
    def majorityElement(self, nums):
        m1, cnt1, m2, cnt2 = 0, 0, 0, 0
        for num in nums:
            if num == m1:
                cnt1 += 1
            elif num == m2:
                cnt2 += 1
            elif cnt1 == 0:
                m1, cnt1 = num, 1
            elif cnt2 == 0:
                m2, cnt2 = num, 1
            else:
                cnt1, cnt2 = cnt1 - 1, cnt2 - 1
        major = [n for n in set([m1, m2]) if nums.count(n) > len(nums)/3]
        return major

s = Solution()
print(s.majorityElement([1, 2, 2, 3, 2, 1, 1, 3]))

 ```

## 参考文档

[cycNote](https://cyc2018.github.io/CS-Notes/#/notes/%E5%89%91%E6%8C%87%20Offer%20%E9%A2%98%E8%A7%A3%20-%2030~39?id=_39-%e6%95%b0%e7%bb%84%e4%b8%ad%e5%87%ba%e7%8e%b0%e6%ac%a1%e6%95%b0%e8%b6%85%e8%bf%87%e4%b8%80%e5%8d%8a%e7%9a%84%e6%95%b0%e5%ad%97)

[Boyer-Moore Majority Vote](<https://www.jianshu.com/p/dfd676b71ef0>)