---
title: 15分钟用Docker部署PHP开发环境
date: 2017-12-09 02:41:17
tags:
- 后端
- laradock
- docker
- laravel
categories:
- 后端学习
permalink: LaradockInstall
---
## 为什么使用laradock
>  搭建环境对于上手框架的新人是一件头疼的事,多人协作开发,线上线下环境的一致也是一个很麻烦的问题,而`laradock`的使用,完美解决了这个问题,相比`homestead`与`vagrant`,`laradock`更加轻量级,只需要数秒就可以完成启动,既可以作为开发环境也可以作为生产环境,支持`PHP`、`MySQL`、 `Nginx`等一系列软件,且安装较为简便。

支持的软件有
```
> Database Engines: MySQL - MariaDB - Percona - MongoDB - Neo4j - RethinkDB - MSSQL - PostgreSQL - Postgres-PostGIS.
> Database Management: PhpMyAdmin - Adminer - PgAdmin
> Cache Engines: Redis - Memcached - Aerospike
> PHP Servers: NGINX - Apache2 - Caddy
> PHP Compilers: PHP FPM - HHVM
> Message Queueing: Beanstalkd - RabbitMQ - PHP Worker
> Queueing Management: Beanstalkd Console - RabbitMQ Console
> Random Tools: HAProxy - Certbot - Blackfire - Selenium - Jenkins - ElasticSearch - Kibana - Grafana - Mailhog - MailDev - Minio - Varnish - Swoole - Laravel Echo…
```

<!-- more -->

## 依赖
+ [Git](https://git-scm.com/downloads)
+ [Docker](https://www.docker.com/community-edition) `>= 1.12`

    > 可以通过`docker -v`查看自己的docker版本，一定要保证大于`1.12`，否则会遇到各种问题，推荐安装`17.0`以上，之前`1.13.1`mysql启动不了。

    附上我的docker版本
    ```
    > docker version
    Client:
    Version:      17.05.0-ce
    API version:  1.29
    Go version:   go1.7.5
    Git commit:   89658be
    Built:        Thu May  4 22:09:06 2017
    OS/Arch:      linux/amd64

    Server:
    Version:      17.05.0-ce
    API version:  1.29 (minimum version 1.12)
    Go version:   go1.7.5
    Git commit:   89658be
    Built:        Thu May  4 22:09:06 2017
    OS/Arch:      linux/amd64
    Experimental: false
    ```

## 安装
### 选择安装位置
+ 首先选择一个文件目录，克隆`laradock`，理论上文件目录可以任选，推荐这样的文件结构
    ```
    + laradock
    + project-1
    + project-2
    ```
+ 这样每个项目文件夹和`laradock`是平行的关系，多个项目共用一个`laradock`,也可以每个项目单独装一个laradock，推荐第一种方式
### 安装laradock
```
git clone https://github.com/laradock/laradock.git
```
### 安装Laravel
1. 进入`laradock`文件夹
    ```
    cd ~/Code/laradock
    ```
    > `Code`是我存放项目的文件夹
2. 修改配置文件
    ```
    cp env-example .env
    ```
    > 编辑`.env`文件可以修改需要安装软件，以及相关软件的设置，如php版本、mysql数据库名称等
3. 构建环境
    ```
    docker-compose up -d nginx mysql
    ```
    > `workspace` 和 `php-fpm`会自动启动，这个不用添加在后面，后面可选择的软件有
    ```
    nginx, hhvm, php-fpm, mysql, redis, postgres, mariadb, neo4j, mongo, apache2, caddy, memcached, beanstalkd, beanstalkd-console, workspace
    ```
    > 第一次构建需下载安装镜像，会花较长时间，之后启动仅需数秒。

    > 可以用`docker-compose ps`查看容器运行状态
4. 进入`workspace`容器
+ 执行`Artisan`, `Composer`, `PHPUnit`等命令需要进入`workspace`容器内才能执行
    ```
    docker-compose exec --user=laradock workspace bash
    ```
    > 以`laradock`身份进入容器，也可以执行`docker-compose exec workspace bash`
5. `Laravel`相关配置
> 从一个项目的创建来说明相关配置
+ 创建一个`Laravel`项目
    ```
    composer create-project laravel/laravel testapp --prefer-dist "5.5.*"
    ```
+ 修改刚创建应用的`.env`文件，主要要修改以下几个地方
    ```
    ...
    DB_HOST=mysql
    DB_DATABASE=default
    DB_USERNAME=default
    DB_PASSWORD=secret

    REDIS_HOST=redis
    ...
    ```
+ 修改`nginx`相关配置
    + 进入`nginx`站点配置文件夹`/laradock/nginx/sites`
        > 默认给出了`app.conf.example`, `laravel.conf.example` 等文件夹，克隆一份修改对应名字
        ```
        cp app.conf.example testapp.conf
        ```
    + 编辑配置文件
        > 修改下主页对应位置，`/var/www/`对应的是laradock的同级目录，应用要对应到`public`文件夹
        ```
        ...
        server_name testapp.dev;
        root /var/www/testapp/public;
        ...
        ```
    + 在hosts里添加解析,文件路径为`/etc/hosts`
        ```
        127.0.0.1 testapp.dev
        ```
    + 重启nginx
        ```
        > docker-compose restart nginx
        Restarting laradock_nginx_1 ... done
        ```
    + 打开浏览器输入` testapp.dev`看到如下界面即安装成功

        ![安装成功](http://githubblog.andyhui.top/%E6%88%90%E5%8A%9F.png)
## 参考
[官方文档](http://laradock.io/)
[项目地址](https://github.com/laradock/laradock)