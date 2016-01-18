---
author: lieeGin
comments: true
date: 2013-01-20 16:09:03+00:00
layout: post
slug: first-procedure
title: 写的第一个存储过程
wordpress_id: 977
categories:
- 一周一博
---

因为工作上存在一个需求，就是每个月将客户的库存信息更新，简单的就是说以上个月的库存记录为基础，在数据库新建一条记录，将上个月月末余存数量转为这个月月初开始数量，然后还包含其他一些字段的赋值，这个就不多说。

原本这个任务是每天用线程去跑。但是经常会出现问题，有时线程不会执行。这次决定将它转移到数据库来做。原本以为是第一次写存储过程，后来发现，把第一次写包也顺带做了。

其实知道存储过程的语法之后，这也没什么难的了。

首先，create or replace procedure  procedure_name  is ，就跟写视图一样，如果需要参数，可以在名字后面加括号，加参数名和类型，如（code varchar2(32)）。

然后，begin。。。。。end 先写好，在里面写需要执行的sql。逻辑什么的就跟写java代码一样了。

这里还使用到了游标，说实话，以前oracle 没好好听课，一直不清楚游标是啥，其实就是一个集合，一般用于循环读取。就跟for循环一样。比如，我在做这个到库存数据的任务中，需要分别为每个客户导数据，那么，我首先要从企业客户中取出各个客户，那么，可以这样定义一个游标：

CURSOR v_enterprise is
select enterprise_code
from system_enterprise ;

然后使用的时候，先打开游标：

open v_enterprise;

开启循环：
loop

提取记录到指定参数中：
fetch v_enterprise into v_enterprise_code;

这样，就可以使用v_enterprise_code做参数去做其他操作了。

oracle给参数赋值，用select attr1，attr2 into pram1，pram2  from XXX的格式。明白语法之后，基本就和写java代码没什么区别了。什么if判断都是差不多的。

接下来说包，我也没有接触很深，我的感觉他就是将多个存储过程放在一起执行。定义一个包，包里指定存储过程：

create package XXX is 。。。。begin。。。  end。

这里要说的就是，我使用的过程中，包里只写存储过程名称，另外需要定义包体。就是说包头包体分开定义。先定义包头，然后 在包体的定义中将存储过程写好就ok。

最后就是定时任务了。我的这个任务是每天凌晨执行，当然有条件判断，满足条件才会导数据。

定义定时任务：

DECLARE
v_jobno NUMBER;
BEGIN
begin
sys.dbms_job.submit(job =>v_jobno,
what => '包名.存储过程名;',
next_date =>trunc(sysdate+1),
interval => 'trunc(sysdate+1)');
commit;
end;
SYS.DBMS_OUTPUT.PUT_LINE('Job Number is: ' || to_char(v_jobno));
COMMIT;
END;

其中：next_date =>trunc(sysdate+1),表示每天凌晨执行。

大致过程就是这样的，表示在测试过程中，因为以前不知道怎么用，后来才知道如果单独执行一个存储过程的话，是需要放在begin和end 中间的：

begin

execute  过程名;

end;




