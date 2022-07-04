---
title: Deepin安装Docker
categories:
  - Note
tags:
  - Note
date: 2022-07-04 15:05:33
---

安装部分来自[cnblogs](https://www.cnblogs.com/langkyeSir/p/14032801.html)，稍作修改，做查询备份用。

## Docker简介

Docker 是一个开源的应用容器引擎，让开发者可以打包他们的应用以及依赖包到一个可移植的容器中，然后发布到任何流行的 Linux 机器上，也可以实现虚拟化。容器是完全使用沙箱机制，相互之间不会有任何接口。

## Deepin 中的 Docker

Deepin 官方的应用仓库已经集成了 docker，但不是类似于 docker-ce 这样的最新版本。由于 Deepin 是基于 debian 的 unstable 版本开发的，通过 $(lsb_release -cs) 获取到的版本信息为 unstable，而 docker 官方源并没支持 debian 的 unstable 版本，因此使用 docker 官方教程是安装不成功的。如果你需要安装 docker-ce，请遵循下面的步骤进行安装：

## 在Deepin中安装Docker

1. 卸载老版本

    ``` bash
    sudo apt-get remove docker.io docker-engine
    ```

2. 安装密钥管理与下载相关的工具

    ``` bash
    // 密钥管理（add-apt-repository ca-certificates 等）与下载（curl 等）相关的工具
    sudo apt-get install apt-transport-https ca-certificates curl python-software-properties software-properties-common
    
    ```

    此处可能会提示 python-software-properties 未安装成功或其他的问题，最后导致 add-apt-repository 命令无法使用

    解决办法：

    ``` bash
    sudo apt-get install python-software-properties
    sudo apt-get update
    sudo apt install software-properties-common
    sudo apt-get update
    ```

3. 下载并安装密钥

    鉴于国内网络问题，强烈建议使用国内源，官方源请在注释中查看。

    国内源可选用清华大学开源软件镜像站或中科大开源镜像站，示例选用了中科大的。

    为了确认所下载软件包的合法性，需要添加软件源的 GPG 密钥。

    ``` bash
    // 中科大源
    curl -fsSL https://mirrors.ustc.edu.cn/docker-ce/linux/debian/gpg | sudo apt-key add -

    // 官方源，能否成功可能需要看运气。
    // curl -fsSL https://download.docker.com/linux/debian/gpg | sudo apt-key add -
    ```

4. 查看密钥是否安装成功

    ``` bash
    sudo apt-key fingerprint 0EBFCD88
    ```

    如果安装成功，会出现如下内容：

    ``` bash
    pub 4096R/0EBFCD88 2017-02-22    Key fingerprint = 9DC8 5822 9FC7 DD38 854A E2D8 8D81 803C 0EBF CD88

    uid Docker Release (CE deb) <docker@docker.com>

    sub 4096R/F273FCD8 2017-02-22
    ```

5. 在 source.list 中添加 docker-ce 软件源

    ``` bash
    sudo add-apt-repository "deb [arch=amd64] https://mirrors.ustc.edu.cn/docker-ce/linux/debian buster stable" 
    #!!!!报错，则手动添加到 /etc/apt/sources.list中
    #// 官方源
    #// sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian buster stable"

    #// 15.10 会提示 aptsources.distro.NoDistroTemplateException: Error: could not find a distribution template for Deepin/stable

    #// 这里我们通过编辑 sudo vim /etc/apt/sources.list 添加一行即可，原因未知
    #//deb [arch=amd64] https://mirrors.ustc.edu.cn/docker-ce/linux/debian buster stable
    ```

    官方在 buster 位置使用的是 $(lsb_release -cs)，但之前已经解释过，在 deepin 里运行它得到的是 unstable，docker 官方不支持 unstable 版本！因此直接使用官方教程的命令会安装失败。

    更改方法：将上述命令中的版本名称 buster，替换成 deepin 基于的 debian 版本对应的代号。查看版本号的命令为：

    ``` bash
    cat /etc/debian_version.
    ```

    举例：

    a). 对于 deepin v20，我操作上面的命令得到 debain 版本是 10.5，debian 10.5 的代号是 buster

    b). 对于 deepin 15.9.2 基于 debian 9.0 , debian 9.0 的代号为 stretch,

    所以 deepin v20 上完整的添加信息为:

    ``` bash
    sudo add-apt-repository "deb [arch=amd64] https://mirrors.ustc.edu.cn/docker-ce/linux/debian buster stable"
    ```

    >或者

    手动添加到/etc/apt/sources.list

    ![换源图](https://img2020.cnblogs.com/blog/2065380/202011/2065380-20201125003339649-262684308.png)

    >图挂了去cnblog原址看

    具体代码：[Debian](https://www.debian.org/releases/index.zh-cn.html)

6. 更新仓库

    ``` bash
    sudo apt-get update
    ```

7. 安装 docker-ce

    ``` bash
    sudo apt-get install docker-ce
    ```

8. 查看 docker 版本

    ``` bash
    docker --version
    ```

9. 让普通用户也可运行 docker

    docker 只允许 root 用户执行，为让普通用户也可运行 docker，执行

    ``` bash
    sudo usermod -aG docker username
    ```

10. 启动 docker

    ``` bash
    systemctl start docker
    ```

11. 验证 docker 是否被正确安装并且能够正常使用

    ``` bash
    sudo docker run hello-world
    ```

## Docker UI 工具

Docker官方的Desktop现在有Linux版本：[Docker Desktop on Linux](https://docs.docker.com/desktop/linux/install/)

但是猜测是网络原因，官方的Desktop一直显示`Docker Destop Stopped`。Deepin的应用代理和系统代理都对其不起作用，遂卸载弃用。

换了`Portainer`，但是`Portainer`只有Personal免费，注意Commercial环境。

`Portainer`本身也是Web的管理界面，安装很简单，启用一个镜像即可。

[官方文档](https://docs.portainer.io/v/ce-2.11/start/install/server/docker/linux)

用到的Docker命令：

创建一个卷为其存储数据用：

``` bash
docker volume create portainer_data
```

启动Container：

``` bash
docker run -d -p 8000:8000 -p 9443:9443 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:2.11.1
```
