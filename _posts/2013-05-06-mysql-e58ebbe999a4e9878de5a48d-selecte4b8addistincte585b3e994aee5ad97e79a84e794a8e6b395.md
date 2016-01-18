---
author: xiaoT
comments: true
date: 2013-05-06 01:40:19+00:00
layout: post
slug: mysql-%e5%8e%bb%e9%99%a4%e9%87%8d%e5%a4%8d-select%e4%b8%addistinct%e5%85%b3%e9%94%ae%e5%ad%97%e7%9a%84%e7%94%a8%e6%b3%95
title: mysql 去除重复 Select中DISTINCT关键字的用法
wordpress_id: 2053
categories:
- 一周一博
---

项目中一个小bug把我搞晕了好几天，后来就被一个distinct搞定了，下面文章看似简单但是在夺标查询和sql语句组合的时候 就搞的复杂了。

在使用mysql时，有时需要查询出某个字段不重复的记录，虽然mysql提供 有distinct这个关键字来过滤掉多余的重复记录只保留一条，但往往只用它来返回不重复记录的条数，而不是用它来返回不重记录的所有值。其原因是 distinct只能返回它的目标字段，而无法返回其它字段，这个问题让我困扰了很久，用distinct不能解决的话，我只有用二重循环查询来解决，而 这样对于一个数据量非常大的站来说，无疑是会直接影响到效率的。所以我花了很多时间来研究这个问题，网上也查不到解决方案，期间把容容拉来帮忙，结果是我 们两人都郁闷了。。。。。。。。。

下面先来看看例子：

table
id name
1 a
2 b
3 c
4 c
5 b

库结构大概这样，这只是一个简单的例子，实际情况会复杂得多。

比如我想用一条语句查询得到name不重复的所有数据，那就必须使用distinct去掉多余的重复记录。

select distinct name from table
得到的结果是:

name
a
b
c

好像达到效果了，可是，我想要得到的是id值呢？改一下查询语句吧:

select distinct name, id from table

结果会是:

id name
1 a
2 b
3 c
4 c
5 b

distinct怎么没起作用？作用是起了的，不过他同时作用了两个字段，也就是必须得id与name都相同的才会被排除。。。。。。。

我们再改改查询语句:

select id, distinct name from table

很遗憾，除了错误信息你什么也得不到，distinct必须放在开头。难到不能把distinct放到where条件里？能，照样报错。。。。。。。

很麻烦吧？确实，费尽心思都没能解决这个问题。没办法，继续找人问。

拉住公司里一JAVA程序员，他给我演示了oracle里使用distinct之后，也没找到mysql里的解决方案，最后下班之前他建议我试试group by。

试了半天，也不行，最后在mysql手册里找到一个用法，用group_concat(distinct name)配合group by name实现了我所需要的功能，兴奋，天佑我也，赶快试试。

报错。。。。。。。。。。。。郁闷。。。。。。。连mysql手册也跟我过不去，先给了我希望，然后又把我推向失望，好狠哪。。。。

再仔细一查，group_concat函数是4.1支持，晕，我4.0的。没办法，升级，升完级一试，成功。。。。。。

终于搞定了，不过这样一来，又必须要求客户也升级了。

突然灵机一闪，既然可以使用group_concat函数，那其它函数能行吗？

赶紧用count函数一试，成功，我。。。。。。。想哭啊，费了这么多工夫。。。。。。。。原来就这么简单。。。。。。

现在将完整语句放出:

select *, count(distinct name) from table group by name

结果:

id name count(distinct name)
1 a 1
2 b 1
3 c 1

最后一项是多余的，不用管就行了，目的达到。。。。。

唉，原来mysql这么笨，轻轻一下就把他骗过去了，郁闷也就我吧（对了，还有容容那家伙），现在拿出来希望大家不要被这问题折腾。

哦，对，再顺便说一句，group by 必须放在 order by 和 limit之前，不然会报错。。。。。。。。！OK了
