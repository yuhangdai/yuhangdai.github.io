---
layout:     post
title:      redis��װ
subtitle:   linuxϵͳ��װredis�Լ�redis-python�ͻ���
date:       2018-06-03
author:     bang
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - redis
---

> redis-in-actionѧϰ�ʼ�

# linuxϵͳ��װredis

### ��װ����redis����

1. ����redisѹ��������ѹ [����·��](https://redis.io/)
2. make�������Դ�ļ� 
	![���뱨�� gcc command not found](./../img/redis-setup/make-error-1.png)
	���������linuxϵͳ������gcc���� yum install gcc
	![���뱨�� jemalloc/jemalloc.h: No such file or directory](./../img/redis-setup/make-error-2.png)
	�������: [ִ��make����ʱ����MALLOC=jemalloc����](https://blog.csdn.net/bugall/article/details/45914867)
3. make install
4. redis-server redis.conf����redis����

### ��װpython����redis�ͻ���
1.�鿴linux�Ƿ�װpython(Ĭ�ϰ�װ��python�汾,û����װ)
	python --version

2.����setuptoolsģ�鲢��ѹ���ļ�
	[���ص�ַ](https://pypi.io/packages/source/s/setuptools/setuptools-33.1.1.zip)

3.�����ѹ�ļ���ִ��python���װreids hiredis�ͻ���
	sudo python -m easy_install redis hiredis
	[��װ���� error: Setup script exited with error: command 'gcc' failed with exit status 1](./../img/redis-setup/setuptools-error-1.png)
	����:�����ļ�������Ҫ��װpython-devel(yum install python-devel) [ԭ��·��](https://blog.csdn.net/qq_41746437/article/details/79340299 "why need python-devel")

4.ִ����������  
	python  
	>>>import redis  
	>>>conn = redis.Redis()  
	>>>conn.set('hello','world')  
������true���ʾ�ɹ���ǰ����redis����Ҫ����������ᱨ�����쳣����

### ��redis����Ϊ����������
[ԭ������](http://blog.csdn.net/lovejj1994/article/details/53096268)

	