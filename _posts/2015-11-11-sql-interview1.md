---
layout: post
title: sql笔试题
category: sql
comments: false
---
##1、sql查询一段日期内的某个时间段的数据量
例如：想查询BOOK_DATE在2010-06-01到2010-08-01之间的13点到15点之间的数据，如何实现？

解决方案：

	select * from 表 
	where (convert(char(10), BOOK_DATE) between '2010-06-01' and '2010-08-01')
	and (convert(char(8), convert(datetime, BOOK_DATE, 120) , 108) between '13:00:00' and '15:00:00')

##2、查询手机消息发送情况，按地区和时段。
数据：  

	msgCode status region stime  
	001		1		sh	2015-11-12 17:59:19  
	002		1		hz	2015-11-12 10:59:19  
	003		0		sh	2015-11-11 09:59:19  
	004		-1		sh	2015-11-11 19:32:19
	005		0		hz	2015-11-11 22:32:19  

1表示发送成功，0表示失败，-1表示未知。未知不算到发送成功率中。  
查询的数据是从早上8点到晚上8点。

			
查询结果：

	region rate
	hz		1.0000
	sh		0.5000

解决方法：

	SELECT region, SUM(CASE status WHEN 1 then 1
	ELSE 0 END )/SUM(CASE status WHEN 1 then 1 WHEN 0 then 1 ELSE 0 END) rate
	FROM msgrecord 
	WHERE CAST(stime AS TIME) BETWEEN '08:00:00' AND '20:00:00'
	GROUP BY region;