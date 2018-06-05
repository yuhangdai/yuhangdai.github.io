---
layout:     post
title:      markdown语法
subtitle:   初识markdown语法
date:       2018-06-03
author:     bang
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - markdown
---

>springboot学习笔记

# springboot学习笔记-spring基础(一)

### 基础配置
  #### spring框架四大原则
  1) 使用POJO进行轻量级和最小侵入式开发
  2) 通过依赖注入和接口编程实现松耦合
  3) 通过AOP和默认习惯进行声明式编程
  4) 使用AOP和模板减少模块化代码

### springbean扫描路径配置
  使用@Configuration @ComponentScan配置需要扫描的路径

### java配置和注解配置
  Java配置通过@Configuration 和@Bean实现
  #### @Configuration声明当前类是一个配置类，相当于一个spring配置的xml文件
  #### @Bean注解在方法上，声明当前方法返回值是一个Bean

  全局配置使用java配置，业务Bean使用注解配置(@Controller @Service @Repository @Component)

 ### AOP
   #### springboot引入aop支持
   1) 引入依赖包 spring-aop aspectjrt aspectjweaver

 	<!-- https://mvnrepository.com/artifact/org.springframework/spring-aop -->
	<dependency>
		<groupId>org.springframework</groupId>
		<artifactId>spring-aop</artifactId>
		<version>5.0.2.RELEASE</version>
	</dependency>
	<!-- https://mvnrepository.com/artifact/org.aspectj/aspectjrt -->
	<dependency>
		<groupId>org.aspectj</groupId>
		<artifactId>aspectjrt</artifactId>
		<version>1.9.1</version>
	</dependency>
	<!-- https://mvnrepository.com/artifact/org.aspectj/aspectjweaver -->
	<dependency>
		<groupId>org.aspectj</groupId>
		<artifactId>aspectjweaver</artifactId>
		<version>1.9.1</version>
	</dependency>

  2) 定义拦截注解    
  3）编写待拦截类，并在相应方法上添加注解      
  4) 编写切面（定义切点PointCut Advice 切面公共方法逻辑）        
  5）配置切面类Java配置，并开启切面注解支持        




