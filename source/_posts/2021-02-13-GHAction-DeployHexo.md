---
title: Deploy Hexo to github page via github action
categories:
  - Note
tags:
  - Note
date: 2021-02-13 00:00:00
---

Travis 最近因为要收费了，从org变com了。

看到原来是github action的原生支持，把原来的CI从Travis搬到了Github action上。

过程中

* Hexo版本和nodejs版本的兼容问题，导致编译失败
* 原先Travis用的是source branch push到master上的方式，但是github action上这种方式不知道可行还有路上各种ssh、Hexo本身的deploy问题，修改了很多小地方。跑了很多次action。
* 造成history特别丑
* 最后发现Hexo官方给出的解决方式还是比较简单的。
* 结合本地Hexo genereate的方式，修改了脚本如下

# Github Action script 

``` yaml

# This is a basic workflow to help you get started with Actions
name: Hexo CI

# Controls when the action will run. 
on:
  # Triggers the workflow on push events but only for the master branch
  push:
    branches: [ master ]
  schedule:
      - cron: '0 22 * * *' # 6am UTC+8 Everyday
  workflow_dispatch:
  
jobs:
  pages:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Use Node.js 12.x
        uses: actions/setup-node@v1
        with:
          node-version: '12.x'
      - name: Fetch
        run: git fetch --all
      - name: Checkout
        run: git checkout origin/master
      - name: Hexo install
        run: npm install hexo -g
      - name: Install Dependencies
        run: npm install
      - name: Clear Hexo
        run: hexo clean
      - name: Build
        run: hexo g
      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public
          publish_branch: gh-page  # deploying branch

```