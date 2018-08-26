# 2 核心类SecurityManager与Subject

## 2.1 开发前准备

1：使用的开发工具：Intellij IDEA
2：创建Maven项目

## 2.2  配置pom.xml文件

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

## 2.3 编写shiro.ini文件

	[users]
	admin=123456
	wangyi=123456
	wangxiaoshan=123456
	wangxiaoli=123456

## 2.4 在包com.marshal.shiro包下新建类ShiroDemo1.java

	package com.marshal.shiro;
	
	import org.apache.shiro.SecurityUtils;
	import org.apache.shiro.authc.AuthenticationException;
	import org.apache.shiro.authc.UsernamePasswordToken;
	import org.apache.shiro.config.IniSecurityManagerFactory;
	import org.apache.shiro.mgt.SecurityManager;
	import org.apache.shiro.subject.Subject;
	import org.apache.shiro.util.Factory;
	
	public class ShiroDemo1 {
	    public static void main(String[] args) {
	    
	        //SecurutyManager---->Factory
	        Factory<SecurityManager> factory = new IniSecurityManagerFactory("classpath:shiro.ini");
	        
	        //ctrl+alt+v：快速生成变量及对应的数据类型
	        SecurityManager securityManager = factory.getInstance();
	        
	        //当前用户：Subject--->SecurityUtils
	        SecurityUtils.setSecurityManager(securityManager);
	        
	        //当前用户
	        Subject user = SecurityUtils.getSubject();
	        
	        //通过UsernamePasswordToken来模拟html/jsp传递过来的用户名与密码
	        UsernamePasswordToken token = new UsernamePasswordToken("aaa","123456");
	        
	        //通过shiro来判断用户是否登录成功:ctrl+alt+t
	        try {
	            user.login(token);
	            System.out.println("登录成功");
	        } catch (AuthenticationException e) {
	            System.out.println("登录失败");
	        }
	    }
	}

## 2.5 测试程序运行结果

当用户名及验证码正确时

    登录成功

当用户名及验证码错误时

    登录失败