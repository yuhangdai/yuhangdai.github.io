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

## broker��ؽű�
### kafka-server-start.sh
	����broker
	kafka��Ҫ����zookeeper�ṩ�����������kafka broker(������)֮ǰ��Ҫ�����������ú�zookeeper��Ϣ
	
	kafka����ʱ��Ҫָ�������ļ�
	bin/kafka-server-start.sh -deamon <path>/server.properties ����
	nohup bin/kafka-server-start.sh <path>/server.properties &
	
	�����������kafka��װĿ¼ͬ��logsĿ¼�²鿴kafka����������Ϣ log.dirs ���õ���kafka��Ϣ������־д���Ŀ¼
	
### kafka-server-stop.sh
	�ýű�����Ѱ��ǰ���������е�kafka broker���̣�Ȼ��ر����ǡ�����û������ϴ��ڶ��broker���̣��ýű����ȫ���ص����ǡ�
	
	-- ע��
	ʹ�ô�����ر�brokerʱ���ܻ���Ϊkafka��װĿ¼����������ִ�йرսű��е�ps ax �� grep����kafka���̺�ʧ�ܣ��Ӷ������޷������رա�
	
	�����������ͨ��
	-- 1.jps�鿴kafka pid ����ʹ��ps ax|grep -i 'kafka\.Kafka'|grep -v grep |awk '{print $1}'�������kafka pid
	-- 2.����kill -s TERM $PID�ر�broker
