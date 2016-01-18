---
author: heimi
comments: true
date: 2013-01-13 15:44:09+00:00
layout: post
slug: js-for-my-work
title: js简单设置a标签href属性
wordpress_id: 890
categories:
- 网络运维
---

之前写过一篇文章：**IT民工如何从体力劳动中解放出来**，由于工作性质总是要编写文章，最近又一直在写新闻源，提交的时候txt也就算了，还必需得是html源码。由于平台不同，为了便于统计，点击咨询的超链接必需带上平台的域名以便进行数据统计和分析。例如，如果文章是要发布到news.qq.com，文章的咨询地址如：http://xxx.com/zixun.html?news.qq.com，每天都要发布不同平台，几十个新闻，琢磨了半天还是要提高下效率。

因为之前的文本辅助软件都是自己随意写的，都是一些文本辅助，但是要想一劳永逸还是不能实现。最近从别人的网站跳转代码上看出来点思路，任何web语言应该处理a链接href属性都能搞定，最终还是觉得js比较靠谱，毕竟限制比较小。好吧，js说白了还真不会，百度了下"js获取当前域名"很快找到答案，代码如下：

    
    host = window.location.host;//取得当前页面域名



    
    var url = "http://xxx.com/LR/Chatpre.aspx?id=xxx&lng=cn&p="+host;//设置url来源


接着就是js设置html a标签href属性了。同样，百度会给你一大堆答案，选择最简单的一种吧：

    
    document.getElementById("ccc").href =url;//设置href的值


上面代码简单实现了如何设置id=ccc 的a标签href值。将以上3行代码放到js，ftp上传到可用空间，html代码中调用xxx.com/ccc.js，搞定。具体html代码如下：
<table >
<tbody >
<tr >

<td ><html>
</td>
</tr>
<tr >

<td >
</td>

<td ><body>
</td>
</tr>
<tr >

<td >
</td>

<td ><a id="ccc" target="_blank" style="text-align: center" ><imgheight="71" src="[http://www.zzwcw.com/uploads/allimg/121217/10_121217101329_1.gif](http://www.zzwcw.com/uploads/allimg/121217/10_121217101329_1.gif)"></a>
</td>
</tr>
<tr >

<td >
</td>

<td ><script type="text/javascript" src="[http://www.ｘｘｘ.com/ccc.js](http://www.xiaoguan8.com/ccc.js)"></script>
</td>
</tr>
<tr >

<td >
</td>

<td ></body>
</td>
</tr>
<tr >

<td > </html>
</td>

<td >
</td>
</tr>
</tbody>
</table>
很简单的代码，确给我的工作带来很大的方便，配上自己写的txt辅助程序，很快就可以完成每天修改链接的繁琐工作。苦逼的工作中寻找些许乐趣。

毕竟不擅长代码编写，但是遇到一些问题总是期望能找到好的方法，最直接的方法，我会寻求百度。当然身边这么多技术人才在，也希望技术牛们，能贴上你们的解决办法！
