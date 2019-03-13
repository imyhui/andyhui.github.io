title: 剑指Offer 19正则表达式匹配
author: andyhui
date: 2019-03-13 22:51:15
tags:
- algorithms
categories:
- 剑指Offer

---

## [正则表达式匹配](<https://www.nowcoder.com/practice/45327ae22b7b413ea21df13ee7d6429c?tpId=13&tqId=11205&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking>)

### 题目描述

> 请实现一个函数用来匹配包括'.'和'*'的正则表达式。模式中的字符'.'表示任意一个字符，而'*'表示它前面的字符可以出现任意次（包含0次）。 在本题中，匹配是指字符串的所有字符匹配整个模式。例如，字符串"aaa"与模式"a.a"和"ab*ac*a"匹配，但是与"aa.a"和"ab*a"均不匹配

<!-- more -->



### 思路 

> 待补



###  代码

```python
# -*- coding:utf-8 -*-
class Solution:
    # s, pattern都是字符串
    def match2(self, s, pattern):
        # write code here
        m, n = len(s), len(pattern)
        dp = [[False]*(n + 1) for _ in range(m + 1)]
        dp[0][0] = True
        for i in range(1, n + 1):
            if pattern[i - 1] == '*':
                dp[0][i] = dp[0][i - 2]
        for i in range(1, m + 1):
            for j in range(1, n + 1):
                if s[i - 1] == pattern[j - 1] or pattern[j - 1] == '.':
                    dp[i][j] = dp[i - 1][j - 1]
                elif pattern[j - 1] == '*':
                    if pattern[j - 2] == s[i - 1] or pattern[j - 2] == '.':
                        dp[i][j] |= dp[i][j - 1]
                        dp[i][j] |= dp[i - 1][j]
                        dp[i][j] |= dp[i][j - 2]
                    else:
                        dp[i][j] = dp[i][j - 2]
        return dp[m][n]
    def match(self, s, pattern):
        # write code here
        if (len(s) == 0 and len(pattern) == 0):
            return True
        if (len(s) > 0 and len(pattern) == 0):
            return False
        if (len(pattern) > 1 and pattern[1] == '*'):
            if (len(s) > 0 and (s[0] == pattern[0] or pattern[0] == '.')):
                return (self.match(s, pattern[2:]) or self.match(s[1:], pattern[2:]) or self.match(s[1:], pattern))
            else:
                return self.match(s, pattern[2:])
        if (len(s) > 0 and (pattern[0] == '.' or pattern[0] == s[0])):
            return self.match(s[1:], pattern[1:])
        return False
s = Solution()
print(s.match('aaa','a*a'))
```

