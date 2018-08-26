# 3 使用JdbcReaml连接数据库

## 3.1 创建数据库表结构

	CREATE DATABASE shiro;

	USE shiro;

	DROP TABLE IF EXISTS `users`;

	CREATE TABLE users (
	  	`id` bigint(20) NOT NULL AUTO_INCREMENT COMMENT '主键',
	  	`username` varchar(40) DEFAULT NULL COMMENT '用户名',
	  	`password` varchar(40) DEFAULT NULL COMMENT '密码',
	  	PRIMARY KEY (`id`)
	) ENGINE=InnoDB AUTO_INCREMENT=5 DEFAULT CHARSET=utf8;

	insert  into `users`(`id`,`username`,`password`) values 
		(1,'marshal','123456'),
		(2,'wangyi','123456'),
		(3,'wangxiaoshan','123456'),
		(4,'wangxiaoli','123456');

## 3.2 配置pom.xml文件

	<?xml version="1.0" encoding="UTF-8"?>
	<project xmlns="http://maven.apache.org/POM/4.0.0"
	         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	    <modelVersion>4.0.0</modelVersion>
	
	    <groupId>com.marshal.shiro</groupId>
        <artifactId>jdbcreaml</artifactId>
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
	
	        <dependency>
	            <groupId>com.alibaba</groupId>
	            <artifactId>druid</artifactId>
	            <version>1.1.10</version>
	        </dependency>
	
	        <dependency>
	            <groupId>commons-logging</groupId>
	            <artifactId>commons-logging</artifactId>
	            <version>1.2</version>
	        </dependency>
	
	        <dependency>
	            <groupId>mysql</groupId>
	            <artifactId>mysql-connector-java</artifactId>
	            <version>5.1.37</version>
	        </dependency>
	    </dependencies>
	
	</project>

## 3.3 编写jdbc_realm.ini文件

	jdbcRealm=org.apache.shiro.realm.jdbc.JdbcRealm
	dataSource=com.alibaba.druid.pool.DruidDataSource
	
	dataSource.driverClassName=com.mysql.jdbc.Driver
	dataSource.url=jdbc:mysql:///shiro
	dataSource.username=root
	dataSource.password=root
	
	jdbcRealm.dataSource=$dataSource
	securityManager.realms=$jdbcRealm

## 3.4 在包com.marshal.shiro.jdbcrealm中创建类ShiroDemo2.java

	package com.marshal.shiro.jdbcrealm;
	
	import org.apache.shiro.SecurityUtils;
	import org.apache.shiro.authc.AuthenticationException;
	import org.apache.shiro.authc.UsernamePasswordToken;
	import org.apache.shiro.config.IniSecurityManagerFactory;
	import org.apache.shiro.mgt.SecurityManager;
	import org.apache.shiro.subject.Subject;
	import org.apache.shiro.util.Factory;
	
	public class ShiroDemo2 {
	
	    public static void main(String[] args) {
	
	        //找资源：ctrl+shift+n
	        //核心类:SecurityManager
	        Factory<SecurityManager> factory = new IniSecurityManagerFactory("classpath:jdbc_realm.ini");
	        SecurityManager securityManager = factory.getInstance();
	
	        //当前用户Subject
	        SecurityUtils.setSecurityManager(securityManager);
	        Subject user = SecurityUtils.getSubject();
	
	        //模拟用户输入用户名与密码
	        UsernamePasswordToken token = new UsernamePasswordToken("lisi","123456");
	        try {
	            user.login(token);
	            System.out.println("登录成功");
	        } catch (AuthenticationException e) {
	            System.out.println("登录失败");
	        }
	    }
	}

## 3.5 测试运行结果


