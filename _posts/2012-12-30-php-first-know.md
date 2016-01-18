---
author: kone
comments: true
date: 2012-12-30 16:44:41+00:00
layout: post
slug: php-first-know
title: PHP初探
wordpress_id: 694
categories:
- 一周一博
---

    当你看到这个标题的时候，也许你会诧异吧！PHP？确定不是Java，确定没看错？当然没看错，我也莫名其妙，怎么突然就PHP了，连Java都是一知半解的时候，怎么突然学起来PHP了。好吧，这其实都是Boss的主意，Boss突然告诉我要我去做PHP，心想有机会多学习一门语言也不错，于是就答应了。然后就开始了稀里糊涂的PHP之旅。
PHP英文全称Personal Home Page，很奇怪吧，PHP有全称，以前我们学C、C++、Java、Javascript、都没听过谁有全称。看来PHP是一门有故事的语言啊。据说是一个叫Rasmus Lerdorf的人一开始是为了统计自己简历的阅览人数而写的脚本，没想到发展成一门如此强大的语言，IT世界永远不乏故事啊。
学习一门语言的最开始，当然是搭建开发环境，这对于一个新手来说总是会碰到各种问题。因为是在window平台下，所以一开始还是在搭建windows下的开发环境。还好PHP有一个集成Apsache+Mysql+PHP的开发环境wamp，下载地址在http://www.wampserver.com/en/，Wamp包括Apache Http服务器，Mysql数据库，PHP开发环境于一身，而且已经完成PHP和Apache的关联。当然，作为一个刚接触的人，不能依赖于这种集成的开发环境，最好能自己明白搭建这种开发环境的具体做法，自己亲身实践过才行。
于是我把wamp先卸载了， 在网上下载了apache和PHP的安装文件，在本地安装好之后，首先在Apache安装目录下找到/conf/httpd.conf，打开httpd.conf一眼可以看出这是Apache的配置文件，里面应该会包含Apache服务器的各项参数。首先找到Global Environment节最后的LoadModule条目下。在条目下添加如下配置：
LoadModule php_module c:/php/php5apache2_2.dll
AddType application/x-httpd-php  .php
PHPIniDir "D:\kone\PHP\wamp\bin\php\php5.3.13"
其中LoadModule php_module对应文件应该是安装的PHP目录下的php跟apache的dll文件，需要保持跟apache'的版本一致，从他的命名可以看出，关联的版本。否则会导致Apache服务器启动失败。 AddType是将一个MIME类型绑定到某个或者某些扩展名上。如果有多个扩展名，需要用空格分隔开来。PHPInidir是你的PHP安装目录。
下面就可以测试是否安装成功。
在apache下的htdos目录下新建一个indexphp文件。
文件内容是：
<?php
phpinfo()
?>
然后在浏览器中访问http://localhost/下面会打印出如下内容。
![图片](http://b262.photo.store.qq.com/psb?/30d6546d-5347-42ec-abc9-5785b269b4ed/unmLOajwYCeTt7GXJOPsjiYkVQLtz02AM1W7KcoUxY0!/b/dGE2M5ylXwAA&bo=YgKpAgAAAAADAO4!)
从展示的信息应该可以看出，这是PHP安装之后的一些信息。如此说明安装环境搭建完成。
了解一门语言，最基本的就是了解其语法特点。
PHP作为一门脚本语言，它的界定语法是以<?php开头，以?>结束。还可以使用短标签的方式<? 代码 ?>，这样看起来是不是有点像Java的JSP的<% %>，但是开启这个功能需要启用PHP的short_php_tag指令。这个可以在PHP的配置文件中修改它，这个暂且放开不说。还有一种就是可以使用类似Javascript在HTML中的定义一样<script language="php">代码</script>。好吧，其实PHP也可以使用类似JSP的<%%>标签。也许你会奇怪，PHP为什么要使用这些标签，当然，毫无疑问，PHP作为一门脚本语言，需要在HTML中嵌套PHP的代码执行，使用这些标签就可以很方便的区分开HTML标签和PHP代码。
好吧，说了这么多了，我想要在PHP中打印出一串字符怎么办？当然，PHP提供了非常强大的打印输出函数，调用这些函数就可以了，答应输出有print(),echo() sprintf()等。
如<?php
echo "hello world<br>";
print  "hello world<br>";




            sprintf  "hello world<br>";




        ?>
它会在页面上打印二行hello world出来。 分别使用不同的函数，但是打印的效果是一样的。也许你会奇怪为什么第三个没有打印hello world。其实第三个是将输出赋值给一个字符串，而不是直接呈现到浏览器上的。这几个函数的具体使用在慢慢学习之后会更加深入的了解。
好了先了解到这里吧，下面将简单介绍下PHP的基本数据类型等。
