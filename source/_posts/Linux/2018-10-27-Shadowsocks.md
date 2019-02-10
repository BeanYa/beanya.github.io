---
title: Shadowsocks
date: 2018-10-27 04:27:29
categories:
- Proxy
tags:
- VPS
- Linux
- Shadowsocks
- Proxy
---

# Shadowsocks是什么
Shadowsocks是GitHub上的一个开源项目（原作者Clowwindy因为某些原因移除了），提供双端Socks5代理服务。
有人拷贝了一份Shadowsocks的源码，[地址](https://github.com/ziggear/shadowsocks) 

# Shadowsocks安装

首先需要有一个可以进行登录的VPS，自行购买。

## 内核升级并开启TcpBBR拥塞控制

仅仅安装Shadowsocks是不够的，可以升级内核并开启TcpBBR拥塞控制，提升速度。

内核的升级用一键脚本完成即可
```
wget --no-check-certificate https://github.com/teddysun/across/raw/master/bbr.sh && chmod +x bbr.sh && ./bbr.sh
```
参考来自[秋水逸冰](https://teddysun.com/489.html)

升级完成并重启系统后，输入`uname -r` 可以查看内核版本，再用`lsmod | grep bbr`查看bbr模块是否开启成功，一般会输出`tcp_bbr *****`即可，也可能没有，不同VPS不同结果。

## Shadowsocks安装

官方提供Python版的安装

Debian / Ubuntu:
```
apt-get install python-pip
pip install shadowsocks
```

CentOS:
```
yum install python-setuptools && easy_install pip
pip install shadowsocks
```

Windows下需要先安装Python，官方说明需要安装对应版本的OpenSSL，未测试，之后再进行`pip install shadowsocks`
[详情](https://github.com/shadowsocks/shadowsocks/wiki/Install-Shadowsocks-Server-on-Windows)

## 开启Shadowsocks服务

示例
`ssserver -p 443 -k password -m aes-256-cfb`

后台运行`ssserver -p 443 -k password -m aes-256-cfb --user nobody -d start`

停止 `sudo ssserver -d stop`

日志 `sudo less /var/log/shadowsocks.log`

## 多端口运行

创建一个配置文件，如ss.json或者config.json

`vim ss.json`

以json方式配置Shadowsocks

以下是一个例子

``` json
{
	"server":"*.*.*.*",
	"local_address":"127.0.0.1",
	"local_port":1080,
	"port_password":{
		"8888":"temp",
        "8989":"temp"
    },
	"timeout":300,
	"method":"aes-256-cfb"
}
```

`*.*.*.*`为VPS公网地址
然后保存文件`:wq`

执行`ssserver -c ss.json -d start`

Shadowsocks服务即在后台运行

# 注意

单纯的执行Shadowsocks的服务命令还不够，还需要修改防火墙规则，面板可以直接在对应的放行端口添加，也可手动添加防火墙规则

例如Centos 7（或使用firewall-cmd做防火墙规则的）

`firewall-cmd --zone=public --add-port=端口号/tcp --permanent`
`firewall-cmd --zone=public --add-port=端口号/udp --permanent `

或

`firewall-cmd --zone=public --add-port=端口起始-端口终/tcp --permanent`
`firewall-cmd --zone=public --add-port=端口起始-端口终/udp --permanent`

其中`--permanent`为了规则持续生效，若不使用UDP转发，可以去掉第二行。

最后`firewall-cmd --reload`重启防火墙即可

# Windows客户端的连接

[下载Windows客户端](https://github.com/shadowsocks/shadowsocks-windows/releases)

直接打开即可，右下角任务栏右键小飞机，服务器地址填VPS公网IP或解析到该服务器的域名，服务器端口填上述ss.json或config.json中开放的端口，密码及加密方式对应填入，本地代理端口默认即可，修改为别的端口也行。

# 技巧

Shadowsocks可以在后台常驻，并且第一次生效后就可以关闭启动了（并不是退出程序，仅仅是关闭系统代理）。

其他程序需要代理时，仅需通过 Socks5 协议，在`127.0.0.1` 1080端口（默认本地代理端口），用户名密码置空或选择不验证即可实现代理。


# 多用户
Enable manager API by specifying --manager-address, which is either a Unix socket or an IP address:

    # Use a Unix socket
    ssserver --manager-address /var/run/shadowsocks-manager.sock -c tests/server-multi-passwd.json
    # Use an IP address
    ssserver --manager-address 127.0.0.1:6001 -c tests/server-multi-passwd.json
    
To add a port:

    add: {"server_port": 8001, "password":"7cd308cc059"}

To remove a port:

    remove: {"server_port": 8001}
    
echo:
    
    echo -n ping > /dev/udp/127.0.0.1/6001

demo:

    ssserver -p 8888 -k password -m aes-256-cfb --manager-address 127.0.0.1:6001