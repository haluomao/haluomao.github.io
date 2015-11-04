---
layout: post
title: 掌握spring
category: tech
comments: false
---
【喵体悟】学会用，对于一个要成为senior programmer的人是远远不够的，还要懂得其原理，知其所以然。

阅读《Spring技术内幕——深入解析Spring架构与设计原理》、
《精通Spring2.0》 罗时飞 2007（一看就知道是中国人写的书，利用一大堆名词和代码来凑数）、《Spring in Action（中文版）》 Craig Walls.etc. 

###1、Spring是什么？
Spring是一个轻量级的IoC和AOP容器框架。

- 轻量级：大小上和系统开支都是轻量级的，而且是非侵入式的。
- 反向控制：实现松耦合，使用IoC，对象是被动接受依赖而不是自己去找。
- 面向切片：将业务逻辑从系统服务中分离出来，达到内聚开发。系统对象只做它们该做的业务逻辑。
- 容器：Spring是一个容器，包含且管理系统对象的生命周期和配置。
- 框架：在Spring中，支持使用简单的组件配置组合成一个复杂的系统。并且提供了很多基础功能（事务管理、持久层集成等）。

###2、Spring的主旨思想是什么？为什么会成功？
IoC 和 AOP

- 控制反转Ioc：BeanFactory使用工厂模式来实现，将系统的配置和依赖关系从代码中独立出来。
- AOP：一种编程技术，用于在提供中提升业务的分离。

###3、IOC容器
一个是BeanFactory、一个是ApplicationContext

###4、为什么springMVC和Mybatis逐渐流行起来了
Spring为Web系统提供了全功能的MVC框架。虽然Spring可以很容易地与其他MVC框架（如Struts)集成，但是Spring的MVC框架利用IoC将**控制逻辑和业务逻辑清晰地分离开**来。

SpringMVC的优点:

- 与Spring框架天生整合，无框架兼容问题
- 与Struts2相比安全性高
- 配置量小、开发效率高

MyBatis的优点：

- 不需要重新学习hibernate框架，在掌握sql的基础上就可以上手；
- 不需要配置实体类与数据表之间的映射关系；
- hibernate不能自己控制sql语句