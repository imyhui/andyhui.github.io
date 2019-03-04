---
layout: post
#文章属性 	post或page
#如果你修改了layout，在scaffolds文件夹里一定要有名字对应的模版文件，否则会采用默认模版。
title: Markdown 基本语法
#文章的标题
date: 2017-08-25 08:19:08
#创建日期
updated: 2017-08-27 17:00:00
#修改时间
comments: true
#是否开启评论 默认:true
tags:
- Markdown
- Hexo
#标签
categories:
- Markdown
#分类
permalink: Markdown_基本语法
#url中的名字 默认:文件名
---
近几天刚刚搭建了博客，用的是Hexo+Next主题，托管在github和codding上，写博文是需要Markdown，所以先学习下Markdown的基本语法，也算是为博客增加一篇博文吧。

---

Markdown基础用法与规则：

### 标题
使用"#"加空格在首行来创建标题
如:
&emsp;&emsp; # 一级标题
&emsp;&emsp; \#\# 二级标题
&emsp;&emsp; \#\#\# 三级标题
![](http://githubblog.andyhui.top/markdown%E6%A0%87%E9%A2%98.png)

---

<!-- more -->
### 加粗功能
使用一组星号"\*\*"或一组下划线"\_\_"来加粗一段文字，用转义符"\\"来打出"\*"
如:
&emsp;&emsp; 这是**加粗的文字**
&emsp;&emsp; 这也是__加粗的文字__

---

### 引用
使用">"在段首来引用一段文字，要在引用前后加入空白行声明开始和结束引用
如:

> 这是一段引用
> 这是一段引用


---

### 无序列表
使用"-"、"*"或"+"加空格来创建无序列表
如:

- 这是一个无序列表
+ 这是一个无序列表
* 这是一个无序列表


---

### 有序列表
使用数字圆点加空格如"1."、"2."来创建有序列表
如:

1. 这是一个有序列表
2. 这是一个有序列表
3. 这是一个有序列表


---

以上来源[**锤子便签**](https:\\cloud.smartisan.com\apps\note\md.html)

---

### 贴代码
用一对重音符"\`\`\` code \`\`\`"引起来，可以在\`\`\`后表明语言
如:

``` cpp
#include<iostream>
using namespace std;
int main()
{
    cout<<"Hello World!"<<endl;
    return 0;
}
```

也可以用4个空格(Tab)缩进再贴上代码实现相同的效果

    #include<iostream>
    using namespace std;
    int main()
    {
        cout<<"Hello World!"<<endl;
        return 0;
    }

---

### 强调标记
用两个重音符"\`强调内容\`"
这是一个`强调标记`

---

### 未完待续