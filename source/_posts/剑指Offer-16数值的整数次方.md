title: 剑指Offer 16数值的整数次方
author: andyhui
tags:
- algorithms
categories:
- 剑指Offer

date: 2019-03-13 22:50:00
---

## [数值的整数次方](https://www.nowcoder.com/practice/1a834e5e3e1a4b7ba251417554e07c00?tpId=13&tqId=11165&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)

### 题目描述

> 给定一个 double 类型的浮点数 base 和 int 类型的整数 exponent，求 base 的 exponent 次方。

<!-- more -->

### 思路

> 快速幂，
>
> n=0：1
>
> n>0：$$x^{n}=x^{n/2}*x^{n/2}*x^{n\%2}$$ 
>
> n<0：$$\frac{1}{x^{n}}$$
>
> 递归 / 非递归

### 代码

```python
# -*- coding:utf-8 -*-
class Solution:
    def Power(self, base, exponent):
        # 递归版
        if exponent == 0:
            return 1
        if exponent == 1:
            return base
        is_neg = False
        if exponent < 0:
            exponent = - exponent
            is_neg = True
        res = self.Power(base * base, exponent // 2)
        if exponent % 2 :
            res *= base
        return 1/res if is_neg else res
    def Power1(self, base, exponent):
        # 非递归
        if exponent == 0:
            return 1
        is_neg = False
        if exponent < 0:
            exponent = - exponent
            is_neg = True       
        res = 1
        while exponent:
            if exponent & 1:
                res *= base
            exponent >>= 1
            base *= base
        return 1/res if is_neg else res

s = Solution()
print(s.Power1(2,-3))
```

