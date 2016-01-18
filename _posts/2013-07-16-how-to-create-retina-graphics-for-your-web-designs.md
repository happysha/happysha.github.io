---
author: happysha
comments: true
date: 2013-07-16 05:32:32+00:00
layout: post
slug: how-to-create-retina-graphics-for-your-web-designs
title: 【转】Web设计师如何制作Retina图像
wordpress_id: 2784
categories:
- 前端/应用开发
- 设计
- 转载
tags:
- retina
---

苹果公司发布了更多的产品适应Retina屏幕。到目前为止，我们知道苹果设备中支持Retina屏幕技术的有“iPhone”、“iPod”、“iPad”和“Macbook Pro”，这些设备能为用户呈现更细腻、平滑和高质量的图片效果，提高了用户的视觉体验。做为一名Web设计师如何为你的网站创建这些适合Retina显屏设备的图片呢？这就是我们今天要学的一个东东。


#### 为什么要支持Retina显示


![Web设计师如何制作Retina图像](http://www.w3cplus.com/sites/default/files/styles/print_image/public/blogs/201212/retinaGraphics.jpg)

最初我并期望采用较大的图片来满足Retina屏幕显示采用巨大的图像，因为他毕竟是一个全新的技术。但后来我花了点时间做了一个统计，才意识到苹果的设置占据了很多移动端的份额，这些设备大多数是“iPhone”、“iPod”和"iPad",而且这些设备都支持Retina屏幕技术。大部分使用13、15寸Retina显示屏的用户都通过”Chrome“、”Firefox“、”Safari“和”IE“上网，如果你需要支持”Opera“浏览器，那是你在迎合一些小众用户。（我自己的网站统计数据，就是这样的一个情况）


#### 如何创建Retina图像


![Web设计师如何制作Retina图像](http://www.w3cplus.com/sites/default/files/styles/print_image/public/blogs/201212/retinaGraphics2.jpg)

你可能为认为，Retina图像只需要使用高分辨率（PPI）来保存就可以，但事实并不是如此。所有你需要做的是为Retina显屏保存放大两倍的中图片，比如说你保存一张200x200像素（css像素）的图生，你需要将图片保存成400x400像素。这些超大型的图像显示成原始图像的大小尺寸，有助于在Retina屏幕上创建光滑和清爽的外观效果。

听起来很简单，那你要怎么获取双倍大小的图像呢？

**使用Illustrator设计Logo和Icon图标**

![Web设计师如何制作Retina图像](http://www.w3cplus.com/sites/default/files/styles/print_image/public/blogs/201212/retinaGraphics3.jpg)

矢量图是创建Retina图像的完美解决方案。如果你有一个Logo或ICON是EPS或者Ai文件，在导出或者复制图片到Photoshop时，矢量图它能够扩展到任何尺寸大小。粘贴的元素可以作为一个智能对象，经将保留其矢量路径，因此他可以翻一番，导了出来，作为适合Retina的一个特殊图像。

**使用Photoshop的矢量特性**

![Web设计师如何制作Retina图像](http://www.w3cplus.com/sites/default/files/styles/print_image/public/blogs/201212/retinaGraphics4.jpg)

Photoshop是一个像素图形的应用软件，但这并不意味着他不具有制作矢量图形的特性。每一个图形工具都可以创建一个矢量层，而不仅仅是像素层，这样一来所有图层样式效果依然可以伸缩的。如果你把元素都乘以2，所有的效果几乎都能精确的放大两倍大小。

**扩大你的像素图像**

![Web设计师如何制作Retina图像](http://www.w3cplus.com/sites/default/files/styles/print_image/public/blogs/201212/retinaGraphics5.jpg)

其中有一条规则，作为设计师的我们不想轻意的去扩大一个图像，但是如果想回去给已经你设计的网站添加Retina屏幕显示的图像，而且你也不想手动的去重新创建每个图像。通常扩展一个图像会层致一个模糊和锯齿点状，但是有一个小选项在Photoshop的图像有一个菜单选择"Neares Neighbor",这样就可以勉强帮你避免模糊的外观和大量的锯齿,这样图像就可以用了。在元素还没有加载完时，他不会加载进来，但是他提供了一个晳时的替换

**设计在200%，然后是缩小？**

![Web设计师如何制作Retina图像](http://www.w3cplus.com/sites/default/files/styles/print_image/public/blogs/201212/retinaGraphics6.jpg)

你可能会想，我为什么不能创建一个两倍大小的Web布局页面，这样我就可以缩小元素来创建需要的图标。在传统的印刷设计理论中是可行的，但是在Web设计中是不行的。因为Web设计是工作在一个像素的基础上，用来创造完美的形状和线条。就算是我们按一定的比例绽放图片，然后通过Photoshop软件导出来，那么导出来 的图片也是一个外表模糊的，特别是小图标的时候。


#### 如何代码控制Retina图像


一旦你创建了一个标准图片的副本，而且这个副本是标准图片大小的两倍像素，那么你就可以使用不同的方法把他们加载到你的页面中。这里有一个快速对文件命名的方法，把标准图片和Retina屏幕下图片放在一个相同的文件目录下，并且Retina下图片命名的方式是在普通图像的文件名的末尾上加个”**@2x**“，比如说普通图像文件名是”snarf.jpg“，在Retina下我们就把图像另外命名为”[snarf@2x.jpg](mailto:snarf@2x.jpg)“。

**简单的javascript方法**

    
    <script src="js/retina.js"></script>


绝对简单的方法，就是使用[retina.js](http://retinajs.com/)脚本来控制调用Retina图像。简单点说，[retina.js](http://retinajs.com/)会自动检查你图片目录中的”@2x“图像，然后在Retina设备下替换普通的图片。

**CSS修改方法**

    
    @media only screen and (-webkit-min-device-pixel-ratio: 2), only screen and (min-device-pixel-ratio: 2) {
      header h1 a {
        background-image: url(images/blogspoon-logo@2x.png);
        background-size: 164px 148px;
      }
    }


或者，你可以通过手动修改css文件来控制Retina设备下调用Retina图像。通过媒体查询，如果媒体中条件含有”min-device-pixel-ration：2“,在目标元素上就调用适合Retina设备的图片”@2x“，但是不能忘了结对对应的元素设置”background-size“背景图片的尺寸和常规图片大小一样。

**HTML的img标签**

    
    <img src="images/snarf@2x.jpg" width="300px" height="150px" />


CSS的方法是通过”media queries“来控制元素的背景图片，但是在HTML中可以使用”img“的图片标签，非常的简单，在"img"标签中加载”@2x“图像，然后通过”img“标签的”width“和”height“属性值来缩放图像，以达到普通图像的尺寸。

如需转载烦请注明出处：

英文原文：[http://line25.com/tutorials/how-to-create-retina-graphics-for-your-web-designs](http://line25.com/tutorials/how-to-create-retina-graphics-for-your-web-designs)

中文译文：[http://www.w3cplus.com/css/how-to-create-retina-graphics-for-your-web-designs.html](http://www.w3cplus.com/css/how-to-create-retina-graphics-for-your-web-designs.html)
