---
author: xiaoT
comments: true
date: 2013-04-01 07:24:45+00:00
layout: post
slug: axis2%e5%88%9b%e5%bb%baweb-service%ef%bc%88%e4%b8%89%ef%bc%89
title: axis2创建web service（三）
wordpress_id: 1346
categories:
- 一周一博
---

### axis2创建web service（三）


这节我们就来写一个客户端来调用一下这个服务。主要关注一下如何用elispe的axis2的插件来生成stub代码。

1.在eclispe 的package Explorer 中点击右键，在菜单中选择新建--->other...----->Axis2 Code Generator

![](http://deltaj.iteye.com/upload/attachment/56345/0533bc95-52fa-3ec1-9e5d-a65cd8e80464.jpg)
2.点击next，进入下一个页面，选择从wsdl文件来产生java文件。
![](http://deltaj.iteye.com/upload/attachment/56360/ebc74115-e99b-3587-a0c4-0b662f0d7603.jpg)
3. 点击next，然后选择wsdl文件，注意此处要填写上一节我们
![](http://deltaj.iteye.com/upload/attachment/56364/a8bdd2d5-b6db-3b16-a49d-e86968e07158.jpg)

4.点击next，进入设置页面，这里我们就用默认的设置。
![](http://deltaj.iteye.com/upload/attachment/56369/a4e9d6ea-70a6-317c-9032-5c9e664a02ed.jpg)
5. 点击next，选择输出文件的路径。
![](http://deltaj.iteye.com/upload/attachment/56377/2a940696-f148-3e85-9e32-173d34d8a044.jpg)
6.点击next，如果看到这个页面，恭喜你已经生成代码成功。
![](http://deltaj.iteye.com/upload/attachment/56366/fffcbf1d-89ee-3272-9e3e-a520bfefb0ec.jpg)
7.在package Explorer中刷新一下项目，然后你发现出现2个新的文件SimpleServerStub和SimpleServerCallbackHandler 。打开SimpleServerStub你会惊喜的发现。著名的小红叉一个接一个的

这是因为没有axis2的类包。我们可以在下载的axis2-1.4.1-bin中找到lib包，把其中的jar都加入我们的工程中。

然后重新编译一下工程，这时我们发现SimpleServerStub还是有几个小红叉。这个是因为这个插件有个小bug。

生成的代码没有实现序列化方法。我们可以自己来加上，在小红叉上点一下，弹出一个小菜单，选择

Add unimplemented methods .
![](http://deltaj.iteye.com/upload/attachment/56387/6eb814ae-c316-3c8c-9b4b-8941e87f3c2e.jpg)
8.








Java代码  ![收藏代码](http://deltaj.iteye.com/images/icon_star.png)








	
  1. /**

	
  2.  * 调用发布的服务。

	
  3.  *

	
  4.  */

	
  5. public class SimpleClient {

	
  6. 
	
  7.  public static void main(String[] args) throws Exception{

	
  8. 
	
  9.   //初始化桩文件

	
  10.   SimpleServerStub stub = new SimpleServerStub();

	
  11.   //初始化SimpleMethod方法。

	
  12.   SimpleServerStub.SimpleMethod request = new  SimpleServerStub.SimpleMethod();

	
  13.   //调用simpleMethod的setName方法。

	
  14.   request.setName("zt");

	
  15.   //

	
  16.   System.out.println(stub.simpleMethod(request).get_return());

	
  17. 
	
  18. 
	
  19.  }

	
  20. }





如果一切正常，你就会看到结果

log4j:WARN No appenders could be found for logger (org.apache.axis2.description.AxisService).
log4j:WARN Please initialize the log4j system properly.
ztSay this is a Simple method ^-^。

调用服务成功。这是个简单的例子，下节我们再做一个复杂一点的例子，来更好的学习axis2
