---
title: Github-SSHKey相关
date: 2021-08-24 17:16:23
categories:
  - Note
tags:
  - Note
---

# Github SSH Key

`Github` 上如果想用 `git@github.com` 的ssh方式，需要在GitHub的Setting里配上客户机的SSHKey的。

# SSH Key - Win10 生成方式

## 检查已有SSH Key

```bash
cat ~/.ssh/id_rsa.pub 
```

得到的形如

> ssh-rsa ................

就是SSH Key了，将其添加到GitHub-Setting-SSH&GPGKey里即可。

## 生成SSH Key

```bash
ssh-keygen -t rsa -C "some comment"
```

一路回车即可，生成完成后查看：

```bash
cat ~\.ssh\id_rsa.pub
```