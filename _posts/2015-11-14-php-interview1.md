---
layout: post
title: php面试题1
category: php
comments: false
---
##1、基础面试题
###1.1 如何设置form表单中的只读属性？
- 利用readonly 设置指定内容的只读属性
- 利用disabled 实现

###1.2 在什么情况下，$name 与 $_POST['name']可以通用？
在php.ini中register_globals=On时，它们才都可以获取form表单中表单元素name的值。

但是不建议开启这个全局变量，因为会带来安全隐患或其他问题。

###1.3 CSS的理解
CSS是W3C协议提出的层叠样式表（Cascading Style Sheet），为了弥补HTML在显示属性设定上的不足而制定的。

最大的用途是：实现内容和表现形式的分离，改变网页的整体表现形式，更容易进行外观维护，使HTML文档代码更为简练，缩短浏览器的加载时间。

###1.4 插入CSS的方式
- 在标签内部定义style属性
- 在head区域，定义一对`<style></style>`标记，在标记内部利用标签名称、类选择符、id选择符设置属性。
- 创建.css文件定义样式，之后再HTML页面中利用`<link>`标签引入文件。如：`<link type="text/css" rel="stylesheet" href="PATH">`

###1.5 在IE6下解决双倍边距的问题
IE6下的bug，margin-left:10px会解析成20px。

加上`display:inline;`.

###1.6 解决超链接被点击后hover样式不出现的问题？
只要对超链接样式属性进行正确的排序即可。顺序如下：
	
	link-visited-hover-action

代码如下：

	a:link{color:red; text-decoration:none}
	a:visited{...}
	a:hover{...}
	a:action{...}

###1.7 定义1px左右高度的容器
通过CSS样式定义的1px高度的区块往往是不能正常显示的，解决的方法如下：

在div标签中控制文字的行高，超出行高的内容设置为不显示：
	
	div{overflow:hidden|zoom:0.08 | line-height:1px;border:1px solid black}

###1.8 `<span>`和`<div>`的区别
- `<span>`是在HTML4.0时才加入，后者在3.0就有了。
- 同样作用于网页布局中，span是属于内联的，一般用于小模块的样式内联到HTML中；div是块级元素，用于组合大块的代码。

###1.9 编写代码，当鼠标划过文本框，自动选择文本框中的内容
`<input id="text" type="text" value="text">`

使用select方法：

`<input id="text" type="text" value="text" onmouseover="this.select()">`

扩展：当鼠标划过，自动情况内容：

`<input id="text" type="text" value="text" onclick="this.value=''">`

###1.10 php中文乱码解决
只要保证php.in、页面编码、文件编码（这个容易忽略）三者编码保持一致。
用utf-8时，文件需要保持为utf-8，并消息BOM格式，页面上设置：

	header("Content-Type: text/html; charset=utf-8");

或
	
	<meta http-equiv="Content-Type" content="text/html; charset=utf-8">

utf-8与utf-8(无BOM)的区别 ：简单来说，BOM是用来表示文件字节是大端编码还是小端编码的三个字节，无BOM保存就是在文件开头没有这三个字节。

>[utf-8与utf-8(无BOM)的区别](http://afericazebra.blog.163.com/blog/static/30050408201211199298711/)

>BOM——Byte Order Mark，就是字节序标记。在UCS 编码中有一个叫做"ZERO WIDTH NO-BREAK SPACE"的字符，它的编码是FEFF。而FFFE在UCS中是不存在的字符，所以不应该出现在实际传输中。UCS规范建议我们在传输字节流前，先传输 字符"ZERO WIDTH NO-BREAK SPACE"。这样如果接收者收到FEFF，就表明这个字节流是Big-Endian的；如果收到FFFE，就表明这个字节流是Little- Endian的。因此字符"ZERO WIDTH NO-BREAK SPACE"又被称作BOM。

>UTF-8不需要BOM来表明字节顺序，但可以用BOM来表明编码方式。字符"ZERO WIDTH NO-BREAK SPACE"的UTF-8编码是EF BB BF。所以如果接收者收到以EF BB BF开头的字节流，就知道这是UTF-8编码了。

>UTF- 8编码的文件中，BOM占三个字节。如果用记事本把一个文本文件另存为UTF-8编码方式的话，用UE打开这个文件，切换到十六进制编辑状态就可以看到开 头的FFFE了。这是个标识UTF-8编码文件的好办法，软件通过BOM来识别这个文件是否是UTF-8编码，很多软件还要求读入的文件必须带BOM。

PHP不支持BOM。PHP在设计时就没有考虑BOM的问题，也就是说他不会忽略UTF-8编码的文件开头BOM的那三个字符。

##2、PHP基础面试题
###2.1 PHP的含义
是PHP Hypertext Preprocessor（PHP超文本预处理器）的缩写，是一种服务器端的、开源的、跨平台的、HTML嵌入式的脚步语言，语法混合了C、Java和Perl的特点，适合Web开发。

###2.2 PHP的优劣势
- 结构化（html嵌入式），把前端代码从程序分离出来、用面向对象编程特性编程
- 规范化。方法和变量命名，提高代码可读性。
- 安全性：php搞笑、灵活、没有固定的框架，但是它把安全问题留给了程序员。程序员要自行解决如跨脚步攻击（XSS）（可以用`htmlspecialchars`函数填补)、跨站请求伪造（CSRF）、代码注入漏洞、字符编码循环漏洞等。

它强大到足以成为在网络上最大的博客系统的核心（WordPress）！
它深邃到足以运行最大的社交网络（facebook）！
而它的易用程度足以成为初学者的首选服务器端语言！

###2.3 类型转换
用settype函数：
	`settype($var, 'bool');`

gettype获取类型

	gettype('1');返回的是string 
	gettype(1);返回的是integer 	

类型判断：is_string()、is_object等。

‘===’比较运算符，表示数值上相等，而且两者的类型也一样

###2.4 PHP基础
- 在 PHP 中，所有用户定义的函数、类和关键词（例如 if、else、echo 等等）都对大小写**不敏感**；（ECHO  和echo是一样的）所有变量都对大小写敏感。（ $color、$COLOR 以及 $coLOR 被视作三个不同的变量）
- Local 和 Global 作用域：
函数之外声明的变量拥有 Global 作用域，**只能**在函数以外进行访问。  
函数内部声明的变量拥有 LOCAL 作用域，只能在函数内部进行访问。  
下列的输出，只有10。

		<?php
		$x=5; // global scope
		  
		function myTest() {
		   $y=10; // local scope
		   echo "<p>在函数内部测试变量：</p>";
		   echo "变量 x 是：$x";
		   echo "<br>";
		   echo "变量 y 是：$y";
		} 
- global 关键词用于访问函数内的全局变量。
要做到这一点，请在（函数内部）变量前面使用 global 关键词：

		function myTest() {
		  global $x,$y;
		  $y=$x+$y;
		}
- PHP 同时在名为 $GLOBALS[index] 的数组中存储了所有的全局变量。下标存有变量名。这个数组在函数内也可以访问，并能够用于直接更新全局变量。

		function myTest() {
		  $GLOBALS['y']=$GLOBALS['x']+$GLOBALS['y'];
		} 
- 在 PHP 中，有两种基本的输出方法：echo 和 print。
  echo 和 print 之间的差异：
	- echo - 能够输出一个以上的字符串,如：`echo "This", " string", " was", " made", " with multiple parameters.";`
	- print - 只能输出一个字符串，并始终返回 1
	- 提示：echo 比 print 稍快，因为它不返回任何值。
	
	```
	$cars=array("Volvo","BMW","SAAB");  ```
	```echo "My car is a {$cars[0]}";	
	```
-  var_dump() 会返回变量的数据类型和值

		$x = 5985;
		var_dump($x);
		//输出：int(5985) 

- 如需设置常量，请使用 define() 函数 - 它使用三个参数：
	- 首个参数定义常量的名称
	- 第二个参数定义常量的值
	- 可选的第三个参数规定常量名是否对大小写敏感。默认是 false。 
	 
	下例创建了一个对大小写敏感的常量，值为 "Welcome to W3School.com.cn!"：

		<?php
		define("GREETING", "Welcome to W3School.com.cn!");
		echo GREETING;
		//define("GREETING", "Welcome to W3School.com.cn!", true);//不敏感
		?>
- 字符串连用`.`,如:`$a = "Hello";$b = $a . " world!";echo $b; // 输出 Hello world!`

- !==运算符：不全等（完全不同）	$x !== $y	如果 $x 不等于 $y，且它们类型不相同，则返回 true。

- 定义函数：

		function functionName() {
		  被执行的代码;
		}

- 在 PHP 中， array() 函数用于创建数组。
	
	- 索引数组 - 带有数字索引的数组：`$cars=array("Volvo","BMW","SAAB");//索引是自动分配的（索引从 0 开始`
	- 关联数组 - 带有指定键的数组:`$age=array("Peter"=>"35","Ben"=>"37","Joe"=>"43");`
	- 多维数组 - 包含一个或多个数组的数组:

			$cars = array
			  (
			  array("Volvo",22,18),
			  array("BMW",15,13),
			  array("Saab",5,2),
			  array("Land Rover",17,15)
			  );

- PHP 中的许多预定义变量都是“超全局的”，这意味着它们在一个脚本的全部作用域中都可用。在函数或方法中无需执行 global $variable; 就可以访问它们。
	- $GLOBALS:引用全局作用域中可用的全部变量
	- $_SERVER:保存关于报头、路径和脚本位置的信息,如：`$_SERVER['PHP_SELF']	返回当前执行脚本的文件名。`
	- **$_REQUEST**:用于收集 HTML 表单提交的数据.
	- ** $_POST**: 广泛用于收集提交 method="post" 的 HTML 表单后的表单数据。$_POST 也常用于传递变量。
	- **$_GET**
	- $_FILES
	- $_ENV
	- $_COOKIE
	- $_SESSION
-  Date() 函数把时间戳格式化为更易读的日期和时间。`date(format,timestamp)`  
mktime() 函数返回日期的 Unix 时间戳:`mktime(hour,minute,second,month,day,year)`  

		$d=mktime(9, 12, 31, 6, 10, 2015);
		echo "创建日期是 " . date("Y-m-d h:i:sa", $d);

	strtotime() 函数用于把人类可读的字符串转换为 Unix 时间。
- include vs. require:require 语句同样用于向 PHP 代码中引用文件。
不过，include 与 require 有一个巨大的差异：如果用 include 语句引用某个文件并且 PHP 无法找到它，脚本会继续执行.


###2.5 php表单、cookie
	
	<html>
	<body>
	
	<form action="welcome.php" method="post">
	Name: <input type="text" name="name"><br>
	E-mail: <input type="text" name="email"><br>
	<input type="submit">
	</form>
	
	</body>
	</html>

welcome.php：

	<html>
	<body>
	
	Welcome <?php echo $_POST["name"]; ?><br>
	Your email address is: <?php echo $_POST["email"]; ?>
	
	</body>
	</html>

输出：
	
	Welcome John
	Your email address is john.doe@example.com

- 防止XSS，用test_input函数来检查传递的数据
	 
		function test_input($data) {
		  $data = trim($data);//去除用户输入数据中不必要的字符（多余的空格、制表符、换行）
		  $data = stripslashes($data);//删除用户输入数据中的反斜杠（\）
		  $data = htmlspecialchars($data);//把特殊字符转换为 HTML 实体
		  return $data;
		}

- 如何创建 cookie？  
setcookie() 函数用于设置 cookie。`setcookie(name, value, expire, path, domain);`
注释：setcookie() 函数必须位于 <html> 标签之前。

	cookie 常用于识别用户。cookie 是服务器留在用户计算机中的小文件。每当相同的计算机通过浏览器请求页面时，它同时会发送 cookie。通过 PHP，您能够创建并取回 cookie 的值。

- 如果您的应用程序涉及不支持 cookie 的浏览器，您就不得不采取其他方法在应用程序中从一张页面向另一张页面传递信息。一种方式是从表单传递数据（有关表单和用户输入的内容，稍早前我们已经在本教程中介绍过了）。



##3、PHP中利用JQuery的Ajax实现功能

Asynchronous JavaScript And XML（异步 JavaScript 及 XML）

通过下面的这个例子进行学习吧。

在文本框中输入一个年份，判断其生肖，并在文本框输出。

	<html>
	<head>
	<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
	</head>
	<body>
	<input type="text" value="年份格式1990" onclick="this.select()">
	<input type="submit" value="Judge">
	<span></span>
	
	<script type="text/javascript" src="jquery-2.1.4.min.js"></script>
	<script>
	$(function(){
		$("input:last").click(function(){
			$.get("in.php", {
				number:$("input:first").val()
			}, function(data){
				$("span").text(data);
				
			});
		});
	});
	</script>
	
	</body>
	</html>

服务器端in.php文件

	<?php
	if(isset($_GET['number'])){
		$array=array("猪","鼠","牛","虎","兔","龙","蛇","马","羊","猴","鸡","狗");
		foreach($array as $key=>$value){
			if(ceil($_GET['number']%12)==$key){
				echo $value;
			}
		}
	}
	?>

##5、PHP高级
##5.1 什么是 PHP 过滤器？
PHP 过滤器用于验证和过滤来自非安全来源的数据。  
验证和过滤用户输入或自定义数据是任何 Web 应用程序的重要组成部分。
设计 PHP 的过滤器扩展的目的是使数据过滤更轻松快捷。

什么是外部数据？1.来自表单的输入数据,2.Cookies,3.服务器变量,4.数据库查询结果.

##5.2 Mysql操作

	$con = mysql_connect("localhost","peter","abc123") or die('Could not connect: ' . mysql_error());
	
	mysql_query("CREATE DATABASE my_db",$con);// Create database
		
	mysql_select_db("my_db", $con);

	// Create table in my_db database
	$sql = "CREATE TABLE Persons 
	(
	FirstName varchar(15),
	LastName varchar(15),
	Age int
	)";
	mysql_query($sql,$con);

	//select
	$result = mysql_query("SELECT * FROM Persons ORDER BY age");
	
	while($row = mysql_fetch_array($result))
	  {
	  echo $row['FirstName'];
	  echo " " . $row['LastName'];
	  echo " " . $row['Age'];
	  echo "<br />";
	  }

	//update
	mysql_query("UPDATE Persons SET Age = '36'
	WHERE FirstName = 'Peter' AND LastName = 'Griffin'");

	//delete
	mysql_query("DELETE FROM Persons WHERE LastName='Griffin'");

	mysql_close($con);

##4、 Zend