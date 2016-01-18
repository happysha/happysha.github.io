---
author: bluishoul
comments: true
date: 2013-05-31 16:40:52+00:00
layout: post
slug: how-to-build-a-jquery-slider
title: 从零写一个 jQuery 图片幻灯插件
wordpress_id: 2498
categories:
- 前端/应用开发
tags:
- jQuery
- 插件
---




# 最终效果




[点击查看最终效果](http://live.qhee.com/home)


![](/wp-content/uploads/2013/05/album-slider-2.gif)



# 1、基础版本




顾名思义，基础版（[点击查看 Demo 预览](http://runjs.cn/detail/uxlkduol)），只有最基本的 Slider 的要求（[点击查看源码](http://runjs.cn/code/uxlkduol)）:





	
  1. 能够放置多个预览图片

	
  2. 能够向前或向后切换

	
  3. 切换到最后一张时，滚动到第一张

	
  4. 兼容性：IE7及以上,Chrome,Safari,Firefox

	
  5. jQuery依赖：jQuery 1.4.4 以上




## 演示效果：





## 源代码：





# 2、中级版本





中级版本开始使用标准的 jQuery 插件方式编码，没有写过 **jQuery** 插件的同学看完下面的例子应该能够写写小插件了。中级版本添加了如下功能：






	
  1. 采用 jQuery 插件方式编码

	
  2. 能够放置任意多的图片，wrapper 宽度自动计算

	
  3. 在鼠标移至 wrapper 的对应的 左边50% 和 右边50% 位置 “上一张”、“下一张” 按钮才出现

	
  4. 自动播放，以及设置打开或关闭自动播放




## 演示效果：





## 源代码：




### [源码过长，点击查看/隐藏源代码](javascript:$(".code_2").toggle();)











# 3、高级版本




高级版本 也将采用 jQuery 插件方式编码，将添加以下新特性：





	
  1. 添加查看 全部图片视图

	
  2. 添加同页面多个 slider 支持

	
  3. 添加查看 原图 以及 分享 功能




## 弄了四个小时了，休息会儿，广告之后马上回来~




---------------------华丽的分割线-------------------------




## 演示效果：





## 源代码：




### [源码过长，点击查看/隐藏源代码](javascript:$(".code_3").toggle();)







