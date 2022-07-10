---
title: Travis+Hexo自动推送博客
date: 2019-02-06 22:42:02
categories:
- Note
tags:
- Note
- BlogBuilding
---
# 简 介

## Hexo是什么

    Hexo 是一个快速、简洁且高效的博客框架。Hexo 使用 Markdown（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。
    本Blog也是基于Hexo搭建。

## Travis是什么

    Travis CI 是目前新兴的开源持续集成构建项目，它与jenkins，GO的很明显的特别在于采用yaml格式，同时他是在在线的服务，不像jenkins需要你本地打架服务器，简洁清新独树一帜。目前大多数的github项目都已经移入到Travis CI的构建队列中，据说Travis CI每天运行超过4000次完整构建。对于做开源项目或者github的使用者，如果你的项目还没有加入Travis CI构建队列，那么我真的想对你说out了。  

# 使用原因

* 单纯的使用Hexo提供的hexo depoly，将编译后的静态页面上传到GitHubPage还不够。
* 如果发生数据丢失、硬盘损坏等，项目文件丢失了。单纯的从编译好的静态页面文件并不能还原Hexo的项目文件，最重要的是项目中的Markdown文件的丢失。
* 不用再调主题

# 步骤

## 注册Travis

Travis支持GitHub账号直接登录，直接用GitHub账号授权即可。

注册后如图

![注册图](https://i.loli.net/2019/02/06/5c5afb068ebdf.jpg)

左侧选项卡点击加号，激活你的GitHubPage项目。

## GitHub 准备

### 项目准备

GitHubPage对应的项目中，需要新建一个分支，名字任意，用来保存Hexo项目。

### 授权准备

* 进入GitHub的账号设置

![账号设置](https://i.loli.net/2019/02/06/5c5afc7c753b2.jpg)

* 选择Developer settings

![Developer settings](https://i.loli.net/2019/02/07/5c5be272b6dc2.jpg)

* 选择Personal Acess Token

![Personal Acess Token](https://i.loli.net/2019/02/06/5c5afc7c5b4e7.jpg)

* 点击右侧的Generate new Token

![Generate new Token](https://i.loli.net/2019/02/06/5c5afdb0111cc.jpg)

* 勾选如下权限

![权限设置](https://i.loli.net/2019/02/06/5c5afe1f2dcc3.jpg)

* 生成Token并复制

* 回到Travis里，在激活的项目右侧点击Setting，下方添加变量'GH_TOKEN'，值为刚刚生成的Token

* 在Hexo项目中，新建'.travis.yml'文件，填入：

    ```yml
    language: node_js
    node_js: stable

    # S: Build Lifecycle
    install:
    - npm install


    #before_script:
    # - npm install -g gulp

    script:
    - hexo g

    after_script:
    - cd ./public
    - git init
    - git config user.name "@Github用户名@"
    - git config user.email "@Github邮箱@"
    - git add .
    - git commit -m "Update docs"
    - git push --force --quiet "https://${GH_TOKEN}@${GH_REF}" master:master
    # E: Build LifeCycle

    branches:
    only:
        - @创建的分支@
    env:
    global:
    - GH_REF: @项目地址@
    ```

## 使用方法

* 使用方法即普通的Git add->commit->push 一套Combo，Travis检测到变动会通过trvais.yml编译并提交到master里，Token已经给了Travis写入权限了。

## 最后结果

最后你会在GitHubPage的仓库里看到master分支和创建的hexo项目分支，其中hexo项目分支是自己手动git push上去的，而master分支即展示在GitHubPage上的静态页面是Travis编译完成并push的。

## 参考文章

[](https://www.2cto.com/kf/201605/505702.html)
