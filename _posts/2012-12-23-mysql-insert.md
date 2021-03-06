---
author: kone
comments: true
date: 2012-12-23 06:21:26+00:00
layout: post
slug: mysql-insert
title: Mysql 插入优化
wordpress_id: 429
categories:
- 数据库
- 程序开发
---

在公司做一个小的群发留言的功能时，因为在执行群发留言的时候要对多张表进行大量的插入操作。不说功能的完善性，效率应该是首先需要保证的。数据库是Mysql数据库，数据量在10W级别，因此要对插入操作进行优化。于是看了下Mysql的开发文档，里面提及几点关于Mysql的插入优化操作。自己做了一点点总结。



先了解Mysql影响插入效率的因素：
连接：（3） -   发送查询给服务器：（2） - 解析查询：（2） - 插入记录：（1*记录大小） -插入索引：（1*索引数量） -关闭：（1） 。1、如果同时从同一个客户端插入很多行，使用含多个VALUE的INSERT语句同时插入几行。这比使用单行INSERT语句快(在某些情况下快几倍)。如果你正向一个非空表添加数据，可以调节bulk_insert_buffer_size变量，使数据插入更快。以上是Mysql文档中的描述，以往我们执行插入操作的时候，使用的都是insert table（column） values（value）的单行插入方式。这是单行插入执行的时候。文档中建议使用在一条上去了语句中插入多行数据，其语法是insert table（col1,col2）values(val11,val21),(val12,val22)的方式。这样一条语句执行的时候会插入多行数据，效率明显有比较大的提高。之后我在Mysql导出sql文件中看到它也是使用这种方式插入。可见效率比单行多次插入要快。
2、如果你从不同的客户端插入很多行，能通过INSERT DELAYED语句加快速度。  如果您使用DELAYED关键字，则服务器会把待插入的行放到一个缓冲器中，而发送INSERT DELAYED语句的客户端会继续运行。如果表正在被使用，则服务器会保留这些行。当表空闲时，服务器开始插入行，并定期检查是否有新的读取请求。如果有新的读取请求，则被延迟的行被延缓执行，直到表再次空闲时为止。Insert Delayed的方式我没有试过，还没有用到过从多客户端插入数据的方式。暂时先mark。
3、当从一个文本文件装载一个表时，使用LOAD DATA INFILE。这通常比使用很多INSERT语句快20倍。 这种方式应该是对于数据从文本中导入的时候，但是我们一般插入数据都是远程插入，不会有固定好格式的文本使用，这种优化方式我也没有具体用过。如果从文本中插入数据，应该会用到。
4、 锁定表可以加速用多个语句执行的INSERT操作。这样性能会提高，因为索引缓存区仅在所有INSERT语句完成后刷新到磁盘上一次。一般有多少INSERT语句即有多少索引缓存区刷新。如果能用一个语句插入所有的行，就不需要锁定。这个以前都没有注意过，不了解insert语句在数据集底层会产生什么样的操作，没想到多次磁盘刷新会降低insert语句的效率。
5、对于事务表，应使用BEGIN和COMMIT代替LOCK TABLES来加快插入。 这个深有体会，我在使用batch insert的时候，感觉插入速度很慢，一开始不知道原因，觉得使用jdbc的批量执行插入应该效率不会差很多，但是事实效率也不是很高，在插入600多条数据都用几分钟。后来上网上查了一下，发现是事务的问题，一开始事务是autocommit=true，这样在执行batch操作的时候，会自动提交事务，每次的插入操作都会执行一次事务提交，效率自然就低了很多。后来我把autocommit设置为autocommit=false，再执行插入操作的时候，果然速度快了很多。1000条数据执行也就1s时间左右。这样效率是明显提高很多了。
6、 在插入之前可以将set UNIQUE_CHECKS = 0 ,插入完成之后再设置成set UNIQUE_CHECKS = 1,这样会关闭唯一性检查，不建议使用。如果表中有索引的话，可先关闭索引建立。等待插入完成之后，再重新构建索引树。
以上是个人总结的一点关于Mysql的插入优化方法，有些地方没有亲身实践过，有什么纰漏，可以指出来。
