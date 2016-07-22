---
layout: post
title: 面试被问到的问题
category: tech
comments: false
---

##1、递归和循环实现的差别
- 通常递归的代码会比较简洁，循环实现比较复杂。
- 递归调用需要额外的时间和空间消耗：每一次函数调用，都需要在内存栈中分配空间以保存参数、返回地址以及临时变量，而且往栈里压入数据和弹出数据都需要时间。
- 递归中有可能很多计算都是重复的，从而对性能产生负面影响。
- 除了效率问题，递归还可能引起**调用栈溢出**。

##2、线程安全和线程不安全
**线程安全就是说多线程访问同一代码，不会产生不确定的结果。编写线程安全的代码是低依靠线程同步。**


线程安全问题都是由全局变量及静态变量引起的。
若每个线程中对全局变量、静态变量只有读操作，而无写操作，一般来说，这个全局变量是线程安全的；若有多个线程同时执行写操作，一般都需要考虑线程同步，否则的话就可能影响线程安全。

首先要明白线程的工作原理，jvm有一个main   memory，而每个线程有自己的working   memory，一个线程对一个variable进行操作时，都要在自己的working   memory里面建立一个copy，操作完之后再写入main   memory。多个线程同时操作同一个variable，就可能会出现不可预知的结果。根据上面的解释，很容易想出相应的scenario。 

而用synchronized的关键是建立一个monitor，这个monitor可以是要修改的variable也可以其他你认为合适的object比如method，然后通过给这个monitor加锁来实现线程安全，每个线程在获得这个锁之后，要执行完   load到workingmemory   －>   use&assign   －>   store到mainmemory   的过程，才会释放它得到的锁。这样就实现了所谓的线程安全。

Bloch 给出了描述五类线程安全性的分类方法：不可变、线程安全、有条件线程安全、线程兼容和线程对立。

1. 不可变的对象一定是线程安全的，并且永远也不需要额外的同步[1]  。因为一个不可变的对象只要构建正确，其外部可见状态永远也不会改变，永远也不会看到它处于不一致的状态。Java 类库中大多数基本数值类如 Integer 、 String 和 BigInteger 都是不可变的。

2. 线程安全的对象具有在上面“线程安全”一节中描述的属性 -- 由类的规格说明所规定的约束在对象被多个线程访问时仍然有效，不管运行时环境如何排列，线程都不需要任何额外的同步。这种线程安全性保证是很严格的 -- 许多类，如 Hashtable 或者 Vector 都不能满足这种严格的定义。
3. 有条件的线程安全类对于单独的操作可以是线程安全的，但是某些操作序列可能需要外部同步。
4. 线程兼容类不是线程安全的，但是可以通过正确使用同步而在并发环境中安全地使用。这可能意味着用一个 synchronized 块包围每一个方法调用，或者创建一个包装器对象，其中每一个方法都是同步的(就像 Collections.synchronizedList() 一样)。也可能意味着用 synchronized 块包围某些操作序列。
5. 线程对立类是那些不管是否调用了外部同步都不能在并发使用时安全地呈现的类。线程对立很少见，当类修改静态数据，而静态数据会影响在其他线程中执行的其他类的行为，这时通常会出现线程对立。线程对立类的一个例子是调用 System.setOut() 的类。

##3、为什么要用单例而不是静态方法？
单例就是我们运行的当前虚拟机中有且只有一个需要的对象，不存在重复。static是给类静态成员变量使用的，属于类的属性，一般是一些常量之类的东西。

- 从加载上来说对于类和对象之间，在类加载到内存时候静态成员变量就存在了，而对象还不存在。
- 静态对象只能调用静态方法和静态变量，如果全部搞成静态方法那么意味着其他成员变量都要是静态的，很不方便，如果一天不要单例了也不容易扩展，很麻烦。

##4、final 和 const
java中的final与C++中的const的区别

final在java中定义常量，可作用于基本类型或者类类型，若是作用于类类型，则此类类型不能作为父类被继承，也就是说它的下面不能有子类，这样的类叫做原子类。  

C＋＋中的const定义常量。


- Java中的final如果是对于基本类型，那和C++ const是一样的  
- 但是如果是对对象而言，就不同了。final表示这个句柄是不可改变的  
  `final   Object   obj=(Object)new   String("a");  `
 ` obj=(Object)new   String("hello");//是非法的  `  
  但是依然可以调用obj的方法。如((String)obj).length()是合法的.    
 而C++如果一个对象被定义成const，就不能调用对象的方法。除非这个方法被定义成const.

##5、static 和 const
(其实有次面试也被问到了，昨天又跌这个坑里了，这是不做笔记不反思的结果）

对于C/C++语言来讲, 
const就是只读的意思,只在声明中使用;   

static一般有2个作用,**规定作用域和存储方式**。对于局部变量,static规定其为静态存储方式,每次调用的初始值为上一次调用的值,调用结束后存储空间不释放;   
对于全局变量,如果以文件划分作用域的话,此变量只在当前文件可见;对于static函数也是在当前模块内函数可见. 

**控制变量的存储方式和可见性：**

- static被引入以告知编译器，将变量存储在程式的静态存储区而非栈上空间。

- static更有一个作用，他会把变量的可见范围限制在编译单元中，使他成为一个内部连接，这时，他的反义词为”extern”.

static const 应该就是上面两者的合集. 

下面分别说明:
   
- 全局:  
const,只读的全局变量,其值不可修改. 
static,规定此全局变量只在当前模块(文件)中可见. 
static const,既是只读的,又是只在当前模块中可见的. 

- 文件: 
文件指针可当作一个变量来看,与上面所说类似. 

- 函数: 
const,返回只读变量的函数. 
static,规定此函数只在当前模块可见. 

- 类:   
const,一般不修饰类,(在VC6.0中试了一下,修饰类没啥作用) 
static,C++中似乎没有静态类这个说法,一般还是拿类当特殊的变量来看.C#中有静态类的详细说明,且用法与普通类大不相同


const 推出的初始目的，是为了取代预编译指令，消除他的缺点，同时继承他的好处。

c++的编译器通常**不为普通const常量分配存储空间**，而是将他们保存在符号表中，这使得他成为一个编译期间的常量，没有了存储和读内存的操作，使得他的效率也非常高，同时，这也是他取代预定义语句的重要基础。这里，我要提一下，为什么说这一点是也是他能取代预定义语句的基础，这是因为，编译器不会去读存储的内容，如果编译器为const分配了存储空间，他就不能够成为一个编译期间的常量了。

##6、预处理指令
作用：

1. 一是避免了意义模糊的数字出现，使得程式语义流畅清晰。如：  
\#define user_num_max 107 这样就避免了直接使用107带来的困惑。

2. 二是能非常方便地进行参数的调整和修改，如上例，当人数由107变为201时，进改动此处即可。
3. 三是提高了程式的执行效率，由于使用了预编译器进行值替代，并不必为这些常量分配存储空间，所以执行的效率较高。

预处理语句虽然有以上的许多好处，但他有个比较致命的缺点，即，**预处理语句仅仅只是简单值替代，缺乏类型的检测机制**。这样预处理语句就不能享受c++严格类型检查的好处，从而可能成为引发一系列错误的隐患。