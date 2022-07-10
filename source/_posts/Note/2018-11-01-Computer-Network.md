---
title: Network
date: 2018-11-01 14:28:51
categories:
- Network
tags:
- Note
- Network
---
# 子网掩码

32位的连续1，用于划分子网。

例：1111 1111 1111 1111 1111 1111 1111 1111 = 255 255 255 255 = 255.255.255.255

# CIDR

192.168.1.0/24，表示32位中前24位为网络前缀（个人理解为主路由的IP地址），即还有8位用于表示`SubnetID`与`HostID`

例：
192.168.1.0/24 使用掩码255.255.255.240 划分子网，其可用子网数为（），每个子网内可用主机地址数为（）

* $Length(255.255.255.240)= 8+8+8+4 = 28$，子网数为 $2^{28-24}=2^4=16$个，除去子网全0和全1的地址，子网数为$16-2=14$个。
* 32位中剩余4位，同划分子网，也有$16$个HostID，再去掉全0和全1
答案： $14\quad14$

# Socket

# TCP

# UDP

# HTTP

* HTTP 协议是TCP/IP家族的一员，工作于应用层。
* 构建于TCP/IP上，默认端口为80
* HTTP的连接是无状态的

## HTTP包

HTTP的包形如：

    <Method> <RequestURL> <Version>

    <Headers>

    <entity-body>

Method包含四种方法:

* GET -- 查
* POST -- 增
* DELETE -- 删
* PUT -- 改

## GET

GET方法应只用于信息的获取，不增加/修改数据或影响数据的状态，是安全且幂等的。
> 幂等：对同一URL地址发起的多个请求应该得到相同的结果

GET请求报文示例：

    GET /books/?sex=man&name=Professional HTTP/1.1
    Host: www.example.com
    User-Agent: Mozilla/5.0 (Windows; U; Windows NT 5.1; en-US; rv:1.7.6)
    Gecko/20050225 Firefox/1.0.1
    Connection: Keep-Alive

POST请求报文示例：

    POST / HTTP/1.1
    Host: www.example.com
    User-Agent: Mozilla/5.0 (Windows; U; Windows NT 5.1; en-US; rv:1.7.6)
    Gecko/20050225 Firefox/1.0.1
    Content-Type: application/x-www-form-urlencoded
    Content-Length: 40
    Connection: Keep-Alive

    sex=man&name=Professional  

## POST
