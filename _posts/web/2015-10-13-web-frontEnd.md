---
layout: post
title: web前端开发面试题
category: web
comments: false
---
###1、 xhtml和html有什么区别？
HTML是一种基本的WEB网页设计语言，XHTML是一个基于XML的置标语言，不过语法上更加严格。

最主要的不同：
XHTML 元素必须被正确地嵌套。  
XHTML 元素必须被关闭。  
标签名必须用小写字母。  
XHTML 文档必须拥有根元素。  

###2、css !important
其作用是提高指定CSS样式规则的应用优先权。

在CSS中，通过对某一样式声明! important ，可以更改默认的CSS样式优先级规则，使该条样式属性声明具有最高优先级，也就是相当于写在最下面。（一般把优先级高的属性放在最下面）

	例:
	p { text-indent: 1em ! important }
	p { font-style: italic ! important }
	p { font-size: 18pt }
	p { text-indent: 1.5em}
	p { font: normal 12pt sans-serif}
	p { font-size: 24pt }
	在这些规则中 未被覆盖的有：
	p { text-indent: 1em ! important }
	p { font-style: italic ! important }
	p { font-size: 24pt }

##3、行内元素有哪些?块级元素有哪些?CSS的盒模型?
块级元素：div p h1 h2 h3 h4 form ul

行内元素: a b br i span input select

Css盒模型:内容(content)、填充(padding)、边框(border)、边界(margin)， CSS盒子模式都具备这些属性。

CSS盒子模型就是在网页设计中经常用到的CSS技术所使用的一种思维模型。


##4、HTML5有那些改进

- 最基本的就是更富语义的标签，以便更好的被机器识别； 
- Canvas+WEBGL等技术，实现无插件的动画以及图像、图形处理能力； 
- 本地存储，可实现offline应用； 
- websocket，一改http的纯pull模型，实现数据推送的梦想； 
- MathML，SVG等，支持更加丰富的render； 
- 跨浏览器方面的推动，统一标准。

##5、CSS引入的方式有哪些? link和@import的区别是?

CSS引入的四种方式：

- 链入外部样式表,把样式表保存为一个样式表文件,然后在页面中用 

	< link rel="stylesheet" type="text/css" href="*.css">

链接这个样式表文件。

- 内部样式表,就是把样式表放到页面的< head>区里.
- 导入外部样式表,用@import,在< head>与< /head>

	< style type="text/css">  
	   < !--   
	      @import "*.css"  
	   -->  
	< /style>

- 内嵌样式,就是在标签内写入style="",比如:
      < td style="border-left:#cccccc">设置表格左边框的颜色为灰色.


　　区别1：link是XHTML标签，除了加载CSS外，还可以定义RSS等其他事务；@import属于CSS范畴，只能加载CSS。

　　区别2：link引用CSS时，在页面载入时同时加载；@import需要页面网页完全载入以后加载。

　　区别3：link是XHTML标签，无兼容问题；@import是在CSS2.1提出的，低版本的浏览器不支持。

　　区别4：link支持使用Javascript控制DOM去改变样式；而@import不支持。

## 6、前端页面有哪三层构成，分别是什么?作用是什么?
结构层 Html 

表示层 CSS

行为层 js

##7、写出几种IE6 BUG的解决方法
超链接hover 点击后失效 使用正确的书写顺序 link visited hover active
（未完）

##8、解释css sprites，如何使用。
Css 精灵 把一堆小的图片整合到一张大的图片上，减轻服务器对图片的请求数量。
（未完）

##9、你如何对网站的文件和资源进行优化?

- 文件合并
- 文件最小化/文件压缩
- 使用CDN托管
- 缓存的使用

##10、什么是语义化的HTML?

直观的认识标签，对于搜索引擎的抓取有好处

##11、清除浮动的几种方式，各自的优缺点
1.使用空标签清除浮动 clear:both（理论上能清楚任何标签，增加无意义的标签）

2.使用overflow:auto（空标签元素清除浮动而不得不增加无意代码的弊端,,使用zoom:1用于兼容IE）

3.是用afert伪元素清除浮动(用于非IE浏览器)
##12、Javascript
###12.1 javascript的typeof返回哪些数据类型
Object、number、function、 boolean、 underfined。

###12.2 例举3种强制类型转换和2种隐式类型转换?
强制（parseInt,parseFloat,number）
隐式（== + –）

”==”和“===”的不同：
前者会自动转换类型
后者不会

###12.2 下面语句真值或输出：
- NaN===NaN //false
- function test(){  
	if(typeof test==='function')//true   
	...  
	}
- typeof Function结果是function
- var arr=new Array(3);  
	arr[2]=1;  
	alert(arr[0]);//undefined  
	alert(arr[2]);//1
- alert(String instanceof Object); //ture
- 
###13、ajax请求时，如何解释json数据
- eval
- parse(更安全）

###14、闭包是什么，有什么特性，对页面有什么影响？
闭包，是指语法域位于某个特定的区域，具有持续参照（读写）位于该区域内自身范围之外的执行域上的非持久型变量值能力的段落。

简单来说，Javascript闭包就是在另一个作用域中保存了一份它从上一级函数或作用域取得的变量（键值对），而这些键值对是不会随上一级函数的执行完成而销毁。

Javascript闭包的实现，通常是在函数内部再定义函数，让该内部函数使用上一级函数的变量或全局变量。

###15、call 和apply函数有什么区别，代码举例。
对于apply和call两者在作用上是相同的，但两者在参数上有区别的。

对于第一个参数意义都一样，但对第二个参数：
apply传入的是一个参数数组，也就是将多个参数组合成为一个数组传入，而call则作为call的参数传入（从第二个参数开始）。

如 func.call(func1,var1,var2,var3)对应的apply写法为：func.apply(func1,[var1,var2,var3])

同时使用apply的好处是可以直接将当前函数的arguments对象作为apply的第二个参数传入。

理解call方法：
调用一个对象的一个方法，以另一个对象替换当前对象。

call([thisObj[,arg1[, arg2[,   [,.argN]]]]])

参数
thisObj
可选项。将被用作当前对象的对象。

arg1, arg2,... , argN
可选项。将被传递方法参数序列。

说明:
call 方法可以用来代替另一个对象调用一个方法。call 方法可将一个函数的对象上下文从初始的上下文改变为由 thisObj 指定的新对象。

如果没有提供 thisObj 参数，那么 Global 对象被用作 thisObj。

###16. 像素问题
- **px:**相对长度单位，像素（px）是相对于显示器屏幕分辨率而言的。  
- **em：**单位名称为相对长度单位。相对于当前对象内文本的字体尺寸，国外使用比较多；  
- **pt：**单位名称为点（Point），绝对长度单位，一般老版本的table使用长度大小单位，但是现在基本上没有使用。  
- **rem:**是CSS3新增的一个相对单位（root em，根em）.与em有什么区别呢？**区别在于使用rem为元素设定字体大小时，仍然是相对大小，但相对的只是HTML根元素。**这个单位可谓集相对大小和绝对大小的优点于一身，通过它既可以做到只修改根元素就成比例地调整所有字体大小，又可以避免字体大小逐层复合的连锁反应。目前，除了IE8及更早版本外，所有浏览器均已支持rem。

笔试题：

	<style  type="text/css">
		body{font-size:10px;}
		div{font-size:8px;}
		h1{font-size:1.25em;}
	</style>
	
	<body>
		<div>
			<h1>text</h1>
		</div>
	</body>

只有这样h1才是10px；

单位换算：  

- 任意浏览器的默认字体高度16px（16像素）。所有未经调整的浏览器都符合: 1em=16px。

- 为了简化font-size的换算，需要在css中的body选择器中声明font-size=62.5%，这就使em值变为 16px*62.5%=10px, 这样12px=1.2em, 10px=1em, 也就是说只需要将你的原来的px数值除以10，然后换上em作为单位就行了。

em的特点：  
1. em的值并不是固定的;  
2. em会继承父级元素的字体大小。

为了单位换算错误推荐使用PX（像素）作为网页制作单位。

##17、html5语义化标签
- article  
article标签装载显示一个独立的文章内容。
例如一篇完整的论坛帖子，一则网站新闻，一篇博客文章等等，一个用户评论等等 artilce可以嵌套，则内层的artilce对外层的article标签有隶属的关系。例如，一个博客文章，可以用article显示，然后一 些评论可以以article的形式嵌入其中。  
-- 例如：
	<!-- html -->
	    <article>
		<h1>文章标题</h1>
		这是一篇文章
		   <article>评论1...</article>
		    <article>评论2...</article>
		</article>
- aside  
aside 用来装载非正文类的内容。例如广告，成组的链接，侧边栏等等。
例如：
	<!-- html -->
		<body>
		<aside>
		热门文章
		</aside>
		<aside>
		广告
		</aside>
		<article>
		<h1>文章标题</h1>
		这是一篇文章
		   <article>评论1...</article>
		    <article>评论2...</article>
		</article>
		</body>

- header 标签定义文档的页面组合，通常是一些引导和导航信息。
	<!-- html -->
		<header>
		<p>this is the page Logo</p>
		<nav>this is page navigation</nav>
		</header>
- footer 标签定义 section 或 document 的页脚。在典型情况下，该元素会包含创作者的姓名、文档的创作日期以及/或者联系信息。
	<!-- html -->
		<footer> © 2015 Felxi copyright </footer>

- nav 标签定义显示导航链接不是所有的成组的超级链接都需要放在nav标签里。  
nav标签里应该放入一些当前页面的主要导航链接。 例如在页脚显示一个站点的导航链接（如首页，服务信息页面，版权信息页面等等），就可以使用nav标签，当然，这不是必须的。 
	<!-- html -->
		<nav>
		<ul>
		<li><a href=”articles.html”>Index of all articles</a></li>
		<li><a href=”today.html”>Things sheeple need to wake up for today</a></li>
		<li><a href=”successes.html”>Sheeple we have managed to wake</a></li>
		</ul>
		</nav>

- mark 标签定义带有记号的文本。请在需要突出显示文本时使用 <mark> 标签。
	<!-- html -->
		<p>Do not forget to buy <mark>milk</mark> today.</p>

- contextmenu 添加到系统右键菜单 [貌似这个功能只有firefox支持，很悲催的]
	<!-- html -->
		<div>添加到系统右键菜单< contextmenu=mymenu /div> <menu type="context" id="mymenu" />

- hgroup 标签用于对网页或区段的标题元素（h1-h6）进行组合。例如，在一个区段中你有连续的h系列的标签元素，则可以用hgroup将他们括起来。
	<!-- html -->
		<hgroup>
		<h1>The reality dysfunction</h1>
		<h2>Space is not the only void</h2>
		</hgroup> <hgroup>
		<h1>Dr. Strangelove</h1>
		<h2>Or: How I Learned to Stop Worrying and Love the Bomb</h2>
		</hgroup>

##18、ECMAScript
ECMAScript是一种由Ecma国际（前身为欧洲计算机制造商协会,英文名称是European Computer Manufacturers Association）通过ECMA-262标准化的脚本程序设计语言。这种语言在万维网上应用广泛，它往往被称为**JavaScript或JScript**，但实际上后两者是ECMA-262标准的实现和扩展。

ECMAScript 6中多了两个定义变量的关键词，一个是let，另一个是const，后者顾名思义就是常量定义，前者的作用域范围是块级的。

一般写过js的童鞋都知道，同其他语言一样，JS中的变量作用域是函数域而不是块级分割的，但是涉及到变量提升（hosting），闭包等问题的时候，很多有经验的程序员依然会头疼。

	var a = 5;
	if(true){
	    var a = 10;
	}
	console.log(a);//10
上面的结果是10，但是我们看到，在if block内外都有一个a的定义，按我们正常的理解来看，这两个a应该占用的是不同的内存，而事实上，他们共用同一个内存。为此，ES 6中的let关键词“修复”了这个问题。

	let a = 5;
	if(true){
	    let a = 10;
	}
	console.log(a); //5
let作用在块级作用域中，所以不管是switch还是if还是for，只要是let定义的变量，他就只能在那个花括号内部起作用。let是一个让程序员比较省心的一个关键词，而还有一个令人兴奋的关键词是let的兄弟const，一旦定义一个变量为const类型，后面就不能对他进行修改。

	const aa = 11;
	alert(aa) //11
	aa = 22;
	alert(aa) //11
关于这两者的兼容性问题，可以到这里查看[http://kangax.github.io/es5-compat-table/es6/](http://kangax.github.io/es5-compat-table/es6/)

Node已经支持了const和let关键词，可以这样使用node --harmony和use strict。目前一些浏览器还不支持这样的写法，但是利用defs.js这个库可以ES3也支持这个。他的原理就是利用esprima来编译并重写你的代码。比如：

	"use strict";
	function fn() {
	    const y = 0;
	    for (let x = 0; x < 10; x++) {
	        const y = x * 2;
	        const z = y;
	    }
	    console.log(y); // prints 0
	}
	fn();
经过def.js重新编译之后变成：

	"use strict";
	function fn() {
	    var y = 0;
	    for (var x = 0; x < 10; x++) {
	        var y$0 = x * 2;
	        var z = y$0;
	    }
	    console.log(y); // prints 0
	}
	fn();

##18、下面两个css样式表达式都不会加载图像！
	#useless-css{
		background-image:url("abc/pic.jpg");
		}
	#img{
		background-image:url("http://haluomao.github.io/images/201509/apple.png");
		display:none;
	}
## AngularJs
## Node.js

## 页面布局