title: 剑指Offer 7重建二叉树
author: andyhui
date: 2019-03-10 23:43:46
tags:
  - algorithms
categories:
  - 剑指Offer

---

## [重建二叉树](https://www.nowcoder.com/practice/8a19cbe657394eeaac2f6ea9b0f6fcf6?tpId=13&tqId=11157&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)

### 题目描述

> 输入某二叉树的前序遍历和中序遍历的结果，请重建出该二叉树。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。例如输入前序遍历序列{1,2,4,7,3,5,6,8}和中序遍历序列{4,7,2,1,5,3,8,6}，则重建二叉树并返回。



<!-- more -->

### 思路

> 前序遍历取出根节点，可根据此将中序遍历结果分为左右子树两部分，递归实现此过程即可



## 代码

```python
# -*- coding:utf-8 -*-
class TreeNode:
    def __init__(self, x):
        self.val = x
        self.left = None
        self.right = None
class Solution:
    # 返回构造的TreeNode根节点
    def reConstructBinaryTree(self, pre, tin):
        if not pre or not tin:
            return None
        root = TreeNode(pre.pop(0))
        index = tin.index(root.val)
        root.left = self.reConstructBinaryTree(pre, tin[:index])
        root.right = self.reConstructBinaryTree(pre, tin[index + 1:])
        return root
```



## 拓展

[LeetCode 1008. 先序遍历构造二叉搜索树](https://leetcode.com/problems/construct-binary-search-tree-from-preorder-traversal/)



> 返回与给定先序遍历 `preorder` 相匹配的二叉搜索树（binary **search** tree）的根结点。
>
> *(回想一下，二叉搜索树是二叉树的一种，其每个节点都满足以下规则，对于 node.left 的任何后代，值总 < node.val，而 node.right 的任何后代，值总 > node.val。此外，先序遍历首先显示节点的值，然后遍历 node.left，接着遍历 node.right。）*

```
输入：[8,5,1,7,10,12]
输出：[8,5,10,1,7,null,12]
```

![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2019/03/08/1266.png)



### 代码

```python
class Solution:
    def bstFromPreorder(self, preorder) -> TreeNode:
        if not preorder:
            return None
        root = TreeNode(preorder[0])
        itr = 1
        while itr < len(preorder) and preorder[itr] < preorder[0]:
            itr += 1
        root.left = self.bstFromPreorder(preorder[1: itr])
        root.right = self.bstFromPreorder(preorder[itr:])
        return root
```

