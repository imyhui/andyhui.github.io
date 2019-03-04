---
title: Git及GitHub使用
date: 2017-09-20 19:35:10
tags:
- git
- github
categories:
- git
permalink: gitfirstuse
---
## Git

### 什么是 Git
> **Git is a free and open source distributed version control system designed to handle everything from small to very large projects with speed and efficiency.** 项目加上Git后能能更好的追踪代码修改，进行版本回溯等操作。当今时代，多人协作开发是公司合作的基本模式，在多人协作的开发过程中Git变得必不可少，接下来大致介绍下Git的基本命令以及GitHub的基本使用。

<!-- more -->
### 为什么用Git

#### 提高开发效率!

> git不仅仅是一个代码版本管理工具，也是一个文档管理工具，在git上很容易维护一个文档

#### git可以提高开发效率，主要表现在:

+ 合并对提交过程的保留
+ 修正提交
+ 廉价好用的本地分支
+ 更强大智能的合并能力
+ 完整配套的开发过程设施(wiki issue 功能大赞！)
+ 查看日志

转自 [Koudle](http://www.jianshu.com/p/834678d9c213)

### Git的下载及安装
首先肯定是[下载Git](https://git-scm.com/downloads)
( `提醒:资源下载较慢，推荐挂vpn`)

![git下载](http://githubblog.andyhui.top/image/gitfirstuse/git%E4%B8%8B%E8%BD%BD.png)


然后安装界面如下(`windows平台`)

![安装1](http://githubblog.andyhui.top/image/gitfirstuse/%E5%AE%89%E8%A3%851.png)

这里注意这两个都是添加到右键菜单栏，很好用

![安装2](http://githubblog.andyhui.top/image/gitfirstuse/%E5%AE%89%E8%A3%852.png)

一路next下去就好

安装完后 打开终端输入
`注意 $ 是表示从命令行输入，不用自己输入，只需要输入后面内容即可，后面一致`
```
$ git --version
```
如果显示
```
git version 2.14.1.windows.1
```
表示安装成功了
### Git基本设置

在桌面上右键`Git Bash here` 启动git bush命令行界面
当然也可以从终端打开

![启动](http://githubblog.andyhui.top/image/gitfirstuse/%E5%90%AF%E5%8A%A8.png)

首先我们对 `Git` 进行全局用户名和邮箱进行设置，请参照下面格式，`Your Name` 替换为你的名字， `you@example.com` 替换为你的邮箱
这里个人信息设置的作用，是为你在代码提交时自动署名标记，方便查看提交日志时区分作者。
```
$ git config --global user.name "Your Name"
$ git config --global user.email you@example.com
```
接下来进行Git推送分支相关设置
这个是命令 `Git`当我们执行 `git push` 没有指定分支时，自动使用当前分支，而不是报错。[更多关于push.default](http://blog.csdn.net/daijingxin/article/details/51326715)

```
$ git config --global push.default simple
```

### Git基本操作
对于有经验的开发者来说，在他每次新建完开发项目的时候，首先要做的第一件事就是将自己的项目纳入到 `Git` 代码版本管理中，完成这个操作一般需要以下这几个步骤：

#### 对Git进行初始化

我们要在对应的项目文件夹(文件夹内)对git初始化，
windows下可直接在对应文件夹下右键 `Git Bush here`
也可以用命令行找到对应文件夹，
这里我们用命令行示范下
```
$ cd D:/andyhui/DataStructure
$ git init
```
`D:/andyhui/DataStructure`这个是我自己的文件目录，替换成你项目的文件目录即可,如果没有就自己创建一个，在里面随意放一个文件即可，比如 一个说明`what.md`或 代码文件 `HelloWorld.cpp`

#### 将项目所有文件纳入到Git暂存区中

这些文件并未真正提交到Git上
这里`-A` 是all的意思，我们也可以指定一个文件
```
$ git add -A
```
 这里的所有文件指的是没在 `.gitignore` 中被忽略的文件。在Git工作区的根目录下创建一个特殊的`.gitignore`文件，然后把要忽略的文件名填进去，Git就会来选择忽略掉一些我们不想纳入到 Git 版本管理中的文件（如缓存文件）。[git忽略文件设置](http://bdxnote.blog.163.com/blog/static/844423520124153051409/)以及[了解更多.gitignore](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/0013758404317281e54b6f5375640abbb11e67be4cd49e0000)。

#### 检查 Git 状态

这条命令将会向你输出存放在 `Git` 暂存区的文件，这意味着这些文件还未真正提交到 Git 中。
```
$ git status
```

#### 保留改动并提交

这行命令会将暂存区的文件都提交到 `Git`，-m 选项后面带的参数表示本次提交的简单描述。
```
$ git commit -m "Initial commit"
$ git log
commit e7419d269d65021fa056b731e09f8bdeaac00d9d (HEAD -> master, origin/master)
Author: andyhui <andyhui686666@gmail.com>
Date:   Thu Sep 21 09:24:53 2017 +0800

    Initial commit
```

#### 查看历史提交记录：
```
$ git log
```

从输出信息中可以很清晰的看到每次提交的作者、日期、描述等信息。按 `q`可退出查看。

![gitlog](http://githubblog.andyhui.top/image/gitfirstuse/gitlog.png)

git 基本提交操作到这就结束了，如果你想学习更多关于 `Git` 相关的知识，可以查阅[《Pro Git》](https://git-scm.com/book/zh/v2)一书进行学习。


## GitHub

### 什么是 GitHub
`GitHub` 是目前全球最大的代码托管平台，许多非常著名的项目如 Linux、Swift、Laravel 等都托管在 `GitHub` 上。开发者们利用 `GitHub` 来进行团队协作开发，查阅或收藏别人开源项目的优秀代码，针对某个 `Bug` 进行技术讨论等。

### GitHub基本操作
#### 注册 GitHub 账号
如果你还没有 `GitHub` 账号的话，请先 [注册](https://github.com/join)。
#### 为 `GitHub` 账号设置 `SSH Key`

生成 `SSH Key`，开始之前，我们先使用以下命令来检查主机上是否已经生成过 `SSH Key`：
```
$ ls -al ~/.ssh
```
如果存在 `id_rsa` 和 `id_rsa.pub`的话，请跳过以下生成 `SSH` 的步骤继续阅读剩下内容。
否则使用以下方法来生成 `SSH Key`，请将 `your_email@example.com` 替换为你的邮箱：
```
$ ssh-keygen -t rsa -C "your_email@youremail.com"
```
命令行会提示让你指定秘钥的名称，按回车键将 `SSH Key`保存到默认文件名即可：
```
Enter a file in which to save the key (/Users/you/.ssh/id_rsa): [Press enter]
```
接下来会询问你为 `SSH Key` 设置密码，每次提交需要用到，可以设置，也可以按回车键即可，默认为空密码：
```
Enter passphrase (empty for no passphrase): [Type a passphrase]
Enter same passphrase again: [Type passphrase again]
```
可以都选择默认，也就是直接敲击几个 `Enter` 键即可。这时候我们再检查一下：
```
$ ls -al ~/.ssh
```
可以看到以下两个文件：
```
id_rsa —— SSH 秘钥的 私钥 (Private Key)
id_rsa.pub —— SSH 秘钥的 公钥 (Public Key)
```

接下来将 `SSH Key` 添加到 `ssh-agent` 中：
```
$ eval `ssh-agent -s`
$ ssh-add ~/.ssh/id_rsa
```
打印出公钥 `id_rsa.pub` 文件里的内容，并把输出的内容复制到剪贴板里：
```
$ cat ~/.ssh/id_rsa.pub
```
![copyssh](http://githubblog.andyhui.top/image/gitfirstuse/copyssh.png)

最后我们需要将公钥添加到 GitHub 账号，先打开 [Github SSH](https://github.com/settings/keys) 令牌管理页面，然后把你刚刚复制的令牌按照下图示例添加：

![sshkey添加](http://githubblog.andyhui.top/image/gitfirstuse/sshkey%E6%B7%BB%E5%8A%A0.png)

测试`ssh key`是否成功
```
$ ssh -T git@github.com
```
输入完密码后，如果出现You’ve successfully authenticated, but GitHub does not provide shell access 。这就表示已成功连上github。

#### 提交代码到 Github

在配置完 GitHub 账号之后，我们便可以开始在上面存放项目代码了。首先 [新建一个 GitHub 仓库](https://github.com/new)，取名为 `你项目的名字`，填上 `Description` 项目描述，`Initialize this repository with a README` 这一项是询问你是否需要生成一个默认的介绍。

![新仓库](http://githubblog.andyhui.top/image/gitfirstuse/%E6%96%B0%E4%BB%93%E5%BA%93.png)


创建完成之后，使用以下命令将代码上传到 `GitHub` 上（将 `your_username` 替换为你自己的 `GitHub` 用户名，`your_projectname` 是你的项目名字，就是刚刚创建仓库的名字）：
```
$ git remote add origin git@github.com:your_username/your_projectname.git
$ git push -u origin master
```
至此，项目已成功托管到 GitHub 上。
(如果Git 提示`fatal: remote origin already exists`[请看这里](http://blog.csdn.net/top_code/article/details/50381432))
(如果提示`error: src refspec master does not match any`[请看这里](http://www.jianshu.com/p/8d26730386f3)))

![代码提交成功](http://githubblog.andyhui.top/image/gitfirstuse/%E4%BB%A3%E7%A0%81%E6%8F%90%E4%BA%A4%E6%88%90%E5%8A%9F.png)


#### 小总结
后面我们如果对本地代码进行了改动，只需运行这 3 条命令即可将代码推送到安全可靠的 `GitHub` 上：

`注意：以下命令作为知识重温，不需要执行`

1、保存到暂存区,-A也可以换成指定文件：
```
$ git add -A
```
2、输入描述信息并提交到本地的 Git：
```
$ git commit -m "Say something"
```
3、将代码推送到 GitHub：
```
$ git push
```
## Git 进阶操作
### 误删恢复
通过上面 `Git` 的基本讲解，你可能还无法真正体会到 `Git` 的强大。在平时开发中，我们有时候可能会因为手误或其它原因将某些重要文件删除。如果之前有将此文件纳入到 `Git` 中，这时便可以利用 `Git` 来对误删文件进行恢复。请看下面演示。

我们先假装不小心删除 `what.md` 文件：
```
$ rm what.md
$ ll
```
使用 ll 打印出文件目录列表时，能看到 `what.md` 文件已被成功移除。

查看 Git 状态：

```
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.

Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        deleted:    what.md

no changes added to commit (use "git add" and/or "git commit -a")
```
能看到有相关提示显示 `what.md` 文件已被删除，这时你可以选择将删除的文件进行恢复或提交。

下面我们使用 `Git` 进行恢复被删除文件：
```
$ git checkout -f
$ ll
```
这时能看到 `what.md` 文件已成功恢复。`git checkout -f` 的作用是将在暂存区的更改文件进行强制撤销。

### 从GitHub克隆项目到本地

首先到我们要克隆的到GitHub的某个仓库，比如[neuq-acmclubTD](https://github.com/imyhui/neuq-acmclubTD),右边有个绿色的`Clone or download`，点开后有`Clone with HTTPS `，当然你也可以直接下载

![克隆连接](http://githubblog.andyhui.top/image/gitfirstuse/%E5%85%8B%E9%9A%86%E8%BF%9E%E6%8E%A5.png)

然后回到要存放的目录下，右键`Git Bash here`使用命令
```
$ git clone https://github.com/imyhui/neuq-acmclubTD.git
```
如果本地的版本不是最新的，可以使用以下命令，`origin`是本地仓库
```
$ git fetch origin
```
把更新的内容合并到本地分支，可以使用以下命令
```
$ git merge origin/master
```

如果你不想手动去合并，那么你可以使用以下命令,这个命令可以拉去最新版本并自动合并
```
git pull <本地仓库> master
```
注意:记得如果不是单独另需创建的branch，每次对本地仓库操作的时候都要使用 `git pull`命令，更新远程仓库到本地中，防止冲突。这点和SVN的update类似
### GitHub的分支管理
几乎所有的版本控制系统都以某种形式支持分支。**使用分支意味着你可以把你的工作从开发主线上分离开来，以免影响开发主线。** 有人把 `Git` 的分支模型称为它的`‘必杀技特性’`，也正因为这一特性，使得 `Git`从众多版本控制系统中脱颖而出。[了解分支](https://git-scm.com/book/zh/v2/Git-%E5%88%86%E6%94%AF-%E5%88%86%E6%94%AF%E7%AE%80%E4%BB%8B)

#### 分支创建合并删除
1. 首先选中主分支
`git checkout master` 代表将当前分支切换到 `master` 分支上，`master` 分支是我们初始化 `Git` 时默认创建的主分支，其它分支都是基于主分支衍生出来的。

```
$ git checkout master
```
2. 创建一个本地分支： `git branch <新分支名字>`,比如
```
$ git branch new_branch
```
3. 切换到新建立的分支： `git checkout <新分支名>`
```
$ git checkout new_branch
Switched to branch 'new_branch'
```
2、3 步骤其实可以用一条命令搞定 ` git checkout -b new_branch `，我习惯用这条,区别[参考这里](https://my.oschina.net/u/587974/blog/74341)

你可以将新建的 `new_branch` 理解为是对 `master` 分支的克隆，在上面做的所有修改都不会影响到 `master` 分支。本节后面会将 `new_branch` 分支合并到 `master` 分支上，合并成功之后，在 `new_branch` 分支上做的所有改动都会并入到 `master` 分支。另外，你也可以选择对一个分支进行删除操作，当一个分支被删除之后，在该分支之上的所有改动也都将被销毁，删除分支的操作不会影响到 `master` 分支。这便是 `Git` 工作流的强大之处。

4. 合并分支操作是`git merge <分支名称>`将分支的操作合并到主分支上,注意，多人协作中当两条分支对同一个文件的同一个文本块进行了不同的修改，并试图合并时，Git不能自动合并的，称之为`冲突(conflict)`。解决冲突需要人工处理。，解决冲突看[这里](http://www.cnblogs.com/mengdd/p/3585038.html)，合并分支示例：
```
$ git checkout master
$ git merge new_branch
```
5. 从本地删除一个分支： `git branch -d <分支名称>`, 删除分支示例：
```
$ git branch -d new_branch
```
6. 将本地分支同步到GitHub上面： `git push <本地仓库名> <新分支名>`

7. 为你的分支加入一个新的远程端： `git remote add <远程端名字> <地址>`

8. 查看当前仓库有几个分支: `git branch`

## 总结
经过以上配置后，之后新建仓库操作如下进行即可
1. 进入对应目录 `cd 你的仓库目录`
2. 初始化git仓库 `git init`
3. 添加提交的文件

|文件数|指令|
|--|--|
|一个文件 | `git add 文件名`|
|全部文件 | `git add -A`|
4. 提交修改提示 `git commit -m`
5. 查看提交状态 `git status`
6. 查看最近日志 `git log`
7. 版本回退操作

|回退次数|指令|
|-- |:------------- |
|回退一个 |`git reset -hard HEAD^`|
|回退两个 | `git reset -hard HEAD^^`|
|回退多个 | `git reset -hard HEAD~100`|

8. (第一次连接)远程仓库提交 `git remote add origin 你复制的地址`
9. (第二次以后)远程仓库提交 `git push`

## 参考
[github官方教程](https://try.github.io/)

[Laravel 教程 - Web 开发实战入门 ( Laravel 5.5 ) ](https://fsdhub.com/books/laravel-essential-training-5.5)

[Linux下Git和GitHub使用方法总结](http://www.linuxidc.com/Linux/2014-03/97821.htm)

[Git 初学者](http://hanfu.space/%E6%8A%80%E6%9C%AF/2015/08/26/git-tutorial/)

[mac os x使用Git简易入门教程 ](http://blog.csdn.net/nellson/article/details/51526273)

[《Pro Git》](https://git-scm.com/book/zh/v2)

推荐看下[`github官方教程`](https://try.github.io/)和[`《Pro Git》`](https://git-scm.com/book/zh/v2)。

## 结束语
`Git`与`GitHub`基础教程到这就结束了，熬夜写了两晚上······半夜写头脑难免混乱可能有疏漏的地方，欢迎给我留言，有部分是参考以上链接的部分内容，侵删。希望大家看完这个教程能有一定收获，毕竟这是以后的合作途径。好了我要去补实验报告了>.<。