---
layout:     post
title:      springbootѧϰ
subtitle:   spring��������
date:       2018-06-04
author:     bang
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - spring 
    - springboot
---

>springbootѧϰ�ʼ�

# spring����(��)

### Spring Aware

	��ʵ�ʵ���Ŀ�У����ܲ��ɱ������Ҫʹ��spring��������Ĺ��ܣ��������bean������ʶ��Spring�����Ĵ��ڣ����ܵ���spring���ṩ����Դ��
�����Spring Aware��Spring Aware��������Ƹ�Spring�ڲ�ʹ�õģ���ʹ��Spring Aware��bean�����Spring������ϡ�

	Spring�ṩ��Aware�ӿ�����
1. BeanNameAware             ��ȡ������bean����
2. BeanFactoryAware 	       ��ȡ��ǰbean factory�����Ե���bean�ķ���
3. ApplicationContextAware*  ��ȡ��ǰ��applicationContext�����Ե��������ķ���
4. MessageSourceAware        ���messageSource���������Ի�ȡ�ı���Ϣ
5. ApplicationEventPublisherAware  Ӧ���¼������������Է����¼�
6. ResourceLoaderAware       �����Դ�����������Ի���ⲿ��Դ�ļ�

ApplicationContext�ӿڼ̳���MessageSource ApplicationEventPublisher��ResourceLoader�ӿڣ���˼̳�ApplicationContext���Ի��Spring���������з���
����ԭ�������ǻ�����Ҫʲô�ӿڣ���ʵ��ʲô�ӿ�

### @EnableAsync �첽����

Springͨ������ִ������ʵ�ֶ��̺߳Ͳ�����̡�ʹ��ThreadPoolTaskExecutor��ʵ��һ�������̳߳ص�TaskExecutor��ʵ�ʿ�������������һ���Ƿ��谭�ģ����첽��
����ͨ������������ͨ��@EnableAsync�����첽�����֧�֣���ͨ����ʵ��ִ�е�Bean�ķ�����ʹ��@Asyncע����������һ���첽����

[�첽����demo]()

### @EnableScheduling ��ʱ����

spring��ʱ����ʵ�ֲ��衣

1. �����������ע��@EnableScheduling �����Լƻ������֧��
2. ��Ҫִ�е����񷽷��ϼ���@Scheduledע�⣬��������һ����ʱ����

### @Conditional

ͨ�����profile�����ǿ��Ի�ò�ͬ��bean��spring4�ṩ��һ����ͨ�õĻ���������bean�Ĵ�������ʹ��@Conditionalע�⡣
@Conditional��������ĳһ���ض���������һ���ض���bean

