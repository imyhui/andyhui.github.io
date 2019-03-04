---
title: 糗事百科爬虫
date: 2017-09-02 13:57:19
tags:
- 爬虫
- linux
- python
- requests
- BeautifulSoup
categories:
- python
permalink: qsbkspider
---


> 一周前买了阿里云服务器，简单部署了一个JudgeService，感觉闲着也是闲着，决定在上面部署一个爬虫，打算每隔一段时间爬取糗事百科前几页的文本段子并以邮件的形式发送到qq邮箱中。

---

### 基本环境
> requests + smtplib + bs4
> 都可以用pip install 来安装


<!-- more -->
### 分析需求
> 基本目的是爬取糗事百科文本部分前几页内容保存
> 后续操作有通过邮件发送到邮箱，之后是挂载到云服务器上每隔一段时间自动爬取并发送邮件

#### 分析url
> 我们这次只爬取文字内容，所以这次爬取的url是 __'https://www.qiushibaike.com/text/'__
> 点开第二页会发现 url变为 __'https://www.qiushibaike.com/text/page/2/'__
> 很清晰的知道 第i页的url也就是 url = __'https://www.qiushibaike.com/text/page/%s/'%str(i)__
> 我们要爬前多少页也就是一个for循环的事

#### 分析网页源码
> 首先来看下网页的基本内容
![]()

> 我们要做的是提取这一个个文本，然后保存下来

> 根据网页源码很容易看出 内容是在 class="content"的div标签下，可以直接套用正则表达式，我们这使用BeautifulSoup库的find_all函数就可以搞定
![]()

### 构造request请求

> 首先就是通过requests库得到网页源码 _html = requests.get(url)_

> 这里我们加一个小的异常处理，也就是如果爬取不到我们将错误信息写入一个文件，文件名为**Http error on time.ctime()** 这里的**[time.ctime()](http://www.runoob.com/python/att-time-ctime.html)**是包含在time里面的一个函数，返回当前时间。

> 然后用BeautifulSoup做成一锅汤**soup = BeautifulSoup(html.text, 'lxml')**
这里我们用lxml HTML 解析器，因为它的优势是速度快，文档容错能力强，(更多关于BeautifulSoup)[http://cuiqingcai.com/1319.html]

之后我们用_find_all_找到每一个笑话，之后呢，把换行标签替换掉，然后加到data\_list 中去

``` python
import requests
from bs4 import BeautifulSoup
import time
import lxml
def getcontent(url):
    try:
        html = requests.get(url)
    except:
        with open("log.log","a") as file:
            file.write("Http error on " + time.ctime())
        time.sleep(60)
        return None
    soup = BeautifulSoup(html.text, 'lxml')
    data_list = []
    for cont in soup.find_all("div", {"class":"content"}):
        raw_data = cont.get_text()
        data = raw_data.replace("\n","")
        data_list.append(data)
    return data_list

def main():
    data_list = []
    for i in range(1,2):
        url = 'https://www.qiushibaike.com/text/page/%s/'%str(i)
        temp_data = getcontent(url)
        data_list.extend(temp_data)
    for i in data_list:
        print(i)
        print('\n\n')
main()
```
### 未完待续