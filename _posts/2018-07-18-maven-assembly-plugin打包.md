---
layout:     post
title:     	maven-assembly-plugin打包工具
subtitle:   assembly打包工具使用
date:       2018-07-18
author:     bang
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - maven-assebly-plugin 
    - java
---

>assembly打包工具使用

# assembly使用

### maven-assembly-plugin项目打包工具使用
   1. pom.xml文件中引入相关插件
   <pre>
			<build>
				<resources>
					<!--
             | 有几个路径，就对应几个 resource 标签
             | 或：
             | 一个目录，对应一个 resource 标签
          -->
					<resource>
						<directory>src/main/resources</directory>
						<filtering>true</filtering>
						<includes>
							<include>application.properties</include>
						</includes>
					</resource>
					<resource>
						<directory>src/main/resources</directory>
						<filtering>false</filtering>
						<excludes>
							<exclude>application.properties</exclude>
						</excludes>
					</resource>
				</resources>
				<plugins>
					<plugin>
						<artifactId>maven-assembly-plugin</artifactId>
						<configuration>
							<descriptors>
								<descriptor>src/main/assembly/assembly.xml</descriptor>
							</descriptors>
						</configuration>
						<executions>
							<execution>
								<id>make-assembly</id>
								<phase>package</phase>
								<goals>
									<goal>single</goal>
								</goals>
							</execution>
						</executions>
					</plugin>
				</plugins>
			</build>
	</pre>
	2.在src/main下新建assembly文件夹,并在其下增加bin文件夹和assembly.xml文件
		src
			 --main
			 		 -- assembly
			 		 					-- bin 
			 		 							-- boot.sh
			 		 					-- assebmly.xml
			 		 -- java 
			 		 -- resources 
			 --test
			 
		assembly.xml 文件内容(具体含义参见相关资料)
		<pre>
				<!--
				 - Copyright 1999-2011 Alibaba Group.
				 -
				 - Licensed under the Apache License, Version 2.0 (the "License");
				 - you may not use this file except in compliance with the License.
				 - You may obtain a copy of the License at
				 -
				 -      http://www.apache.org/licenses/LICENSE-2.0
				 -
				 - Unless required by applicable law or agreed to in writing, software
				 - distributed under the License is distributed on an "AS IS" BASIS,
				 - WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
				 - See the License for the specific language governing permissions and
				 - limitations under the License.
				-->
				<assembly>
				    <id>assembly</id>
				    <formats>
				        <format>tar.gz</format>
				    </formats>
				    <includeBaseDirectory>true</includeBaseDirectory>
				    <fileSets>
				        <fileSet>
				            <directory>src/main/assembly/bin</directory>
				            <outputDirectory>bin</outputDirectory>
				            <fileMode>0755</fileMode>
				        </fileSet>
				        <fileSet>
				            <directory>src/main/resources</directory>
				            <outputDirectory>config</outputDirectory>
				            <includes>
				                <include>logback-spring.xml</include>
				                <include>application.properties</include>
				            </includes>
				            <fileMode>0644</fileMode>
				        </fileSet>
				    </fileSets>
				    <dependencySets>
				        <dependencySet>
				            <outputDirectory>lib</outputDirectory>
				        </dependencySet>
				    </dependencySets>
				</assembly>
		</pre>
		
		3. boot.sh 文件内容
		<pre>
			#!/bin/sh
				# 定义几个变量 
				PRG_NAME=cu-serviceapi-server
				WORK_DIR=$(cd `dirname $0`; pwd)/../
				LOG_DIR="$WORK_DIR"/logs
				PID_FILE=${LOG_DIR}/${PRG_NAME}.pid
				
				JAVA=java
				JAVA_OPTS="-Djava.io.tmpdir=$WORK_DIR/tmp -Xms256m -Xmx512m -XX:+UseParNewGC -XX:+UseConcMarkSweepGC -XX:-CMSConcurrentMTEnabled -XX:CMSInitiatingOccupancyFraction=70 -XX:+CMSParallelRemarkEnabled -Dwork.dir=${WORK_DIR}"
				CLASS_PATH=" -classpath "$(echo ${WORK_DIR}lib/*.jar|sed 's/ /:/g')
				#CLASS_PATH=" -Djava.ext.dirs=lib "
				
				# 修改成自己的启动类
				CLASS=com.aotain.serviceapi.server.ServiceapiServerApplication
				# springboot相关配置文件路径
				CONFIG_PATH=" --spring.config.location=$WORK_DIR/config/application.properties --logging.config=$WORK_DIR/config/logback-spring.xml"
				
				if [ ! -d "${LOG_DIR}" ]; then
				  mkdir -p ${LOG_DIR}
				fi
				
				if [ ! -d "$WORK_DIR/tmp" ]; then
				  mkdir -p $WORK_DIR/tmp
				fi
				
				cd $WORK_DIR
				
				case "$1" in
				
				  start)
				  	if [ -f "${PID_FILE}" ]; then
				    	echo "${PRG_NAME} is running,pid=`cat ${PID_FILE}`."
				    else
				    	exec "$JAVA" $JAVA_OPTS $CLASS_PATH $CLASS $CONFIG_PATH >> ${LOG_DIR}/${PRG_NAME}.log 2>&1 &
						echo "${PRG_NAME} is running,pid=$!."
				    	echo $! > ${PID_FILE}
				        echo "${PRG_NAME} start----> "`date  '+%Y-%m-%d %H:%M:%S'` >>${LOG_DIR}/${PRG_NAME}.out
				    fi
				    ;;
				
				  stop)
				  	if [ -f "${PID_FILE}" ]; then
				    	kill -15 `cat ${PID_FILE}`
				    	rm -rf ${PID_FILE}
				    	echo "${PRG_NAME} is stopped."
					echo "${PRG_NAME} end----> "`date  '+%Y-%m-%d %H:%M:%S'` >>${LOG_DIR}/${PRG_NAME}.out
				    else
				    	echo "${PRG_NAME} is not running."
				    fi
				    ;;
				
				  restart)
				    bin/$0 stop
				    sleep 1
				    bin/$0 start
				    ;;
				
				  status)
				  	if [ -f "${PID_FILE}" ]; then
				    	echo "${PRG_NAME} is running,pid=`cat ${PID_FILE}`."
				    else
				    	echo "${PRG_NAME} is not running."
				    fi
				    ;;
				
				  *)
				    echo "Usage: ${PRG_NAME}.sh {start|stop|restart|status}"
				    ;;
				
				esac
				
				exit 0
				
				
		</pre>	 			
	
	