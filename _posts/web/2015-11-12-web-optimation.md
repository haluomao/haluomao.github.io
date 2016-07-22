---
layout: post
title: 前端优化
category: web
comments: false
---
先对优化部分有一个大局观，以后遇到具体问题再深入研究！

#1、前端性能优化
>参考：[前端攻略系列](http://www.cnblogs.com/Darren_code/archive/2011/12/31/property.html)

##1.1 减少HTTP请求
当我们请求的网页文件中有很多图片、CSS、JS甚至音乐等信息时，将会频繁的与服务器建立连接，与释放连接，这必定会造成资源的浪费，且每个HTTP请求都会对服务器和浏览器产生性能负担。

网速相同的条件下，下载一个100KB的图片比下载两个50KB的图片要快。所以，请减少HTTP请求。

**解决办法：**

**合并**图片（css sprites），合并CSS和JS文件；图片较多的页面也可以使用 **lazyLoad** 等技术进行优化。 还可以使用**压缩**来减少请求流量。

##1.2 正确理解 Repaint 和 Reflow
Repaint(重绘)就是在一个元素的外观被改变，但没有改变布局(宽高)的情况下发生，如改变visibility、outline、背景色等等。

Reflow(重排)就是DOM的变化影响到了元素的几何属性（宽和高），浏览器会重新计算元素的几何属性，会使渲染树中受到影响的部分失效，浏览器会验证DOM树上的所有其它结点的visibility属性，这也是Reflow低效的原因。  
如：改变窗囗大小、改变文字大小、内容的改变、浏览器窗口变化，style属性的改变等等。如果Reflow的过于频繁，CPU使用率就会噌噌的往上涨，所以前端也就有必要知道 Repaint 和 Reflow的知识。

**解决办法：**
上面提到通过设置style属性改变结点样式的话，每设置一次都会导致一次reflow，所以最好通过设置class的方式；　有动画效果的元素，它的position属性应当设为fixed或absolute，这样不会影响其它元素的布局；如果功能需求上不能设置position为fixed或absolute，那么就权衡速度的平滑性。

　　总之，因为 Reflow 有时确实不可避免，所以只能**尽可能限制Reflow的影响范围**。

##1.3 减少对DOM的操作

对DOM操作的代价是高昂的，这在网页应用中的通常是一个性能瓶颈。

天生就慢。在《高性能JavaScript》中这么比喻：“把DOM看成一个岛屿，把JavaScript(ECMAScript)看成另一个岛屿，两者之间以一座收费桥连接”。所以每次访问DOM都会教一个过桥费，而访问的次数越多，交的费用也就越多。所以一般建议尽量减少过桥次数。

**解决办法：**
修改和访问DOM元素会造成页面的Repaint和Reflow，循环对DOM操作更是罪恶的行为。所以请合理的使用JavaScript变量储存内容，考虑大量DOM元素中循环的性能开销，在循环结束时一次性写入。

　　**减少对DOM元素的查询和修改，查询时可将其赋值给局部变量。**

　　注：在IE中:hover会降低响应速度。

##1.4 使用JSON格式来进行数据交换
  
　　JSON是一种轻量级的数据交换格式，采用完全独立于语言的文本格式，是理想的数据交换格式。同时，JSON是 JavaScript原生格式，这意味着在 JavaScript 中处理 JSON数据不需要任何特殊的 API 或工具包。

　　与XML序列化相比，JSON序列化后产生的数据一般要比XML序列化后数据体积小，所以在Facebook等知名网站中都采用了JSON作为数据交换方式。

##1.5 高效使用HTML标签和CSS样式

HTML是一门标记语言，使用合理的HTML标签前你必须了解其属性，比如Flow Elements，Metadata Elements ，Phrasing Elements。比较基础的就是得知道块级元素和内联元素、盒模型、SEO方面的知识。

- 块级元素(block),默认是独自占据一行的。比如`<p>、<h1~h6>、DIV, FORM, TABLE、<ul>、<ol>、<dl>、<pre>、<hr />`
- 内联元素(inline)，默认是几个内联元素都可以在同一行上显示。比如`<a>、<span>、LABEL, INPUT,IMG`等。 对行内元素设置高度、宽度、内外边距等属性，都是无效的。

**一般来说块级元素可以包含块级元素和内联元素；
    但内联元素只能包含内联元素。**

网页设计中常听的属性名：内容(content)、填充(padding)、边框(border)、边界(margin)， CSS盒子模式都具备这四个属性。

SEO比较杂糅，优化可以从文档类型、语言编码、标题标签、alt、h1、strong、字数、css和js的调用、标签规范化等多个方面进行。

　　CSS是用来渲染页面的，也是存在渲染效率的问题。CSS选择符是从右向左进行匹配的，这里对css选择符按照开销从小到大的顺序梳理一下：　

　　ID选择符 #box  
　　类选择符 .box    
　　标签 div  
　　伪类和伪元素 a:hover

##1.6 使用CDN加速（内容分发网络）

其基本思路是**尽可能避开互联网上有可能影响数据传输速度和稳定性的瓶颈和环节，使内容传输的更快、更稳定。**

通过在网络各处放置节点服务器所构成的在现有的互联网基础之上的一层智能虚拟网络，CDN系统能够**实时地**根据**网络流量**和**各节点的连接**、**负载状况**以及**到用户的距离和响应时间**等综合信息将用户的请求重新导向离用户最近的服务节点上。

实时性不太好是CDN的致命缺陷。远程服务器的网络内容网页要与复本服务器或缓存器中的网页保持同步。

**解决方法**：在网络内容发生变化时将新的网络内容从服务器端直接传送到缓存器，或者当对网络内容的访问增加时将数据源服务器的网络内容尽可能实时地复制到缓存服务器。 

##1.7 将CSS和JS放到外部文件中引用，CSS放头，JS放尾

易维护、易扩展，方便管理和重复利用。

JavaScript是浏览器中的霸主，为什么这么说，因为在浏览器在执行JavaScript代码时，不能同时做其它事情，即`<script>`每次出现都会让页面等待脚本的解析和执行（不论JavaScript是内嵌的还是外链的），JavaScript代码执行完成后，才继续渲染页面。这个也就是JavaScript的阻塞特性。

　　因为这个阻塞的特点，建议把JavaScript代码放到</body>标签以前(相当于最后了），这样既能有效的防止JavaScript的阻塞，又能使得页面的HTML结构能更快的释放（加载）。

　　HTML规范清楚指出CSS要放包含在页面的<head>区域内，这里就不多解释了。

##1.8 精简CSS和JS文件
CSS和JavaScript的压缩，能直接减少下载的文件体积。

使用 YUI Compressor，它的特点是：移除注释；移除额外的空格；细微优化；标识符替换。

　　YUI Compressor是java程序，如果你对java很熟悉的话可快速的上手使用yuicompressor.jar；如果你对java很陌生也没关系，一样可以使用YUI Compressor。

 1.压缩JS
　　`java -jar yuicompressor-2.4.2.jar api.js > api.min.js`

 2.压缩CSS
　　`java -jar yuicompressor-2.4.2.jar style.css > style.min.css`

##1.9 压缩图片和使用图片Sprite技术

一般图片压缩的方式有：

　　1.缩小图片分辨率；

　　2.改变图片格式；

　　3.降低图片保存质量。

　　关于图片精灵(Sprite)技术就和我们工作直接相关，不管是在CSS中的图片还是在HTML结构中的图片都会产生HTTP请求，前端优化的第一条就是减少请求数，最直接有效的方法是使用图片精灵（CSS Sprite）。

**图片精灵就是把许多图片放到一张大图片里面，通过CSS来显示图片的一部分。**

　　至于图片精灵的操作细节就不多做介绍了，网上相关内容很多。

##1.10 注意控制Cookie大小和污染

因为Cookie是本地的磁盘文件，每次浏览器都会去读取相应的Cookie，所以建议去除不必要的Coockie，**使Coockie体积尽量小以减少对用户响应的影响**；

　　使用Cookie跨域操作时注意在适应级别的域名上设置coockie以便使子域名不受其影响

　　Cookie是有生命周期的，所以请注意设置合理的过期时间，合理地Expire时间和不要过早去清除coockie，都会改善用户的响应时间。