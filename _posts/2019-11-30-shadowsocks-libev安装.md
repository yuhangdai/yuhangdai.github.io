---
layout:     post
title:      shadowsocks安装
subtitle:   shadowsocks
date:       2019-10-24
author:     bang
header-img: img/post-bg-2015.jpg
catalog: true
tags:
    - linux
    - shadowsocks
---

### **安装shadowsocks-libev**
	cd /etc/yum.repos.d/
	curl -O url
	centos7 url=https://copr.fedorainfracloud.org/coprs/librehat/shadowsocks/repo/epel-7/librehat-shadowsocks-epel-7.repo
	centos8 url=https://copr.fedorainfracloud.org/coprs/outman/shadowsocks-libev/repo/epel-8/outman-shadowsocks-libev-epel-8.repo

安装

?	yum update
?	yum install -y epel-release
?	yum install -y libsodium shadowsocks-libev simple-obfs
?	yum install -y shadowsocks-libev
?	
?	

### 修改ss参数
	cd /etc/shadowsocks-libev，查看是否存在config.json，如果不存在该文件则需要新建。
	
	配置对应的参数：
	
	server：当前自己的服务器的地址
	比如：0.0.0.0
	
	server_port：ss服务的端口
	一般要大于1024，小于65536,需要确保防火墙开放此端口
	
	password：ss客户端连接时要使用的密码


	method：加密方式
	常用的方式是：aes-256-cfb
	
	timeout：超时时间，单位：秒
	比如：300
	
	mode：ss服务的模式
	比如：tcp_and_udp，即支持tcp也支持udp

### **打开防火墙对应端口**
	firewall-cmd --permanent --add-port=xxxx/tcp
	firewall-cmd --reload
	
	确认端口是否已开放
	netstat -tnlp | grep xxxx

### **启动shadowsocks**
	systemctl restart shadowsocks-libev
设置开机自启动
	systemctl enable shadowsocks-libev
查看服务状态
	systemctl status shadowsocks-libev	