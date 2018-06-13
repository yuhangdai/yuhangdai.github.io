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

### Spring Aware

	在实际的项目中，可能不可避免的需要使用spring容器本身的功能，这是你的bean必须意识到Spring容器的存在，才能调用spring所提供的资源，
这就是Spring Aware。Spring Aware本来是设计给Spring内部使用的，若使用Spring Aware，bean将会和Spring容器耦合。

	Spring提供的Aware接口如下
1. BeanNameAware             获取容器中bean名称
2. BeanFactoryAware 	       获取当前bean factory，可以调用bean的服务
3. ApplicationContextAware*  获取当前的applicationContext，可以调用容器的服务
4. MessageSourceAware        获得messageSource，这样可以获取文本信息
5. ApplicationEventPublisherAware  应用事件发布器，可以发布事件
6. ResourceLoaderAware       获得资源加载器，可以获得外部资源文件

ApplicationContext接口继承了MessageSource ApplicationEventPublisher和ResourceLoader接口，因此继承ApplicationContext可以获得Spring容器的所有服务，
但是原则是我们还是需要什么接口，就实现什么接口

### @EnableAsync 异步任务

Spring通过任务执行器来实现多线程和并发编程。使用ThreadPoolTaskExecutor可实现一个基于线程池的TaskExecutor。实际开发过程中任务一般是非阻碍的，即异步的
我们通过在配置类中通过@EnableAsync开启异步任务的支持，并通过在实际执行的Bean的方法中使用@Async注解声明其是一个异步任务

[异步任务demo]()

### @EnableScheduling 定时任务

spring定时任务实现步骤。

1. 在配置类加上注解@EnableScheduling 开启对计划任务的支持
2. 在要执行的任务方法上加上@Scheduled注解，声明这是一个定时任务

### @Conditional

通过活动的profile，我们可以获得不同的bean。spring4提供了一个更通用的基于条件的bean的创建，即使用@Conditional注解。
@Conditional根据满足某一个特定条件创建一个特定的bean

