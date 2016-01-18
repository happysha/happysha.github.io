---
author: shmily
comments: true
date: 2012-12-02 14:20:51+00:00
layout: post
slug: character
title: 有关保存文件时的编码选项与html/jsp页面设定字符编码的配置
wordpress_id: 195
categories:
- 一周一博
- 程序开发
---

分两种情况介绍

注：首先，各位得对一次 请求/响应 的流程有基本认识，即：浏览器发出请求--》服务器接收并处理请求--》将html形式的页面返回（响应）给浏览器，一次 请求/响应 完毕！

静态页面（html）：

保存文件时的编码选项(默认为ANSI，中文操作系统ANSI即为GBK)必须得与html页面中的content-Type（即在meta标签中配置的 http-equiv="content-Type"）中的配置的码一致，访问此页面时才不会出现乱码。（若不显示定义meta标签，则默认是meta标 签中给出的是系统ANSI编码，中文操作系统是GBK）








JSP代码








	
  1. <meta http-equiv="content-Type" content="text/html;charset=字符编码">











	
  1. <meta http-equiv="content-Type" content="text/html;charset=字符编码">





原因：web服务器接收到静态请求后（如对html页面的请求），web服务器仅仅是从目录结构中搜索到它，并将它以流的形式返回，而它的编码类型在保存 文件时已经确定了，而上面的meta标签就是告诉浏览器以何种字符编码去解码，所以保存文件时的编码选项必须得与html页面中的content- Type中的配置的字符编码一致。

动态页面（jsp）：

保存文件时的编码选项必须与jsp页面中的pageEncoding属性中配置的编码一致（或者在没有pageEncoding属性时与 contenType属性中配置的编码一致，两者的优先级是：pageEncoding>contentType），才不会出现乱码。








JSP代码








	
  1. <%@page contentType="text/html;charset=字符编码" pageEncoding="字符编码"%>











	
  1. <%@page contentType="text/html;charset=字符编码" pageEncoding="字符编码"%>





原因：web容器会根据pageEncoding中的编码将jsp页面转换成servlet文件（若没有pageEncoding属性，则使用 contentType中的编码将jsp文件转换成servlet），其原理也就是以流的形式读jsp文件，所以保存jsp文件时的编码选项必须与 pageEncoding属性中配置的字符编码一致（或者在没有pageEncoding属性时与contenType属性中配置的编码一致）。而在 servlet中生成html文件时使用的是contentType中配置的编码将html页面以流的形式输出（若没有设置contentType中的 charset则使用的是pageEncoding，此时，与之前不同，它们的优先级是contentType>pageEncoding），浏览 器也会以contentType中的编码（或pageEncoding）来解码（之所以这么说是因为浏览器根据响应头来解码，而他们恰恰改变的是响应 头）。所以contentType中的编码可以与jsp文件保存时的编码选项不同（因为在有pageEncoding属性的情况下，他们之间没有直接联 系，但若没有pageEncoding属性则另当别论，原因上面已经说过）！

这是我做的实验

实验结果：

正常中文

pageEncoding="UTF-8" contentType="text/html; charset=gbk"

以utf-8格式保存的

显示的时候页面编码格式是 gbk





正常中文

pageEncoding="UTF-8"

以utf-8格式保存的

显示的时候页面编码格式是 utf-8



乱码中文

pageEncoding="UTF-8" contentType="text/html; charset=gbk"

以ascii格式保存的

显示的时候页面编码格式是 gbk







乱码中文

pageEncoding="UTF-8"

以asscii格式保存的

显示的时候页面 编码格式 是 utf-8





正常中文

contentType="text/html; charset=gbk"

以ascii格式保存的

显示的时候页面编码格式是gbk





正常中文（这个结果的原因在探索中，估计是utf-8格式包容 ascii格式）

contentType="text/html; charset=gbk"

以ascii格式保存的

显示的时候页面编码格式是gbk

