title: CI 持续集成
author: andyhui
tags:
  - CI
  - devops
categories:
  - devops
permalink: Continuous_Integration
date: 2019-03-04 19:45:00
---
之前废弃Hexo时，觉得hexo比较麻烦，每次都要执行
```
hexo clean
hexo deploy
hexo generate
```
，才能推到线上，虽然有人把命令简化了一下
```
hexo clean && hexo d -g
```
一行就能搞定，但我还是觉得命令太长，每次复制太麻烦，于是发现了持续集成工具[`travis-ci`](https://www.travis-ci.org/)，因此顺便了解一下持续集成。
<!-- more -->

## 什么是持续集成？
> 持续集成（英语：Continuous integration，缩写 CI）是一种软件工程流程，是将所有软件工程师对于软件的工作副本持续集成到共享主线（mainline）的一种举措。每次集成都通过自动化的构建（包括编译，发布，自动化测试）来验证，从而尽早地发现集成错误。

也就是说，上面的命令可以通过持续集成工具自动化执行，这样每次我们对博客做出的修改，只需提交`commit`后，推送到`github`，持续集成工具自动在线构建博客并部署到`GitHub Pages`,简化了博客发布流程。

下面是几张图片描述下持续集成、持续交付和持续部署
### 持续集成
![持续集成流程](http://githubblog.andyhui.top/image/Continuous_Integration%E6%8C%81%E7%BB%AD%E9%9B%86%E6%88%90%20Continuous%20Integration.jpeg)
> 持续集成强调开发人员提交了新代码之后，立刻进行构建、（单元）测试。根据测试结果，我们可以确定新代码和原有代码能否正确地集成在一起。

### 持续交付
![持续交付流程](http://githubblog.andyhui.top/image/Continuous_Integration%E6%8C%81%E7%BB%AD%E4%BA%A4%E4%BB%98%20Continuous%20Delivery.jpeg)
> 持续交付在持续集成的基础上，将集成后的代码部署到更贴近真实运行环境的「类生产环境」（production-like environments）中。比如，我们完成单元测试后，可以把代码部署到连接数据库的 Staging 环境中更多的测试。如果代码没有问题，可以继续手动部署到生产环境中。

### 持续部署
![持续部署流程](http://githubblog.andyhui.top/image/Continuous_Integration%E6%8C%81%E7%BB%AD%E9%83%A8%E7%BD%B2%20Continuous%20Deployment.jpeg)
> 持续部署则是在持续交付的基础上，把部署到生产环境的过程自动化。


## 关于Hexo的一次持续集成实践

> 详细流程见[这里](https://easyhexo.com/1-Hexo-install-and-config/1-5-continuous-integration.html#%E6%B3%A8%E5%86%8C-travis-ci-%E8%B4%A6%E5%8F%B7%EF%BC%8C%E7%BB%91%E5%AE%9A-github-%E8%B4%A6%E6%88%B7)

写下对于这个的一些补充
1. 对于博客源文件，最好添加**`.gitignore`**,忽略掉`node_modules`，依赖文件太大，影响上传速度。
2. 仓库必须Public,私有仓库既不能通过name.github.io访问，也不能完成CI
3. 对于主题文件，如果有`.git`文件可能会造成git add失败，如果主题不打算更新可删掉主题文件内的`.git`文件夹

## 下一步计划
- 学习主流CI工具，如[`Jenkins`](https://juejin.im/entry/565fbc6c60b215d646403d33)
- [基于Docker的CI平台实践](https://juejin.im/entry/5a2a269df265da43052e8878)


## 参考文档
[EasyHexo 持续集成Continuous Integration
](https://easyhexo.com/1-Hexo-install-and-config/1-5-continuous-integration.html#%E4%BB%80%E4%B9%88%E6%98%AF%E6%8C%81%E7%BB%AD%E9%9B%86%E6%88%90%EF%BC%9F)

[致产品经理： 持续集成、持续交付、持续部署和DevOps
](https://blog.csdn.net/jjm1437/article/details/71601450)
[如何理解持续集成、持续交付、持续部署？
](https://www.zhihu.com/question/23444990)
## 推荐阅读
[微服务化的基石——持续集成
](https://zhuanlan.zhihu.com/p/33206437)