---
layout:     post
title:     	maven-assembly-plugin�������
subtitle:   assembly�������ʹ��
date:       2018-07-18
author:     bang
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - maven-assebly-plugin 
    - java
---

>assembly�������ʹ��

# assemblyʹ��

### maven-assembly-plugin��Ŀ�������ʹ��
   1. pom.xml�ļ���������ز��
   <pre>
			<build>
				<resources>
					<!--
             | �м���·�����Ͷ�Ӧ���� resource ��ǩ
             | ��
             | һ��Ŀ¼����Ӧһ�� resource ��ǩ
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
	2.��src/main���½�assembly�ļ���,������������bin�ļ��к�assembly.xml�ļ�
		src
			 --main
			 		 -- assembly
			 		 					-- bin 
			 		 							-- boot.sh
			 		 					-- assebmly.xml
			 		 -- java 
			 		 -- resources 
			 --test
			 
		assembly.xml �ļ�����(���庬��μ��������)
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
		
		3. boot.sh �ļ�����
		<pre>
			#!/bin/sh
				# ���弸������ 
				PRG_NAME=cu-serviceapi-server
				WORK_DIR=$(cd `dirname $0`; pwd)/../
				LOG_DIR="$WORK_DIR"/logs
				PID_FILE=${LOG_DIR}/${PRG_NAME}.pid
				
				JAVA=java
				JAVA_OPTS="-Djava.io.tmpdir=$WORK_DIR/tmp -Xms256m -Xmx512m -XX:+UseParNewGC -XX:+UseConcMarkSweepGC -XX:-CMSConcurrentMTEnabled -XX:CMSInitiatingOccupancyFraction=70 -XX:+CMSParallelRemarkEnabled -Dwork.dir=${WORK_DIR}"
				CLASS_PATH=" -classpath "$(echo ${WORK_DIR}lib/*.jar|sed 's/ /:/g')
				#CLASS_PATH=" -Djava.ext.dirs=lib "
				
				# �޸ĳ��Լ���������
				CLASS=com.aotain.serviceapi.server.ServiceapiServerApplication
				# springboot��������ļ�·��
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
	
	