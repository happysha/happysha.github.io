---
author: kone
comments: true
date: 2013-01-21 05:12:47+00:00
layout: post
slug: controller-in-magent
title: Magento中的Controller
wordpress_id: 991
categories:
- 一周一博
---

Magento也是基于MVC的设计思想,虽然它使用的是Zend的MVC架构,但是还是有它自己的特点在其中.在MVC的架构中,我们总会比较关注我们的请求发送到服务器是交给谁处理的,也就是我们MVC中的C.在PHP中,PHP文件放在服务器中,我们直接通过访问PHP文件可以执行PHP中的代码.不像Java中具有Tomcat这样的容器和Servlet这样的机制.所以,在Magento中是通过一个index.php文件来拦截请求,然后进行请求的路由处理和模型调用.在Magento中index文件会将请求交给Mage::run()函数处理.

Magento将请求交给前端控制器,然后交给路由控制器,最后交给用户控制器处理.至于具体处理细节,需要仔细阅读源码方可知道.

下面将用一个简单的例子来介绍一下Magento的控制器.

首先需要新建一个自己的module,在magento根目录下的app/etc/modules下新建一个以自己模块命名的文件,比如Makingware_Coupon.xml,一般下划线前面使用项目或者公司名,后面使用某一个模块名命名.当然,xml文件内容自然不能为空.在xml文件中进行如下配置.

![1](/wp-content/uploads/2013/01/12.png)



配置标签中Makingware_Coupon根据你命名的module配置文件名一样.其中active表示是否启用这个module,codePool表示该module的代码在哪个文件夹下.加入如下配置之后,在后台点击System->Configuration.在左侧列表的ADVANCED拦中找到advanced,展开Disabled Module Output,可以看到如下

![2](/wp-content/uploads/2013/01/21.png)



说明Magento已经开启你的module了.

接下来就新建一个属于你的控制器吧,当然,首先得建立几个文件夹.在magento的根目录下.

app/code/local/Makingware/Coupon/Block

app/code/local/Makingware/Coupon/controllers

app/code/local/Makingware/Coupon/etc

app/code/local/Makingware/Coupon/Helper

app/code/local/Makingware/Coupon/Model

app/code/local/Makingware/Coupon/sql

在local下新建以module名命名的文件夹,其中Block存放Block文件,这在后续将会介绍到,controllers存放的控制器文件,etc存放的配置文件,Helper存放定义的Helper文件,Model自然就是存放模型文件,sql中存放的是安装magento的时候自定的表安装的时候的安装文件.

我们的控制器自然是放在controllers文件夹下,新建一个CodeController命名的PHP文件,在其中声明一个类名为Makingware_Coupon_CodeController 继承自Mage_Core_Controller_Front_Action,其中类名使用module名+控制器名命名,这样Magento自己会找到该文件夹下的控制器类.下面在Controller中声明一个方法

public function indexAction(){
echo "hello world";
}

方法将输出一个字符串,方法声明之后,怎么样去调用方法呢?不要着急,接下来还需要一点东西才能让我们这个控制器能够使用,在etc下新建一个config.xml文件,config文件以config标签开始.

<config>

....

</config>

在config标签中加入如下结点

![3](/wp-content/uploads/2013/01/31.png)



从结点名可以看出它是标示该config文件属于哪个module,及版本信息.

然后再在config标签下添加一个如下配置：

![4](/wp-content/uploads/2013/01/41.png)



该配置使用<frontend>标签开始，下面是router和layout标签，先暂时只讲router标签,router标签就是一个前端路由配置，<router>标签下有一个叫<coupon>的结点，这个结点使用模块名作为标签名，在此例子中也就Makingware下面的coupon模块,当然你可以用你自己模块作为名称,<use>标签我们暂时不管,使用如上值就可以了，下面在<args>标签下有module和frontName标签，其中module标签使用最开始建立的module名作为值，frontName使用router下的<coupon>作为值.layout标签等讲到布局的时候再介绍。

配置好前端路由控制之后，我们应该怎么样才能访问到控制器呢？Magento的路由控制器url映射规则是使用模块名+控制器名+方法名，从我们新建的控制器类名Makingware_Coupon_CodeController可以看出，模块名应该是coupon,控制器名应该是code（magento会自己根据命名规则找到CodeController）,接下来方法名应该是我们定义的indexAction方法了，不过Magento也会根据命名规则自动将Action加入到方法名中，所以我们的方法名在url中应该是index,从前面就可以得到我们访问该控制器的url应该是coupon/code/index.接下来在浏览器中输入http://localhost/coupon/code/index/就可以访问我们的控制器了，如果浏览器能输出helloworld就说明您的控制器配置成功了.如果没有,那么自己再仔细找找原因或者百度一下吧。






