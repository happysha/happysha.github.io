---
author: bluishoul
comments: true
date: 2012-12-24 15:58:58+00:00
layout: post
slug: my-first-blood-of-nodejs
title: Node.JS／SeaJS 初体验
wordpress_id: 480
categories:
- 一周一博
- 程序开发
tags:
- git
- nodejs
- seajs
---

做前端开发的童鞋对 JavaScript 肯定一点都不陌生，但是你是否听说过服务器端也能跑 JavaScript ，半年前听说 [NodeJS](http://nodejs.org/) 后觉得很神奇，就像最初接触 Java 的时候知道 Java 能桌面、Web 和 移动开发，顿觉碉堡。

但是那时候 JavaScript 基础还不是很好，所以没有好好地接触 [NodeJS](http://nodejs.org) ，最近才开始认真玩起来，同时，[OSC ](http://oschina.net) 的新项目考虑使用 [SeaJS](http://www.oschina.net/p/seajs) 来进行模块化设计，下文将粗略地说明如何利用 NodeJS 和 SeaJS 进行简单的模块化设计，其中也会用到 Git 这个版本控制工具，我也会简单地说明。

![](http://nodejs.org/images/logo.png)

**1、NodeJS 的基本认识和使用**

NodeJS 是服务器端运行的 JavaScript ，使用 google 的 [V8](https://github.com/v8/v8) 作为引擎。

通过以下步骤即能运行 NodeJS



	
  * 安装 NodeJS ：前往 [http://nodejs.org/download/ ](http://nodejs.org/download/ )下载试用你当前平台的 NodeJS，安装很简单，几步搞定

	
  * 安装后最好重启一下，以便环境变量起效。

	
  * 打开命令行或shell下运行命令：node -v ,若看到版本信息，则证明安装好了


然后我们可以新建一个 js 文件，命名为 server.js,代码如下：


以 utf-8 编码保存好后，cd 到当前文件目录，在命令行或 shell 中执行命令：node server.js，即可看到输出如下 log：

server start up at [http://localhost:8080](http://localhost:8080)

然后在 server.js **同目录**下建立 index.html 文件，在其中写入任意的 HTML 代码，保存为 utf-8 编码格式。

最后，在浏览器中打开 [http://localhost:8080](http://localhost:8080) ，即可看到刚才你所写的 HTML 文档内容，再命令行或者shell中会看到有日志输出。

至于如何书写 NodeJS 代码，可以参考前面的 server.js 代码及[官方 API 文档](http://nodejs.org/api/)即可。

**2、Git 的基本使用**

先下载 TortoiseGit：[http://code.google.com/p/tortoisegit/downloads/list](http://code.google.com/p/tortoisegit/downloads/list)

然后安装好后，在命令行/shell下执行 git clone https://github.com/bluishoul/group_modules.git ，将会在当前目录 clone 下文中需要使用的一个 我在 [GitHub](https://github.com/bluishoul/group_modules) 上的项目。

![](http://seajs.org/docs/assets/images/logo.png) **3、SeaJS 的基本认识和使用**

SeaJS 是阿里系的开源项目，是一个适用于 Web 端的模块加载器，能够帮助我们构件模块化的前段或后端的 JavaScript 代码，上文使用Git clone下来的项目就是使用 SeaJS 来构件的。

该项目主要用来构件 OSC 最新项目的各种组件功能。

至于如何写一个简单的 SeaJS 模块，还是官方文档更加好，我也就不费太多口舌了：[http://seajs.org/docs/#quick-start](http://seajs.org/docs/#quick-start)

同样的，你会发现，在你 Clone 的上面的项目文件夹中会有一个 server.js，没错，就是我在 NodJS 的使用中的例子代码，你只需要在该项目目录下执行： node server.js 即可，然后在浏览器中打开 [http://localhost:8080](http://localhost:8080) 就可看到该项目的内容。

用心的同学可以在 Chrome 中 F12 打开调试 ，从 index.html 开始设置断点，然后再是 main.js ，希望你能获得很多。

就写到这里了，写了个大概，需要了解更多的，可以参考 NodeJS 和 SeaJS 的官网 API 文档，这些开源项目都把文档做得很好，而且很活跃，学起来很方便。

