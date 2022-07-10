---
title: deepin-oh-my-zsh
categories:
  - Note
tags:
  - Note
date: 2022-07-11 00:25:42
---

# Oh-my-zsh

不说了，就是很帅的terminal，由zsh而来

# 安装

先安装zsh

```bash
# 切换到root
su

# 先安装zsh
apt-get -y install zsh

# 看看已经安装的shell
cat /etc/shells

# 切换到zsh
chsh -s /bin/zsh

# reboot，不重启可能看不到zsh
reboot

# 查看当前Shell
echo $SHELL
```

再安装oh-my-zsh

[官方Repo](https://github.com/ohmyzsh/ohmyzsh)

README提供了3个下载方式

| Method    | Command                                                                                           |
| :-------- | :------------------------------------------------------------------------------------------------ |
| **curl**  | `sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"` |
| **wget**  | `sh -c "$(wget -O- https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"`   |
| **fetch** | `sh -c "$(fetch -o - https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"` |