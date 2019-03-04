---
title: oj信息爬取
date: 2017-08-29 15:04:51
tags:
- 爬虫
- oj
- python
- requests
categories:
- python
permalink: ojrankscan
---


> 假期俱乐部举办了编程训练营，每个人负责管理15人的营，每天作业会在oj的一个总榜上
> 关于各营营长每天统计很麻烦，所以我写了一个简单的爬虫来节省一部分工作
> ** 代码改变世界，使人更高效的完成自己的工作**

---

### 基本环境

> Windows 10 + python 3.6.2 + requests 库

<!-- more -->
### requests 库安装

```python
pip install requests
```

![requests安装](http://githubblog.andyhui.top/requests%E5%AE%89%E8%A3%85.png)

### 分析需求

> 首先需要统计的 Contest 有3周的作业 加 最后的结课测试

![ojContestList](http://githubblog.andyhui.top/ojContestList.png)

> 每个榜单结构都是一致的，我只需要统计自己营里的**昵称**和**总解决数目**就好

![oj榜单](http://githubblog.andyhui.top/oj%E6%A6%9C%E5%8D%95.png)

> url 是 "http://oj.acmclub.cn/contestrank.php?cid=" + contestID

> 右键查看网页源代码 两个a标签中刚好有我们的数据，用简单正则表达式匹配下就好

![oj榜单源码](http://githubblog.andyhui.top/oj%E6%A6%9C%E5%8D%95%E6%BA%90%E7%A0%81.png)

### 构造request爬取网页

> 首先拿出一个榜单来处理，由于不需要登陆就可以查看榜单所以我直接抓取榜单html页面

``` python
import requests
def getHTMLText(url):
    try:
        r = requests.get(url, timeout=30)
        r.raise_for_status()
        r.encoding = r.apparent_encoding
        return r.text
    except:
        return ""

def main():
    for no in range(1166,1169):
        url = 'http://oj.acmclub.cn/contestrank.php?cid='+str(no)
        html = getHTMLText(url)
        print(html)
main()
```

**这算一个基本框架了，通过request得到网页源码，中间_r.raise_for_status()_是错误检查，后面是根据推断的编码类型设置字符编码**
运行结果如下
![result1](http://githubblog.andyhui.top/result1.png)
### 对html源码处理

> 首先看网页源码

![oj榜单源码](http://githubblog.andyhui.top/oj%E6%A6%9C%E5%8D%95%E6%BA%90%E7%A0%81.png)

> 这里可以用正则表达式库 **re** 来进行字符匹配，如果昵称符合规范**xx营xx号_Nickname_name**就很容易处理了，匹配两个a标签之间的内容
``` python
rege = r'<a href=.*?>(0{0,1}'+str(num)+'营.*?)</a><td><a href=.*?>([0-9]{1,2})</a>'
```

> 对html的处理函数也就是很容易写了

``` python
import requests
import re
def getHTMLText(url):
    #省略
def fillscoreList(slist, html, num):
    rege = r'<a href=.*?>(0{0,1}'+str(num)+'营.*?)</a><td><a href=.*?>([0-9]{1,2})</a>'
    score = re.findall(rege,html)
    for x in score:
        slist.append(x)

def main():
    num = int(input("请输入营号:"))
    for no in range(1166,1169):
        sinfo = []
        url = 'http://oj.acmclub.cn/contestrank.php?cid='+str(no)
        html = getHTMLText(url)
        fillscoreList(sinfo, html, num)
        for (name,solve) in  sinfo:
            print(name,solve)
main()
```
这样得到的sinfo就是包含元组(name,solve)的列表，程序到这阶段基本算是完工了，但是输出的样式也并不尽人意，比如_没有对齐_，看起来很乱，而且三周内容_挤在一块_不好区分，接下来就对这个程序进行优化
![result2](http://githubblog.andyhui.top/result2.png)

### 格式化输出

> 我们想要达到的效果是三周内容清晰可辨，并且有良好的对齐，下面就来是实现下
> python 的 字符串 有**format函数**，通过这个来达到我们想要的效果
> 对于(xx营xx号_Nickname_name,solve_num)这样一个元组，通过格式限定符来达到**指定字段宽度**和**居中对齐**

``` python
tplt = "{0:<20}\t\t{1:^3}"
print(tplt.format("xx营xx号_Nickname_name","   解决总题目数",chr(12288)))
```

{}来指明位置 相当于c的printf中的%，{0} 指的是第0个元素，填充常跟对齐一起使用^、<、>分别是居中、左对齐、右对齐，后面带宽度
:号后面带填充的字符，只能是一个字符，不指定的话默认是用空格填充，后面我们指定了中文空格

> 所以现在的程序就是这样

``` python
import requests
import re
def getHTMLText(url):
    #省略
def fillscoreList(slist, html, num):
    #省略
def printscoreList(slist, num):
    tplt = "{0:20}\t\t{1:^3}"
    print(tplt.format("xx营xx号_Nickname_name","     解决题目数",chr(12288)))
    for i in range(num):
        u=slist[i]
        print(tplt.format(u[0],u[1],chr(12288)))
def main():
    num = int(input("请输入营号:"))
    for no in range(1166,1169):
        sinfo = []
        url = 'http://oj.acmclub.cn/contestrank.php?cid='+str(no)
        html = getHTMLText(url)
        fillscoreList(sinfo, html, num)
        print("*"*15,"第%d周%d营成绩"%(int(no-1165),num),"*"*18)
        printscoreList(sinfo, len(sinfo))
main()
```

运行结果如下
![result3](http://githubblog.andyhui.top/result3.png)
### 未完待续