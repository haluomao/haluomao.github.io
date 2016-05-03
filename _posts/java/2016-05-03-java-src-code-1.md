---
layout: post
title: Java源码阅读1
category: java
comments: false
---

## 阅读Java源码的初衷

1. 装b
2. 满足自己的好奇心
3. 提升自己的编码能力
4. 为下次面试做好准备

## 执行过程

阅读代码需要有编程基础和足够的耐心，最后要有记录和思考，虽说如此，但我任务这个比看ACM和IEEE会议上的paper要容易一些吧。

1. 选好IDE和需要阅读的源代码： Intellij idea (或eclipse) + JDK 1.7
1. 先看一些大牛门的建议，少走一些弯路。
  > [Java源码阅读的真实体会](http://zwchen.iteye.com/blog/1154193)  
  [Java 推荐读物与源代码阅读](http://www.360doc.com/content/10/0116/16/724027_13720736.shtml)  
  [如何更有效地学习开源项目的代码？](https://www.zhihu.com/question/19637879)

1. 观看顺序建议
    - 先熟悉代码结构，有一个大局观和查看计划；
    - 再看类库预热，如：String类的实现（core包），Util中基本数据结构的实现（util包），并发(concurrency包)，有关文本的（text包），有关网络的http(http包)等等;
    - 然后再看JVM部分代码，这里需要先理解JVM的工作原理，尽量读懂代码，但也不要过分深入，除非工作内容和这个密切相关；
    - 最后，一定要整理回顾，将所看的内容整理成文章，用脑记下来。

1. 有时间去看看spring的源码，据说很赞。


## Java代码阅读之路
