---
author: xiaoT
comments: true
date: 2013-04-01 07:25:41+00:00
layout: post
slug: axis2%e5%88%9b%e5%bb%baweb-service%ef%bc%88%e5%9b%9b%ef%bc%89
title: axis2创建web service（四）
wordpress_id: 1348
categories:
- 一周一博
---

**axis2创建web service（四）**

上节我们做了一个简单的例子，调用的服务里的方法只是简单返回一个字符串，这次我们要做一个复杂点的例子，调用服务里的方法返回一个java Bean对象。

1. 首先做一个简单的java bean ，代码如下








Java代码  ![收藏代码](http://deltaj.iteye.com/images/icon_star.png)








	
  1. package com.deltaj.server;

	
  2. 
	
  3. public class Persion {

	
  4.     // 姓名

	
  5.     private String name;

	
  6.     // 年龄

	
  7.     private int age;

	
  8. 
	
  9.     public String getName() {

	
  10.         return name;

	
  11.     }

	
  12. 
	
  13.     public void setName(String name) {

	
  14.         this.name = name;

	
  15.     }

	
  16. 
	
  17.     public int getAge() {

	
  18.         return age;

	
  19.     }

	
  20. 
	
  21.     public void setAge(int age) {

	
  22.         this.age = age;

	
  23.     }

	
  24. 
	
  25. }





2.做一个服务，里面只发布一个方面，这个方法返回这个bean。








Java代码  ![收藏代码](http://deltaj.iteye.com/images/icon_star.png)








	
  1. package com.deltaj.server;

	
  2. 
	
  3. public class BeanServer {

	
  4. 
	
  5.     /**

	
  6.      * 简单的测试方法

	
  7.      *

	
  8.      */

	
  9.     public Persion testMethod(String name, int age) {

	
  10.         Persion persion = new Persion();

	
  11.         persion.setName(name);

	
  12.         persion.setAge(age);

	
  13.         return persion;

	
  14.     }

	
  15. }





3.按照第二节的做法，把这个服务发布出来。

4.同样按照第三节的方法，用这个wsdl来生成stub代码。

5.然后我们开始做一个方法来调用一下这个服务。








Java代码  ![收藏代码](http://deltaj.iteye.com/images/icon_star.png)








	
  1. package com.deltaj.client;

	
  2. 
	
  3. import com.deltaj.server.TestServerStub;

	
  4. 
	
  5. public class BeanClient {

	
  6.     public static void main(String[] args) throws Exception{

	
  7.         // 初始化桩文件

	
  8.         TestServerStub stub = new TestServerStub();

	
  9.         // 初始化TestMethod方法。

	
  10.         TestServerStub.TestMethod request = new TestServerStub.TestMethod();

	
  11.         // 设置bean的属性值。

	
  12.         request.setName("delta ");

	
  13.         request.setAge(20);

	
  14.         //

	
  15.         System.out.println("The name is:"+stub.testMethod(request).get_return().getName());

	
  16.         System.out.println("The age is:"+stub.testMethod(request).get_return().getAge());

	
  17.     }

	
  18. 
	
  19. }





6.如果按照这里说的做的话，你会看到

log4j:WARN No appenders could be found for logger (org.apache.axis2.description.AxisService).
log4j:WARN Please initialize the log4j system properly.
The name is:delta
The age is:20

祝你好运。：）
