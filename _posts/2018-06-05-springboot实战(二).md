---
layout:     post
title:      springboot学习
subtitle:   spring常用配置
date:       2018-06-04
author:     bang
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - spring 
    - springboot
---

>springboot学习笔记

# spring基础(二)

### @Value使用Spring EL为属性注入值

1. 注入普通字符
2. 注入操作系统属性
3. 注入表达式运算结果
4. 注入其它Bean的属性
5. 注入文件内容
6. 注入网址内容
7. 注入属性文件

### @PostConstruct @PreDestroy

在构造器完成之后和销毁之前执行一些逻辑

### Profile

Profile为在不同环境下使用不同的配置提供了支持
1) 通过设定Environment的ActiveProfiles来设定当前context需要使用的配置环境，在开发中使用@Profile注解类和方法，达到在不同情况下实例化不同bean目的
2) 通过设定jvm的spring.profiles.active参数来设置环境变量
3) Web项目设置在Servlet的context parameter中


### Spring事件

Spring的事件为bean与bean之间的消息通信提供了支持。当一个Bean处理完一个任务之后，需要通知另外一个Bean作相应的处理
只需要让另外Bean监听当前Bean所发送的事件即可

1) 自定义事件，继承ApplicationEvent
2) 定义事件监听器，实现ApplicationListener
3) 使用容器发布事件



