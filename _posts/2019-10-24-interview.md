---
layout:     post
title:      ���Գ�������
subtitle:   ��������
date:       2019-10-24
author:     bang
header-img: img/post-bg-2015.jpg
catalog: true
tags:
    - interview
    - ������
---

#### [.md�﷨](http://xianbai.me/learn-md/article/syntax/horizontal-rule.html)

#### javascript
1. [**laydate�޷��ظ���Ⱦ����**]()��ɾ��ԭ��Ԫ��Ȼ��ƴ����Ԫ�أ��ٽ�����Ⱦ

		
#### java

1. **���񲻿���ԭ��**��
	- Ӳ������
	- �������⣨����bug��
	- �м��������ѩ���ȣ���
		�������һ�㷢���ڻ���Ӧ������, ���л��汻���ʱ,�Լ���ʱ���ڴ�������ʧЧʱ. 
		�����Ļ��治����, ʹ����ֱ�����,��ɷ����ṩ�߳���������,������񲻿���.
	- �û�����

2. [**java��ʱ����**](https://juejin.im/post/5ca761c36fb9a05e2726b18e)
	**��̬�޸Ķ�ʱ����cron����ʽ**
		
#### mybatisԭ��
	mybatis��ֵ����(mybatis��select˳����и�ֵ����select a��b��c��d������Ϊa b c d���Ը�ֵ)
	���DefaultResultSetHandler#applyAutomaticMappings()

		
#### [redis�ĵ�](https://gnuhpc.gitbooks.io/redis-all-about/Problem/memory/scan-bigkey.html)

1. [**hash�㷨��һ����hash�㷨**](https://segmentfault.com/a/1190000017847097)

	- **hash�㷨**	
	�ŵ㣺��hash(key)%indexȻ�󽫶Զ�Ӧkey�Ĳ���ӳ�䵽ͬһ������
	ȱ�㣺������ɾ�������ᵼ�´���key������ɢ�кʹ洢
	
	- **һ����hash�㷨**
	�ŵ�
		�ݴ��ԣ�A�ڵ�崻�ֻ�ᵼ��A�ڵ���������ɢ��
		��չ�ԣ�����D�ڵ�ֻ�ᵼ�½ڵ�����D�ڵ�ǰ�Ĳ���������Ҫ����ɢ��
	ȱ��
		������б�����ݷֲ���ƽ�⣩
	
	- **����ڵ����**
		��ÿ���ڵ��������ϣֵ��ÿ��������λ�ö������ڶ�Ӧ�ڵ��У���Щ�ڵ��Ϊ����ڵ㡣
		Ȼ��������ڵ㵽ʵ�ʽڵ�Ķ�Ӧ��ϵ
		
2. **���洩͸**

    ���洩͸��ָ��ѯһ��һ�������ڵ����ݣ����ڻ����ǲ�����ʱ����д�ģ����ҳ����ݴ�����,
����Ӵ洢��鲻��������д�뻺�棬�⽫������������ڵ�����ÿ������Ҫ���洢��ȥ��
ѯ,ʧȥ�˻�������塣��������ʱ������DB�͹ҵ��ˣ�Ҫ���������ò����ڵ�keyƵ����������
��Ӧ��,�����©��

	**�������**
  - ���ò�¡�������������ݿ������ݱ��浽bitmap�����˵������ڵ����ݱ����ѯ���ݿ⡣
  - ��ѯ���ص�����Ϊ�գ��������� �ݲ����ڣ�����ϵͳ���ϣ���������Ȼ������ս����
  	�л��棬�����Ĺ���ʱ���̣ܶ�������������
  

3. **����ѩ��**

	����key������ͬ�Ĺ��ڲ��ԣ����»�����ͬһʱ��ʧЧ�����в�ѯ������DB������DBѹ������ѩ����
	
	**�������**
	- ����ʧЧʱ���ɢ��	
	- �ü������߶��еķ�ʽ��֤����ĵ��� �̣����̣�д
		
4. **�������**	
	���ȵ㡰key��������ʧЧʱ�����߲������ʣ�**����**��Ե��ǵ������ȵ㡰key��**ѩ��**����Զ��key��
	
	[**�������**](https://www.iteye.com/blog/carlosfu-2269687)
	- ʹ�û�����
	- "��ǰ"ʹ�û�����(mutex key)
	- "��Զ������"
	- ��Դ����
	
5. **��key����**
	- ��д��key�ᵼ�³�ʱ���أ�������������
	- ���ɾ����key��DEL�����������Redis������ʮ�룬ʹ������������������Ӧ�ó����
	Redis��Ⱥ������������ص�Ӱ��
	
	**�������**[1](https://blog.csdn.net/u013474436/article/details/88808914)[2](https://www.iteye.com/blog/carlosfu-2269687)
	-	������Ҫÿ�ζ�������ȡ
		���Գ��Խ�����ֲ�ɼ���key-value�� ʹ��multiGet��ȡֵ�������ֲ���������ڷֲ�
		���β�����ѹ����������ѹ��ƽ̯�����redisʵ���У����ͶԵ���redis��IOӰ�죻
	- ����ÿ��ֻ��Ҫ��ȡ��������
		�������һ������һ�����ֲ�ɼ���key-value�� Ҳ���Խ�����洢��һ��hash�У�ÿ��
		field����һ����������ԣ�ʹ��hget,hmget����ȡ���ֵ�value��ʹ��hset��hmset����
		�²�������
	
### mysql	
	1. select a from table_x order by b ������������ 

	
### springboot
1. [����parent��module��Ŀ������springboot](https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/#using-boot-maven-without-a-parent)
��pom�ļ����������´��룺

		<dependencies>
		  ...
		  <dependency>
		      <groupId>org.springframework.boot</groupId>
		      <artifactId>spring-boot-autoconfigure</artifactId>
		      <version>${spring.boot.version}</version>
		  </dependency>
		</dependencies>
		<dependencyManagement>
		  <dependencies>
		      <dependency>
		          <groupId>org.springframework.boot</groupId>
		          <artifactId>spring-boot-autoconfigure</artifactId>
		          <version>${spring.boot.version}</version>
		          <type>pom</type>
		          <scope>import</scope>
		      </dependency>
		      <dependency>
		          <groupId>org.springframework.boot</groupId>
		          <artifactId>spring-boot-dependencies</artifactId>
		          <version>${spring.boot.version}</version>
		          <type>pom</type>
		          <scope>import</scope>
		      </dependency>
		  </dependencies>
		</dependencyManagement>
		
2. [�Զ�����ԭ��]()


	
### springcloud

- **Eureka**
- **Feign**
- **Ribbon**
- **Hystrix**
- **Zuul**
	
	
### �ܹ��ݱ�
	1.���ڵ㣬��Ӧ�ã������ݿ�
	2.���ڵ㣬��Ӧ��


### javascript
#### bootstrap table
	1.**bootstrap table �������к�**

		{	
			title: '���',
			width:'60px',
			formatter:function (value, row, index){
        var page = $('#helpTable').bootstrapTable("getPage");
        return page.pageSize*(page.pageNumber - 1) + index + 1;
    	}
    },
  2.bootstrap table **ˢ������**

		searchBtnClick:function () {
			$("#searchBtn").on('click',function () {
				$("#helpTable").bootstrapTable('refreshOptions',{pageNumber:1, url:systemHelpUrl.listData});
				$("#helpTable").bootstrapTable('refresh', systemHelpUrl.listData);
			})
		},

#### prettyfile

	��̬���ӵ�input[file](prettyfile)��ʼ��
		$("#inputid").prettyFile();
	�ظ���ʼ������
		�ᵼ�³��ֶ��input��