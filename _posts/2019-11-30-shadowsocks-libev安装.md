---
layout:     post
title:      shadowsocks��װ
subtitle:   shadowsocks
date:       2019-10-24
author:     bang
header-img: img/post-bg-2015.jpg
catalog: true
tags:
    - linux
    - shadowsocks
---

### **��װshadowsocks-libev**
	cd /etc/yum.repos.d/
	curl -O url
	centos7 url=https://copr.fedorainfracloud.org/coprs/librehat/shadowsocks/repo/epel-7/librehat-shadowsocks-epel-7.repo
	centos8 url=https://copr.fedorainfracloud.org/coprs/outman/shadowsocks-libev/repo/epel-8/outman-shadowsocks-libev-epel-8.repo

��װ

?	yum update
?	yum install -y epel-release
?	yum install -y libsodium shadowsocks-libev simple-obfs
?	yum install -y shadowsocks-libev
?	
?	

### �޸�ss����
	cd /etc/shadowsocks-libev���鿴�Ƿ����config.json����������ڸ��ļ�����Ҫ�½���
	
	���ö�Ӧ�Ĳ�����
	
	server����ǰ�Լ��ķ������ĵ�ַ
	���磺0.0.0.0
	
	server_port��ss����Ķ˿�
	һ��Ҫ����1024��С��65536,��Ҫȷ������ǽ���Ŵ˶˿�
	
	password��ss�ͻ�������ʱҪʹ�õ�����


	method�����ܷ�ʽ
	���õķ�ʽ�ǣ�aes-256-cfb
	
	timeout����ʱʱ�䣬��λ����
	���磺300
	
	mode��ss�����ģʽ
	���磺tcp_and_udp����֧��tcpҲ֧��udp

### **�򿪷���ǽ��Ӧ�˿�**
	firewall-cmd --permanent --add-port=xxxx/tcp
	firewall-cmd --reload
	
	ȷ�϶˿��Ƿ��ѿ���
	netstat -tnlp | grep xxxx

### **����shadowsocks**
	systemctl restart shadowsocks-libev
���ÿ���������
	systemctl enable shadowsocks-libev
�鿴����״̬
	systemctl status shadowsocks-libev	