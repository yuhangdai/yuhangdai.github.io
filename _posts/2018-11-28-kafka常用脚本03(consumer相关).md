---
layout:     post
title:      kafkaѧϰ�ʼ�
subtitle:   kafka���ýű�
date:       2018-11-30
author:     bang
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - kafka
    - zookeeper
---

# kafka���ýű�

## consumer��ؽű�

### kafka-consumer-groups.sh
	
	�������京��
	--bootstrap-server	ָ��kafka��Ⱥ��broker�б�CSV��ʽ����ѯ�°汾��������ʱʹ��
	--list   �г���Ⱥ��ǰ������������
	--describe ��ѯ������������
	--group ָ��������������
	--zookeeper ָ��zookeeper������Ϣ����ѯ�ϰ汾��������ʱʹ��
	--reset-offsets ����������������λ��
	
	--> �°汾��ѯ����������Ϣ
	bin/kafka-consumer-groups.sh --bootstrap-server localhost:2181 --list
	
	--> kafka-producer-perf-test.sh ʹ��producer���ܲ��Խű��������ݷ������
	bin/kafka-producer-perf-test.sh --topic test --throughput -1 --num-records 500000 --record-size 100 --producer-props bootstrap.servers=localhost:9092 acks=-1