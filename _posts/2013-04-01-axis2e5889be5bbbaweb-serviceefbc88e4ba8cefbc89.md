---
author: xiaoT
comments: true
date: 2013-04-01 07:23:22+00:00
layout: post
slug: axis2%e5%88%9b%e5%bb%baweb-service%ef%bc%88%e4%ba%8c%ef%bc%89
title: axis2创建web service（二）
wordpress_id: 1344
categories:
- 一周一博
---

**axis2创建web service（二）**

工具都已经准备齐全了。我们来动手做一个小例子来小试牛刀！

这一节我们先利用axis2来发布一个web service 的服务，然后在下一节我们做一客户端来调用这个服务。

我们的服务很简单的，就是输入一个字符串，然后打印出一段字符串。

代码很简单，主要是测试用。








Java代码








	
  1. package com.deltaj.server;

	
  2. 
	
  3. public class SimpleServer {

	
  4. 
	
  5.     /**

	
  6.      * 简单的测试方法

	
  7.      *

	
  8.      */

	
  9.     public String simpleMethod(String name) {

	
  10.         return name + "Say this is a Simple method ^-^";

	
  11.     }

	
  12. 
	
  13. }





主要的过程就是如何利用axis2的eclispe插件来发布这个服务啦。

1。在eclispe 的package Explorer 中点击右键，在菜单中选择新建--->other...----->Axis2 Service Archiver
![](http://deltaj.iteye.com/upload/attachment/55872/b54ed5f9-2ce8-3c4f-ba3f-52344546bded.jpg)

2.然后点击next进入了类选择页面，在这个页面中的Class File Location选择框中选择类所在的文件夹。
![](http://deltaj.iteye.com/upload/attachment/55874/a56ec7ad-88e6-3cf8-8c9f-42c15ca2e74a.jpg)
3.点击next之后进入了选择 wsdl文件，这里我们选择skip wsdl。
![](http://deltaj.iteye.com/upload/attachment/55887/620647d0-c388-3ba1-9551-d84d67776b8f.jpg)

4. 点击next之后，进入的是选择jar文件的页面，这里我们没有外部的jar，所以点击next直接跳过这个页面。
![](http://deltaj.iteye.com/upload/attachment/55880/6885b10f-8f52-3e30-b81e-b873367b281a.jpg)
4.点击next之后，进入的是选择xml页面，这里我们选择的是自动生成xml，也就是勾选

Generate the service xml automatically这一项
![](http://deltaj.iteye.com/upload/attachment/55884/b5c4f691-2adc-3852-89b3-c577f48fff96.jpg)
5.点击next之后，进入的是生成xml文件的页面，在service name 里填写这个服务所起的名字，这里我起名为simpleServer,然后在class name 中填写要发布的类，这里一定要写全路径，写好后就可以点击load 按钮，

如果一切ok的话，你会看到如下画面
![](http://deltaj.iteye.com/upload/attachment/55894/7d2a98bb-4329-3958-9f3a-040b5e565f9a.jpg)
6 点击next 后，进入的是输出artiver文件的页面，先要在output File location 中选择要输出的路径，

在output  File Name中输入artiver文件的名称。我起的名字是simpleServer
![](http://deltaj.iteye.com/upload/attachment/55898/585ac20d-29bb-3ac6-83af-7aa3515f548f.jpg)
7.点击finish ，如果看到如下的画面，恭喜你，服务发布成功啦。
![](http://deltaj.iteye.com/upload/attachment/55910/cfbcdac8-3d5d-35b1-a438-9ebdd32e8c15.jpg)

8.接下来，我们就可以把这个aar文件放入tomcat中发布，首先把生成的aar文件拷贝到tomcat目录中的axis2项目的service目录中位置如图。
![](http://deltaj.iteye.com/upload/attachment/55912/8c710f5c-11ec-3b13-b878-5be6fb0a6138.jpg)
9.接下来启动tomcat，在地址栏中输入[http://localhost:8080/axis2](http://localhost:8080/axis2) ,你会看到axis2的欢迎画面
![](http://deltaj.iteye.com/upload/attachment/55916/134ae492-6626-3522-839d-0246f1aad2e5.jpg)
10.点击Service连接，你会看到发布的服务列表。这里面就能看到我们发布的simpleService
![](http://deltaj.iteye.com/upload/attachment/55920/7cdacb38-1815-32eb-9723-c3b9fd0c3443.jpg)
11.点击我们的服务simpleServer的连接，我们会看到。至此，服务发布成功。
![](http://deltaj.iteye.com/upload/attachment/55922/f1132cbb-3bb8-3831-a095-3e1e3cd5a98a.jpg)
