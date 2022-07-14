---
title: Deepin 安装oh-my-zsh
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

切换`oh-my-zsh`的主题，我一般喜欢用自带的`agnoster`

打开zsh配置

```bash
vi ~/.zshrc
```

修改主题

```bash
ZSH_THEME="agnoster"
```

由于需要显示Git分支等符号来自于symbol字体，需要额外安装。

这里用Firacode安装，简单快捷。

在Debian/Ubuntu下安装较为简单：

```bash
sudo apt install fonts-firacode
```

来自[官方](https://github.com/tonsky/FiraCode/wiki/Linux-instructions#manual-installation)

之后可以顺带修改VSCode的字体，重启`zsh`即可。

## 可能遇到的问题

安装后我遇到了`nvm`，`npm`的`Command Not Found`的错误。

尝试重新安装`nvm`就好了
