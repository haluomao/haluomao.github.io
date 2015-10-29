---
layout: post
title: 掌握spring
category: tech
comments: false
---
【喵体悟】学会用，对于一个要成为senior programmer的人是远远不够的，还要懂得其原理，知其所以然。

阅读《Spring技术内幕——深入解析Spring架构与设计原理》、
《精通Spring2.0》 罗时飞 2007（一看就知道是中国人写的书，利用一大堆名词和代码来凑数）、
###1、先去借书！！

###2、Spring的主旨思想是什么？为什么会成功？
IoC 和 AOP

- 控制反转Ioc

###3、IOC容器
一个是BeanFactory、一个是ApplicationContext

###4、为什么springMVC和Mybatis逐渐流行起来了

SpringMVC的优点:

- 与Spring框架天生整合，无框架兼容问题
- 与Struts2相比安全性高
- 配置量小、开发效率高

MyBatis的优点：

- 不需要重新学习hibernate框架，在掌握sql的基础上就可以上手；
- 不需要配置实体类与数据表之间的映射关系；
- hibernate不能自己控制sql语句