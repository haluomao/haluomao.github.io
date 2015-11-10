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

TBC