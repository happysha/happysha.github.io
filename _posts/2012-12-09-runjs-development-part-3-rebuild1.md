---
author: bluishoul
comments: true
date: 2012-12-09 09:53:41+00:00
layout: post
slug: runjs-development-part-3-rebuild1
title: RUNJS 开发经验分享 之 重构（模块化）
wordpress_id: 281
categories:
- 前端/应用开发
- 程序开发
tags:
- runjs
- 多图
- 重构
---

这一部分我将搭配着我的设计原型和实际实现来给大家介绍，RunJS 是如何重构的~

一、如图(1) ,该图是 RunJS 重构的整体设计原型

RunJS 重构：

1、模块化：谁显示，谁负责事件处理

2、全站ajax，无刷新

3、dialog 统一管理，使用更方便

4、流程化设计，使用 switch case 模拟流程控制，以及使用事件栈

5、消息提醒（放于 head 中间位置？）

6、可扩展的设置页面（类似于 eclipse）

7、使用向导（对某一功能详细生动的介绍）

![重构总体设计原型](/wp-content/uploads/2012/12/IMG_0186.jpg)

**模块化（见图2）**：



	
  * **Menu**：RunJS 顶部**紫色**范围，主要有编辑器的快捷操作，以及系统功能

	
  * **Toolbar**：RunJS Menu下的一长条，**绿色**部分，主要是服务于其下的 Editor 的，比如自动引库功能以及功能开关等

	
  * **Explorer**：RunJS 左边的**橘色**部分，相当于 Eclipse 中的资源管理器，主要用来显示和管理用户的代码，以及资源文件

	
  * **Editor**：RunJS 最核心的一部分，是由 [**CodeMirror** ](http://codemirror.net/)打造而成，占据位置最大，**蓝色**部分，负责代码编辑、高亮、实时预览等强大功能

	
  * **RunJS**：该模块并不能在视觉上有所体现，而是起到一个聚合的模块，通过它管理其他各个模块间的相互调用




![RunJs 视觉分块](/wp-content/uploads/2012/12/runjs_rebuild_constructure.jpg)以上的视觉分块在第一版本中就已经存在，但是在功能实现上并没有真正的分离，如上一部分博文所说的，抽象的得很简单，于是，此次重构从视觉上分块，将其模块化为四部分，每一部分相互独立，然后通过 RunJS模块 来相互调用其他模块的接口。







**模块设计（如下面的代码）**：




Menu:








	
  * initView/initEvents：初始化视图、事件绑定

	
  * Events：事件统一定义

	
  * Private Functions/Prototype：私有方法和Prototype扩展的方法（相当于公有方法）







具体实现请看下面代码，我作了详细的注释，就不一条条再解释了，有任何问题，请在下面给我留言，我会在之后补上解释。



