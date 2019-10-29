---
layout:     post
title:      面试常见问题
subtitle:   面试问题
date:       2019-10-24
author:     bang
header-img: img/post-bg-2015.jpg
catalog: true
tags:
    - interview
    - 面试题
---

#### [.md语法](http://xianbai.me/learn-md/article/syntax/horizontal-rule.html)

#### javascript
1. [**laydate无法重复渲染问题**]()：删除原有元素然后拼接新元素，再进行渲染

		
#### java

1. **服务不可用原因**：
	- 硬件问题
	- 软件问题（程序bug）
	- 中间件（缓存雪崩等）：
		缓存击穿一般发生在缓存应用重启, 所有缓存被清空时,以及短时间内大量缓存失效时. 
		大量的缓存不命中, 使请求直击后端,造成服务提供者超负荷运行,引起服务不可用.
	- 用户量大

2. [**java定时任务**](https://juejin.im/post/5ca761c36fb9a05e2726b18e)
	**动态修改定时任务cron表达式**
		

		
#### [redis文档](https://gnuhpc.gitbooks.io/redis-all-about/Problem/memory/scan-bigkey.html)

1. [**hash算法和一致性hash算法**](https://segmentfault.com/a/1190000017847097)

	- **hash算法**	
	优点：对hash(key)%index然后将对对应key的操作映射到同一主机上
	缺点：新增、删除主机会导致大量key的重新散列和存储
	
	- **一致性hash算法**
	优点
		容错性：A节点宕机只会导致A节点数据重新散列
		扩展性：增加D节点只会导致节点增加D节点前的部分数据需要重新散列
	缺点
		数据倾斜（数据分布不平衡）
	
	- **虚拟节点机制**
		对每个节点计算多个哈希值，每个计算结果位置都放置在对应节点中，这些节点称为虚拟节点。
		然后建立虚拟节点到实际节点的对应关系
		
2. **缓存穿透**

    缓存穿透是指查询一个一定不存在的数据，由于缓存是不命中时被动写的，并且出于容错考虑,
如果从存储层查不到数据则不写入缓存，这将导致这个不存在的数据每次请求都要到存储层去查
询,失去了缓存的意义。在流量大时，可能DB就挂掉了，要是有人利用不存在的key频繁攻击我们
的应用,这就是漏洞

	**解决方案**
  - 采用布隆过滤器，将数据库中数据保存到bitmap，过滤到不存在的数据避免查询数据库。
  - 查询返回的数据为空（不管是数 据不存在，还是系统故障），我们仍然把这个空结果进
  	行缓存，但它的过期时间会很短，最长不超过五分钟
  

3. **缓存雪崩**

	缓存key采用相同的过期策略，导致缓存在同一时间失效，所有查询都请求DB，导致DB压力过大雪崩。
	
	**解决方案**
	- 缓存失效时间分散开	
	- 用加锁或者队列的方式保证缓存的单线 程（进程）写
		
4. **缓存击穿**	
	”热点“key缓存数据失效时，被高并发访问（**击穿**针对的是单个”热点“key，**雪崩**是针对多个key）
	
	[**解决方案**](https://www.iteye.com/blog/carlosfu-2269687)
	- 使用互斥锁
	- "提前"使用互斥锁(mutex key)
	- "永远不过期"
	- 资源保护
	
5. **大key问题**
	- 读写大key会导致超时严重，甚至阻塞服务
	- 如果删除大key，DEL命令可能阻塞Redis进程数十秒，使得其他请求阻塞，对应用程序和
	Redis集群可用性造成严重的影响
	
	**解决方案**[1](https://blog.csdn.net/u013474436/article/details/88808914)[2](https://www.iteye.com/blog/carlosfu-2269687)
	-	对象需要每次都整存整取
		可以尝试将对象分拆成几个key-value， 使用multiGet获取值，这样分拆的意义在于分拆
		单次操作的压力，将操作压力平摊到多个redis实例中，降低对单个redis的IO影响；
	- 对象每次只需要存取部分数据
		可以像第一种做法一样，分拆成几个key-value， 也可以将这个存储在一个hash中，每个
		field代表一个具体的属性，使用hget,hmget来获取部分的value，使用hset，hmset来更
		新部分属性
	
### mysql	
	1. select a from table_x order by b 建立合适索引 

	
### springboot
1. [已有parent的module项目中引入springboot](https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/#using-boot-maven-without-a-parent)
2. [自动配置原理]()


	
### springcloud

- **Eureka**
- **Feign**
- **Ribbon**
- **Hystrix**
- **Zuul**
	
	
### 架构演变
	1.单节点，单应用，单数据库
	2.单节点，单应用
	