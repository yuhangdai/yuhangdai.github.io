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

## consumer相关脚本

### kafka-consumer-groups.sh
	
	参数及其含义
	--bootstrap-server	指定kafka集群的broker列表，CSV格式，查询新版本消费者组时使用
	--list   列出集群当前所有消费者组
	--describe 查询消费者组详情
	--group 指定消费者组名称
	--zookeeper 指定zookeeper连接信息，查询老版本消费者组时使用
	--reset-offsets 重新设置消费者组位移
	
	--> 新版本查询消费者组信息
	bin/kafka-consumer-groups.sh --bootstrap-server localhost:2181 --list
	
	--> kafka-producer-perf-test.sh 使用producer性能测试脚本生产数据方便测试
	bin/kafka-producer-perf-test.sh --topic test --throughput -1 --num-records 500000 --record-size 100 --producer-props bootstrap.servers=localhost:9092 acks=-1