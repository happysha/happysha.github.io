---
author: xiaoT
comments: true
date: 2013-04-01 07:20:35+00:00
layout: post
slug: axis2%e5%88%9b%e5%bb%baweb-service%ef%bc%88%e4%b8%80%ef%bc%89
title: axis2创建web service（一）
wordpress_id: 1342
categories:
- 一周一博
---

** axis2创建web service（一）**

**                                             **

axis2 是新一代的web service开发工具，它会让你的web service开发变得轻松，快捷。下面让我们以一个实际的例子来体验一下。

首先，工欲善其事，必先利其器。就让我们先做好一些必备的准备工作吧。

1.下载axis2 的2进制的包和war,现在的最新版本是1.4.1 发布时间是2008-8-25

地址分别是：[http://apache.mirror.phpchina.com/ws/axis2/1_4_1/axis2-1.4.1-bin.zip](http://apache.mirror.phpchina.com/ws/axis2/1_4_1/axis2-1.4.1-bin.zip)

[http://apache.mirror.phpchina.com/ws/axis2/1_4_1/axis2-1.4.1-war.zip](http://apache.mirror.phpchina.com/ws/axis2/1_4_1/axis2-1.4.1-war.zip)

2.把下载后的war放入tomcat的webapps目录里，然后启动tomcat，这样war包就会自动解压为目录axis2

在浏览器中输入[http://localhost:8080/axis2/](http://localhost:8080/axis2/) ，如果一切正常你会看到下面的画面

![](http://deltaj.iteye.com/upload/attachment/55067/037b1dca-5361-3e0c-af18-372bff9419f4.jpg)

3，就开始准备一下axis2的eclispe的插件了。axis2的eclispe插件分为2个，一个是帮助我们生成aar文件的，另一个是帮我们用wsdl文件生成stub代码的。

下载地址是

[http://www.apache.org/dyn/mirrors/mirrors.cgi/ws/axis2/tools/1_4_1/axis2-eclipse-service-archiver-wizard.zip](http://www.apache.org/dyn/mirrors/mirrors.cgi/ws/axis2/tools/1_4_1/axis2-eclipse-service-archiver-wizard.zip)

[http://www.apache.org/dyn/mirrors/mirrors.cgi/ws/axis2/tools/1_4_1/axis2-eclipse-codegen-wizard.zip](http://www.apache.org/dyn/mirrors/mirrors.cgi/ws/axis2/tools/1_4_1/axis2-eclipse-codegen-wizard.zip)

下载完2个压缩文件后，可以直接把解压后的文件拷贝到plugins目录中，也可以在links目录中写文件路径的方式来安装插件，安装完插件后，打开eclipse，在package explorer 中点击右键--->选择new---->other

如果安装正确你会看到
![](http://deltaj.iteye.com/upload/attachment/55065/3c283216-1185-3f9d-8e10-582c478b5019.jpg)
这样准备工作就都做好了。接下来就是正式开发了。

开发的过程，下回分解。。。。。
