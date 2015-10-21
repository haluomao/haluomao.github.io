---
layout: post
title: 弱无止境。。
category: commonS
comments: false
---
#1、3+a：如果a中重载了+，a+3是对的，3+a是错误的。
因为：a+3会调用 A(a)+A(3).

#2、HTTPS协议
HTTPS协议是由SSL+HTTP协议构建的可进行加密传输、身份认证的网络协议。

#3、HTTP 2.0在2013年8月进行首次合作共事性测试。
在开放互联网上HTTP 2.0将只用于https://网址，而 http://网址将继续使用HTTP/1，目的是在开放互联网上增加使用加密技术，以提供强有力的保护去遏制主动攻击。  
HTTP/2.0提供的HTTP语义优化的运输。  
HTTP/2基于SPDY协议,充分解决了TCP连接的限制，它允许多个并发HTTP请求公用一个TCP会话  
针对只能由客户端发起请求的问题，HTTP/2添加了一种新的交互模式，即服务器推送。

#4、进程状态包括就绪，运行，等待；  
有进程处于就绪状态，则必有进程处于运行状态，不一定有进程处于等待状态。  
故10个进程处于就绪状态，则至少有1个进程处于运行状态。

#5、iframe可用在以下几个场景中：  
1：典型系统结构，左侧是功能树，右侧就是一些常见的table或者表单之类的。为了每一个功能，单独分离出来，采用iframe。   
2：ajax上传文件。   
3：加载别的网站内容，例如google广告，网站流量分析。  
4： 在上传图片时，不用flash实现无刷新。  
5： 跨域访问的时候可以用到iframe，使用iframe请求不同域名下的资源。  
6 与第三方域名下的页面共享cookie
也可参考：

[学习HTML：iframe用法总结](http://blog.csdn.net/super_marioli/article/details/4437082)

#6、cookie  
如果在一台计算机中安装多个浏览器，每个浏览器都会以独立的空间存放cookie；  
Cookie的大小限制在4kb左右，对于复杂的存储需求来说是不够用的；  
由于在HTTP请求中的Cookie是明文传递的，所以安全性成问题；

#7、使用crontab命令编辑

分　 时　 日　 月　 周　 命令  
第1列表示分钟1～59 每分钟用*或者 */1表示  
第2列表示小时1～23（0表示0点）  
第3列表示日期1～31  
第4列表示月份1～12  
第5列标识号星期0～6（0表示星期天）  
第6列要运行的命令  

以下的命令得在（ ）自动执行：06 03 * * 3 lp /usr/local/message | mail -s "server message" root

A:每周三03:06分

#8、解析xml  
SAX不需要像dom解析那样在内存中建立一个dom对象，占用内存，sax解析是逐行解析的，每次读入内存的只是一行xml，所以速度快，效率高点。不过sax一般是处理固定格式的xml。

####9、庄碧樊
在无噪声情况下，若某通信链路的带宽为3khz 。采用4个相位。每个相位具有4种振幅的QAM调制技术，则该通信链路的最大数据传输速率是？*（24kbit/s）*

奈奎斯特公式----无噪信道传输能力公式： 
 
`C=2*H*log2N(bps) `  

H为信道的带宽，本题中H=3KHz；  
N为一个码元所取得离散值个数，本题中N=16(4个相位，每个相位4中振幅)。  

`C=2*H*log2N=2*3kHz*log216=2*3k*4=24kbps; ` 

香农公式是在带噪信道容量计算时使用的公式： 
 
    C=H*log2(1+S/N)(bps)  
S为信号功率，N为噪声功率，S/N为信噪比；

#10、五个基本操作： [数据库关系代数表达式学习](http://www.blogjava.net/decode360/archive/2009/04/15/292362.html)   

    并(∪)、差(-)、笛卡尔积(×)、选择(σ)、投影(π) 
四个组合操作： 

    交(∩)、联接(等值联接)、连接（cross ）、除法(÷) 

关系模式R(a,b,c,d,)中，σ3<'4'(R) 代表：从R中选择第三列的属性值小于4的行：

	Select * from　R　where　c<'4'

#11、char是一个基本数据类型。它可以表示一个byte大小的数字，即8位，而Base64使用基于6位的编码。

12位的char和20位的char用Base64编码，位数会不同：  

12x 8/6 = 16;而20 x 8/6 = 20 x 4/3 = 24 + 2.666 ，多余的需要用  ====补齐到4位，所以是28。