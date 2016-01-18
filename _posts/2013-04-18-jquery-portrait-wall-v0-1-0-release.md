---
author: bluishoul
comments: true
date: 2013-04-18 10:41:19+00:00
layout: post
slug: jquery-portrait-wall-v0-1-0-release
title: jQuery 插件 Portrait Wall (肖像墙) v0.1.0 发布
wordpress_id: 1926
categories:
- 前端/应用开发
- 程序开发
tags:
- jQuery
---

# 一、一瞥


_1、2行7列_
![Demo](/wp-content/uploads/2013/04/demo.png)

_2、3行4列_
![Demo2](/wp-content/uploads/2013/04/demo2.png)

_3、[演示地址](http://sandbox.runjs.cn/show/oxynfmff)_

_4、git 库地址：[http://git.oschina.net/bluishoul/portrait-wall](http://git.oschina.net/bluishoul/portrait-wall)_


# 二、如何使用


_1、引入库_

[code lang="html"]
<script type="text/javascript" src="http://runjs.cn/js/sandbox/jquery/jquery-1.8.3.min.js">
</script><script type="text/javascript" src="http://sandbox.runjs.cn/uploads/rs/90/wwourf2n/jquery-portraitwall.js"></script>
[/code]

_2、添加一个div用于显示头像墙_

[code lang="html"]
<div class="portrait-wall">
</div>
[/code]

_3、构建需要显示的头像item_

可利用模版语言在 portrait-wall 中生成，也可以用 Javascript 生成，以下以 Javascript 方式为例：
[code lang="javascript"]
$(function(){
    var item_tpl = '</pre>
<div class="item" id="" title="" data-hashd="1">
<div class="info"><a href="http://www.oschina.net/" target="_blank">OSChina</a></div>
</div>
<pre>
';
    var images = [
        "http://sandbox.runjs.cn/uploads/rs/90/wwourf2n/253224_100.jpg",
        "http://sandbox.runjs.cn/uploads/rs/90/wwourf2n/130291_100.jpg",
        "http://sandbox.runjs.cn/uploads/rs/90/wwourf2n/139572_100.jpg",
        "http://sandbox.runjs.cn/uploads/rs/90/wwourf2n/127735_100.jpg",
        "http://sandbox.runjs.cn/uploads/rs/90/wwourf2n/571282_100.jpg",
        "http://sandbox.runjs.cn/uploads/rs/90/wwourf2n/590093_100.jpg",
        "http://sandbox.runjs.cn/uploads/rs/90/wwourf2n/912704_100.jpg",
        "http://sandbox.runjs.cn/uploads/rs/90/wwourf2n/933828_100.jpg"
    ];
    var hdimages = [
        "http://sandbox.runjs.cn/uploads/rs/90/wwourf2n/89964_200.jpg",
        "http://sandbox.runjs.cn/uploads/rs/90/wwourf2n/89964_200.jpg",
        "http://sandbox.runjs.cn/uploads/rs/90/wwourf2n/89964_200.jpg",
        "http://sandbox.runjs.cn/uploads/rs/90/wwourf2n/89964_200.jpg",
        "http://sandbox.runjs.cn/uploads/rs/90/wwourf2n/89964_200.jpg",
        "http://sandbox.runjs.cn/uploads/rs/90/wwourf2n/89964_200.jpg",
        "http://sandbox.runjs.cn/uploads/rs/90/wwourf2n/89964_200.jpg",
        "http://sandbox.runjs.cn/uploads/rs/90/wwourf2n/89964_200.jpg"
    ];
    //构建items
    var counts = images.length;//图片个数
    var pt = $(".portrait-wall");
    for (var i = 0; i < counts; i++) {
        var item = $(item_tpl);
        item.attr("id", "item" + (i + 1));
        pt.append(item);
        if(i==0){
            item.find(".info").css("bottom","0px");
        }
    }
  //下面启用插件以及配置参数
  *****
});
[/code]

_4、启用 portrait-wall 插件，并配置参数_

[code lang="javascript"]
$(".portrait-wall").portraitwall({
      width: 100,
      height: 100,
      columns: 4,
      rows:3,
      images: images,
      hdimages: hdimages,
      onHDShow:function(item,options){
          $(item).find('.info').animate({
              bottom:0
          });
      },
      onHDClick:function(item,options){

      },
      onNoHDClick:function(item,options){
          var self = $(item).find('.info');
          if(parseInt(self.css("bottom"))==-100){
              self.animate({
                  bottom:0
              });
          }else{
              self.animate({
                  bottom:-100
              });
          }
      },
      css: [
          '.portrait-wall{margin:40px auto;}',
          '.portrait-wall .item{overflow:hidden;}',
          '.portrait-wall .cur{box-shadow:0px 0px 10px rgba(0,0,0,0.2) inset;}',
          '.portrait-wall .info{position:absolute;text-align:center;width:100%;height:100px;bottom:-100px;background-color:rgba(0, 0, 0, .5);;color:#FFF;line-height:100px;}',
          '.portrait-wall .info a{color:#FFF;text-shadow: 2px 2px 1px black;font-size: 14px;}',
          '.portrait-wall .info.show{bottom:0px;}'
      ]
 });
[/code]

_4、1 参数详解_

`width`：小头像宽

`height`：小头像高

_注：_当前只支持宽高相等图片

`columns`：头像显示列数

`rows`：头像显示行数

`images`：小头像图片 `URL` 数组

`hdimages`：高清头像图片 `URL` 数组

`css`：头像墙样式，字符串数组

`onHDShow`：当高清头像显示时被调用，具有两个参数 `item` 为当前显示的 item 节点，`options` 配置参数对 象

`onHDClick`：当高清头像显示后被点击是调用，参数同上

`onNoHDClick`：当没有高清头像的节点被点击时调用，参数同上


# 三、HOW IT WORKS?


_1、根据 位置数 确定占位矩阵_
![](/wp-content/uploads/2013/04/mt1.png)
_2、根据 位置数 确定 值矩阵_
![](/wp-content/uploads/2013/04/mt2.png)
_3、占位矩阵 与 值矩阵转换，然后再按转换后的位置重新计算显示位置:_
转换步骤：
(1) - 根据 v_matrix 矩阵获取对应新的 位置数：getIndexByValue
(2) - 根据 位置数 获取 占位矩阵：getCurMatrix
(3) - 根据 显示位置 重建占位矩阵

如下演示： cur = 15 到 cur = 18 的具体转换：
![](/wp-content/uploads/2013/04/mt3.png)
_4、前一状态 到 当前状态的转换_
![](/wp-content/uploads/2013/04/mt4.png)

根据当前给定位置数获得所占据的显示位（2*2）矩阵 如：cur = 2，columns = 4，rows = 5，返回 [2,3,6,7]
![](/wp-content/uploads/2013/04/mt5.png)

