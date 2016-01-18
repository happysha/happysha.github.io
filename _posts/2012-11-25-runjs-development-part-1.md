---
author: bluishoul
comments: false
date: 2012-11-25 14:20:15+00:00
layout: post
slug: runjs-development-part-1
title: RunJS 开发经验分享 之 前世今生
wordpress_id: 137
categories:
- 一周一博
- 程序开发
tags:
- javascript
- js
- runjs
---

大家都喜欢一部分一部分写，喜欢待续，所以我在第一部分的文字里先大概说一下 [RunJS](http://runjs.cn) 从何而来，这东西是干嘛用的。

从字面意义来看 RunJS 很直观：运行 JavaScript，也就是一个能够运行你的 JavaScript 脚本的网站，这是我加入 [OSChina.NET](http://oschina.net/) 以来做得比较久的一个项目了，这个项目最开始是想替代 OSChina.NET 的另一个项目 [OSCTools.net](http://osctools.net) 中的 [JSBin](http://www.oschina.net/p/jsbin) 工具的，这个工具是我从原官方网站直接把代码弄过来的，然后根据各种前端操作，我们自己写出了对应的后台，但是这个工具没有用户系统，也就是说，没法登录，没法保留用户编辑的代码，只能一次生成一个随机串当作一个代码的标识，用户需要记住这个代码的 URL 才能下次继续访问，这样根本没有太大的用户粘度,而原项目的 [JavaScript](http://www.ostools.net/tools/jsbin/jsbin.js) 脚本特别的复杂（因为所有的 JS 都被压缩成了一个），在它基础上进行二次开发几乎是不可能的，之前在它基础上增加了一点点功能就让我苦不堪言。

后来，我们便考虑着自己写一个，但是因为考虑到这个网站的特殊性：能够在我们的站点上运行任何脚本，在这样的网站上添加用户系统需要面对的最大的问题就是安全问题，我们的项目开发基本上都是在 OSChina.NET 架构代码上构建的，而 OSChina 采用 Cookies 保持用户会话，所以我们首先面对的问题就是如何防止用户的 Cookies 被恶意脚本盗取，一开始就是因为没有找到可行方案而搁置了，但是一个偶然的机会，我们了解到 Cookies 可以通过设置 httponly 使得 JS 无法通过 document.cookie 拿到会话 cookies（[详情请见此](http://www.oschina.net/question/100267_65112) ，[什么是httponly](http://www.oschina.net/question/100267_65116)），这样我们才开始放心的开发了（其实这只不过是我们面对的最基础的一个安全问题）。

一开始，RunJS 就被定位成了一个做前端代码演示的平台，拥有用户系统，但是不保存用户密码（利用 Openid 登录：例如 QQ、微博、Gmail 等第三方帐号登录），能够在线编辑 JavaScript、HTML、CSS 并且能够实施预览代码效果（类似于 Dreamweaver 所见即所得：但是这个比 Dreamweaver 的可见即所得更加准确和真实 ：)），它还有一个资源管理器，用来管理用户所有的代码，还有一点，就是 Fork ：Fork 听得多的一个地方就是 Github 了，Fork 其实就是把别人的代码复制一份，自己接着开发和改造，而复制的代码和原代码之间则有了一种关系：分支，这就是最初的定位和基本功能。

当时，红薯就给我们激动地分析着功能，然后在白板上画下了最初的 UI ，然后当天晚上就有了一原型图，用的啥工具不记得了，不过那工具确实很不错，下次提醒我写上， :lol: 。接下来的两个月，便就是全力投入到开发中，其中的设计细节，我将在下一篇中详细说明，敬请期待，哈哈~~


See you NEXT WEEK!
