title: Python 练习册，每天一个小程序
author: andyhui
tags:

  - python
categories:
  - python
date: 2019-03-06 23:23:00

---

> Talk is cheap. Show me the code.--Linus Torvalds



最近发现一个有趣的项目——[**show-me-the-code**](https://github.com/Yixiaohan/show-me-the-code)，25道`python`, 题目，涵盖各个方面，同时兼具挑战性，考察编码能力和资料搜集学习能力。

<!-- more -->

## 写在前面

完整代码在[这里](https://github.com/imyhui/show-me-the-code/)更新，为了不污染全局Python环境，使用了[`pipenv`](https://github.com/pypa/pipenv)管理依赖，要运行代码只需只需

```shell
pipenv install
pipenv shell
python xxx.py
```



## 0000 

> 将你的 QQ 头像（或者微博头像）右上角加上红色的数字，类似于微信未读信息数量那种提示效果。 



查资料得知，`Python3`图像处理库为Pillow，于是看到了*廖雪峰*老师的[教程](https://www.liaoxuefeng.com/wiki/0014316089557264a6b348958f449949df42a6d3a2e542c000/0014320027235877860c87af5544f25a8deeb55141d60c5000)，简单看了下几个例子及[Pillow文档](https://pillow.readthedocs.io/en/stable/index.html)，代码便很容易写了

```python
from PIL import Image, ImageDraw, ImageFont
def main():
    # 打开图片，获取图片宽度和高度
    im = Image.open('avatar.jpg')
    w, h = im.size
    
    # 创建Draw对象
    draw = ImageDraw.Draw(im)
    # 导入字体创建Font对象
    font = ImageFont.truetype('Arial.ttf', 36)
    # 图片左上角为(0, 0), 绘制文本为'99+', 字体为导入的字体，填充颜色为红色
    draw.text((w*0.90, h*0.01),'99+', font=font,fill='#FF0000')

    im.show()

if __name__ == "__main__":
    main()
```



运行效果

![add_num_pic](http://githubblog.andyhui.top/add_num.png)



未完待续。。。