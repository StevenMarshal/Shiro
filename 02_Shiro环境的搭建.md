# 2 Shiro环境的搭建

1：启动开发工具Intellij IDEA
2：创建Maven项目
3：配置pom.xml文件

	<?xml version="1.0" encoding="UTF-8"?>
	<project xmlns="http://maven.apache.org/POM/4.0.0"
	         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	    
	    <modelVersion>4.0.0</modelVersion>
	
	    <groupId>com.marshal.shiro</groupId>
	    <artifactId>study1</artifactId>
	    <version>1.0-SNAPSHOT</version>
	
	    <dependencies>
	        <dependency>
	            <groupId>org.apache.shiro</groupId>
	            <artifactId>shiro-core</artifactId>
	            <version>1.2.4</version>
	        </dependency>
	
	        <dependency>
	            <groupId>org.slf4j</groupId>
	            <artifactId>slf4j-log4j12</artifactId>
	            <version>1.7.12</version>
	        </dependency>
	    </dependencies>
	
	</project>

4：编写shiro.ini文件

	[users]
	admin=123456
	wangyi=123456
	wangxiaoshan=123456
	wangxiaoli=123456

