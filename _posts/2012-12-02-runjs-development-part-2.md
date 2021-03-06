---
author: bluishoul
comments: true
date: 2012-12-02 14:57:36+00:00
layout: post
slug: runjs-development-part-2
title: RunJS 开发经验分享 之 自由与纠结同行
wordpress_id: 193
categories:
- 一周一博
- 程序开发
---

新起一个项目其实是很爽的，至少对我来说是很爽的（Ronny估计看着觉得纠结了），因为我可以从零开始，完全按照自己的想法来构建一个项目，我想要用什么技术，我想要什么效果，我想要使用怎样的编码风格，都由我自己决定，至少在一个大家都不感冒 JavaScript 的小团队里，我可以决定大部分的东西。

我们开始这个项目以后，就分工明确，我负责前端部分，@王振威负责后端（包括Java代码，数据库，服务器配置所有后台的管理，还有负责设计与后端交互的[API](http://runjs.cn/js/api.js)[JavaScript形式]），曾沙负责美工设计。我们三个各司其职，不亦乐乎的开始了。

我没计算进度，每天都按照自己的节奏编码，这样感觉很好，Boss没有给我任何相关的压力，给我很多的空间，可以自己把握，相当的自由，但是我也没有涣散，我知道自己在干什么，自己想要把它做成什么样。

开始设计的时候，就简单的抽象了一下（详细代码可[见此](http://runjs.cn/js/base1.js)），主要模块如下：

1、类RunJS:负责渲染界面

2、类Controls：负责处理页面的逻辑以及交互，其中包括所有的弹窗、流程处理、事件绑定。

3、API：负责与后台交互，比如保存操作等，采用Ajax进行交互

4、Resource：主要是辅助编辑器自动引入的常用的JavaScript库。

看上去分得还挺多，写起来应该还算清楚，从表面上看上去是这样的，类RunJS中的control_event:负责处理所有逻辑、交互，是以json的格式组织的：


var control_event = {




  save : function(callback) {....},




  upload:function(params){....}




}







看上去很清楚？可别被迷惑了，看看这个JSON有多长：1616行，而且调用关系复杂，因为有处理流程的问题，所以有时候会反复相互调用，比如：当你没有项目的时候，将当前代码保存，会提示你创建项目，然后创建项目以后你可以顺利保存；然而，当你正在编辑项目的时候，你想要创建新的项目，但是现在又会去检查编辑状态，确定是不是需要保存，以防止当前编辑的内容丢失，因此会调用保存的代码，这样，如果判断条件控制不好，就会出现相互调用的循环，这样的调用关系很乱也很复杂，流程控制也不够明确和清晰。




为何会有这么长的代码，因为模块化不够才如此，所有的操作看似很有条理，但是东西一多，情况就完全不同了，“量变引起质变”，这句话算是体会到了。




这也是由于设计中太多自由带来的麻烦，不过，也许也是因为经验不足导致，以前很少有机会一次写这么多的JS，而且这些JS完全只服务于一个页面，就像我们学习Java的时候写桌面程序一样，很多业务就在一个dialog里面完成了，所以代码会很多，多了就不好管理了。




所以，我还在没写完这个项目的时候就开始想着重构了，因为，哪怕多加一个很简单的弹窗，我都会觉得很难受，我得从上千行的JS中去寻找我需要调用的函数，而且因为重用性也不够高，所以我总是需要写很多重复的代码来完成类似的功能，或者通过JS来修改一下已有的一些窗口设置，从而达到复用，这样就很复杂了，所有的东西都不够透明和简单，代码复杂，就必定会出问题，简单才是保证高效和稳定的基础。




将近两个月的开发，让我明白了这么一个道理：




  **模块化不是花架子，是能够让代码更加简单、更容易维护、更简单地扩展的有利工具！**




而通常情况是，有时候你根本不知道，你是否需要模块化，因为，你不知道将来你的代码量将会到达怎么样的级别，但是，现在我告诉你，模块化绝对不会是坏事！




关于具体如何重构 RunJS 以及更多的技术细节，我会在今后的连载文章中跟大家分享~敬请关注~
