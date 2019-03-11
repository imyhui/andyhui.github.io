title: 剑指Offer 12矩阵中的路径
author: andyhui
date: 2019-03-11 22:03:23
tags:
  - algorithms
categories:
  - 剑指Offer
---

## [矩阵中的路径](https://www.nowcoder.com/practice/c61c6999eecb4b8f88a98f66b273a3cc?tpId=13&tqId=11218&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)

### 题目描述

> 请设计一个函数，用来判断在一个矩阵中是否存在一条包含某字符串所有字符的路径。路径可以从矩阵中的任意一个格子开始，每一步可以在矩阵中向左，向右，向上，向下移动一个格子。如果一条路径经过了矩阵中的某一个格子，则之后不能再次进入这个格子。 例如 a b c e s f c s a d e e 这样的3 X 4 矩阵中包含一条字符串"bcced"的路径，但是矩阵中不包含"abcb"路径，因为字符串的第一个字符b占据了矩阵中的第一行第二个格子之后，路径不能再次进入该格子。

<!-- more -->



### 思路

> 首先应将字符串转为二维数组，然后对于每个字母作为起始字母`DFS`扫描一遍即可，注意搜索的写法。



### 代码

```python
# -*- coding:utf-8 -*-
class Solution:
    def hasPath(self, matrix, rows, cols, path):
        # write code here
        if rows == 0 or cols == 0:
            return False
        self.build_matrix(matrix, rows, cols)
        for i in range(rows):
            for j in range(cols):
                if self.find(i, j, 0, rows, cols, path):
                    return True
        return False

    def find(self, i, j, l, rows, cols, path):
        if l == len(path):
            return True
        if i < 0 or i >= rows or j < 0 or j >= cols or self.flag[i][j] or self.new_matrix[i][j] != path[l]:
            return False
        self.flag[i][j] = 1
        for n in [[-1, 0], [1, 0], [0, -1], [0, 1]]:
            if self.find(i+n[0], j+n[1], l+1, rows, cols, path):
                return True
        self.flag[i][j] = 0
        return False

    def build_matrix(self, matrix, rows, cols):
        self.flag = []
        self.new_matrix = []
        for i in range(rows):
            self.flag.append([0]*cols)
            self.new_matrix.append(list(matrix[i*cols:cols+i*cols]))


# s = Solution()
# print(s.hasPath("ABCESFCSADEE", 3, 4, "ABCCED"))

```

