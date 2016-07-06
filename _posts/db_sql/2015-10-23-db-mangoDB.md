---
layout: post
title: MangoDB
category: db
comments: false
---
Modified @2016年7月6日 10:25:49


# mongodb
sql server能够做到读写分离，双机热备份和集群部署, so does mongodb.

## 主从复制

			 --- 从数据库
			 |	
	主数据库--	 
			 |
			 --- 从数据库

好处：
	
- 数据备份
- 数据恢复
- 读写分离

在默认的情况下，mongodb从属数据库不支持数据的读取，在驱动中给提供了一个叫做“slaveOkay"可以显式的读取从属数据库，以此来减轻主数据库的性能压力。


## 分片技术
mongodb采用分片解决方案：将集合进行拆分，然后将拆分的数据均摊到几个片上。

首先要了解”片键“的概念，也就是说拆分集合的依据是什么？按照什么键值进行拆分集合....

mongos就是一个路由服务器，它会根据管理员设置的“片键”将数据分摊到自己管理的mongod集群，数据和片的对应关系以及相应的配置信息保存在"config服务器"上。

mongod:   一个普通的数据库实例，如果不分片的话，我们会直接连上mongod。

  ① shards：片。

  ② databases:  其中有个partitioned字段表示是否分区。

  ③ chunks： 段。

## mongodb的三要素

- 数据库-db
- 集合-collection 相当与关系数据库中的“表”
- 文档-document	相当与关系数据库中的“行”

这里的文档是一个json的扩展（Bson)，文档是采用“K-V”格式存储的

removed在mongodb中是一个不可撤回的操作。


## find 操作
  日常开发中，查询条件最多的也就是两类：

     ①： >, >=, <, <=, !=, =。

     ②：And，OR，In，NotIn

这些操作在mongodb里面都封装好了：

<1> "$gt", "$gte", "$lt", "$lte", "$ne", 直接用，这些跟上面的1是一一对应的。

<2> 默认值, "$or", "$in"，"$nin", 这些跟上面的2是一一对应的。
 
<3> 在mongodb中还有一个特殊的匹配，那就是“正则表达式”.

	db.user.find<{"name":/^j/}>

<4> 如果查询很复杂，可以使用$where

	db.user.find<{$where:function(){ return this.name=='jack'} } >

## upsert操作

这个可是mongodb创造出来的“词”，update方法的第一次参数是“查询条件”，那么这个upsert操作就是说：如果没有查到，就在数据库里面新增一条。

避免了在数据库里面去判断是update还是add操作，使用起来很简单

将update的第三个参数设为true即可。

## 聚合函数

常见的聚合操作跟sql server一样，有：count，distinct，group，mapReduce。

### mapReduce
mapReduce其实是一种编程模型，用在分布式计算中，其中有一个“map”函数，一个”reduce“函数。

   ① map：

          这个称为映射函数，里面会调用emit(key,value)，集合会按照你指定的key进行映射分组。

   ② reduce：

         这个称为简化函数，会对map分组后的数据进行分组简化，注意：在reduce(key,value)中的key就是emit中的key，
         vlaue为emit分组后的emit(value)的集合，这里也就是很多{"count":1}的数组。

   ③ mapReduce:

          这个就是最后执行的函数了，参数为map，reduce和一些可选参数。

## 性能分析函数（explain）

mongodb提供了一个关键字 explain 可以作为性能分析工具。

	db.person.find().explain()

输出的关键字含义：

- cursor:  这里出现的是”BasicCursor",什么意思呢，就是说这里的查找采用的是“表扫描”，也就是顺序查找。

- nscanned:  扫描的文档个数。

- n:  返回文档个数。

- millis: 耗时（毫秒）。 

## 建立索引（ensureIndex）

	db.person.ensureIndex({"name":1})

使用了ensureIndex在name上建立了索引。”1“：表示按照name进行升序，”-1“：表示按照name进行降序。

mongodb采用B树的结构来存放索引,使用索引后性能会提升很多。

建立唯一索引，重复的键值自然就不能插入：
	db.person.ensureIndex({"name":1},{"unique":true})

组合索引，只需增加条件就行。

删除索引:dropIndexes。
	db.person.dropIndexes("name_1")


## 参考
> [8天学通MongoDB](http://www.cnblogs.com/huangxincheng/archive/2012/02/18/2356595.html)