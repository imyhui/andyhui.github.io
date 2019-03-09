title: 剑指Offer15 二进制中1的个数
author: andyhui
tags:
  - algorithms
categories:
  - 剑指Offer
date: 2019-03-09 23:46:00

---

## [二进制中1的个数](https://www.nowcoder.com/practice/8ee967e43c2c4ec193b040ea7fbb10b8?tpId=13&tqId=11164&rp=1&ru=%2Fta%2Fcoding-interviews&qru=%2Fta%2Fcoding-interviews%2Fquestion-ranking&tPage=1)

### 题目描述

> 输入一个整数，输出该数二进制表示中1的个数。其中负数用补码表示。

<!-- more-->



### 思路1

> 32位整数取出每一位，与1做`&`，求和即可

### 代码1

```python
class Solution:
    def NumberOf1(self, n):
        # move n
        count = 0
        for _ in range(32):
            count += n & 1
            n = n >> 1
        return count
```



### 思路2

> 对比思路一，不对n做移位，而是用一个变量，实现一个过滤器的作用来取每一位



### 代码2

```python
    def NumberOf1(self, n):
        # move flag
        count = 0
        flag = 1
        for _ in range(32):
            if n & flag:
                count += 1
            flag <<=1
        return count 
```



### 思路3

> 对于一个数n, `n&(n-1)`结果即消掉末尾1的结果，如8 = $$(1100)_{2}$$，8-1 = 7 = $$(1011)_{2}$$
>
> 1100 & 1011 = 1000
>
> 即消去了末尾的1
>
> **注意**
>
> 由于Python 的动态类型，导致数字不会像`C++`那样溢出`int`范围变为0，因此要先做一步处理，若为负数则加上 2*32次方，转为补码，再进行统计

### 代码3

```python
    def NumberOf12(self, n):
        # not run if n<0
        if n<0:
            n += 2**32
        count = 0
        while n != 0:
            count += 1
            n = n & (n-1)
        return count
```

