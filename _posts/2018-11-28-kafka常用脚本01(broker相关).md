---
layout:     post
title:      kafka学习笔记
subtitle:   kafka常用脚本
date:       2018-11-30
author:     bang
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - kafka
    - zookeeper
---

# kafka常用脚本

## broker相关脚本
### kafka-server-start.sh
	启动broker
	kafka需要依赖zookeeper提供服务，因此启动kafka broker(服务器)之前需要先启动并配置好zookeeper信息
	
	kafka启动时需要指定配置文件
	bin/kafka-server-start.sh -deamon <path>/server.properties 或者
	nohup bin/kafka-server-start.sh <path>/server.properties &
	
	启动后可以在kafka安装目录同级logs目录下查看kafka启动服务信息 log.dirs 配置的是kafka消息数据日志写入的目录
	
### kafka-server-stop.sh
	该脚本会搜寻当前机器中所有的kafka broker进程，然后关闭它们。如果用户机器上存在多个broker进程，该脚本则会全部关掉它们。
	
	-- 注意
	使用此命令关闭broker时可能会因为kafka安装目录过长，导致执行关闭脚本中的ps ax 和 grep查找kafka进程号失败，从而导致无法正常关闭。
	
	遇到此问题可通过
	-- 1.jps查看kafka pid 或者使用ps ax|grep -i 'kafka\.Kafka'|grep -v grep |awk '{print $1}'命令查找kafka pid
	-- 2.运行kill -s TERM $PID关闭broker
