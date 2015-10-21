---
layout: post
title: Java 面试题2（不定期更新）
category: Java
comments: false
---
## 1、匿名内部类
参考：[java中的匿名内部类总结](http://www.cnblogs.com/nerxious/archive/2013/01/25/2876489.html)

摘要：匿名内部类的基本实现

	abstract class Person {
	    public abstract void eat();
	}
	 
	public class Demo {
	    public static void main(String[] args) {
	        Person p = new Person() {
	            public void eat() {
	                System.out.println("eat something");
	            }
	        };
	        p.eat();
	    }
	}

只要一个类是抽象的或是一个接口，那么其子类中的方法都可以使用匿名内部类来实现。

最常用的情况就是在多线程的实现上，因为要实现多线程必须继承Thread类或是继承Runnable接口。
##2. immutable不可变对象

不可变对象是指创建后状态不可以修改的Object，每次对他们的改变都是产生了新的immutable的对象，而mutable Objects就是那些创建后，状态可以被改变的Objects.

举个例子：String和StringBuilder，String是immutable的，每次对于String对象的修改（如trim，uppercase,substring等）都将产生一个新的String对象，而原来的对象保持不变，而StringBuilder是mutable，因为每次对于它的对象的修改都作用于该对象本身，并没有产生新的对象。

**使用Immutable类的好处：**

1）Immutable对象是线程安全的，可以不用被synchronize就在并发环境中共享

2）Immutable对象简化了程序开发，因为它无需使用额外的锁机制就可以在线程间共享

3）Immutable对象提高了程序的性能，因为它减少了synchroinzed的使用

4）Immutable对象是**可以被重复使用的，你可以将它们缓存起来重复使用，就像字符串字面量和整型数字一样**。你可以使用静态工厂方法来提供类似于valueOf（）这样的方法，它可以从缓存中返回一个已经存在的Immutable对象，而不是重新创建一个。

immutable也有一个**缺点**就是会制造大量垃圾，由于他们不能被重用而且对于它们的使用就是”用“然后”扔“，字符串就是一个典型的例子，它会创造很多的垃圾，给垃圾收集带来很大的麻烦。当然这只是个极端的例子，合理的使用immutable对象会创造很大的价值。

**如何在Java中写出Immutable的类？** 

要写出这样的类，需要遵循以下几个原则：

1）immutable对象的状态在创建之后就不能发生改变，任何对它的改变都应该产生一个新的对象。

2）Immutable类的所有的属性都应该是final的。

3）对象必须被正确的创建，比如：对象引用在对象创建过程中不能泄露(leak)。

4）对象应该是final的，以此来限制子类继承父类，以避免子类改变了父类的immutable特性。

5）如果类中包含mutable类对象，那么返回给客户端的时候，返回该对象的一个拷贝，而不是该对象本身（该条可以归为第一条中的一个特例）

例子：

	public final class Contacts {
	 
	    private final String name;
	    private final String mobile;
	 
	    public Contacts(String name, String mobile) {
	        this.name = name;
	        this.mobile = mobile;
	    }
	   
	    public String getName(){
	        return name;
	    }
	   
	    public String getMobile(){
	        return mobile;
	    }
	}

##3. Java中BigDecimal和BigInteger

float和double类型的主要设计目标是为了科学计算和工程计算。他们执行二进制浮点运算，这是为了在广域数值范围上提供较为精确的快速近似计算而精心设计的。然而，它们没有提供完全精确的结果，所以不应该被用于要求精确结果的场合。但是，商业计算往往要求结果精确，这时候BigDecimal就派上大用场啦.

BigInteger：支持任意精度的整数，可以精确地表示任意大小的整数值，同时在运算过程中不会丢失任何信息。

BigDecimal 由任意精度的整数非标度值 和32 位的整数标度 (scale) 组成。

	BigDecimal aDouble =new BigDecimal(1.22);
	System.out.println("construct with a double value: " + aDouble);

输出结果是：construct with a double value:1.2199999999999999733546474089962430298328399658203125

从上面的例子可以看出：参数类型为double的构造方法的结果有一定的不可预知性（而用String是完全可预知的）

另外，BigInteger与BigDecimal都是不可变的（immutable）的，在进行每一步运算时，都会产生一个新的对象，所以a.add(b);虽然做了加法操作，但是a并没有保存加操作后的值，正确的用法应该是a=a.add(b);

输出位数设置:

		//BigDecimal输出位数设置（按照四舍五入）
		BigDecimal tmp = new BigDecimal("39614081257132168796771975167.05");
		tmp=tmp.setScale(1, BigDecimal.ROUND_HALF_UP);
		System.out.println(tmp);

##5、Java中double输出精度控制方法
保留两位小数

方法一：

	{
	   double c=3.154215;
	   java.text.DecimalFormat myformat=new java.text.DecimalFormat("0.00");
	   String str = myformat.format(c);    
	}

方式二：

	{
	   java.text.DecimalFormat df = new java.text.DecimalFormat("#.00"); 
	   df.format(number);
	   //例：new java.text.DecimalFormat("#.00").format(3.1415926)
	   #.00 表示两位小数 #.0000四位小数 以此类推...
	}

方式三：

	{
	   double d = 3.1415926;
	   String result = String .format("%.2f");
	   //%.2f: %. 表示 小数点前任意位数, 2 表示两位小数,格式后的结果为f,表示浮点型
	}
##6、Java的输入问题
输入空行结束输入，这段代码是不行的：

	while(cin.hasNext()){
		String tmp = cin.nextLine();			
		if(tmp.equals("")){
			System.out.println("space");
			break;
		}
	}

将while里面换成true就行了。

###7、Java中的引用
在Java中的引用类型,是指除了基本的变量类型之外的所有类型,所有的类型在内存中都会分配一定的存储空间(形参在使用的时候也会分配存储空间,方法调用完成之后,这块存储空间自动消失)。

 基本的变量类型只有一块存储空间(分配在stack中), 而引用类型有两块存储空间(一块在stack中,一块在heap中), 方法形参的值传递(引用)是指形参和传进来的参数指向同一个值的内存(heap)中;

1. 引用是一种数据类型，保存了对象在内存中的地址，这种类型即不是我们平时所说的简单数据类型也不是类实例(对象)；

2. 不同的引用可能指向同一个对象，换句话说，一个对象可以有多个引用，即该类类型的变量。

3. 对象是如何传递的呢。关于对象的传递，有两种说法，即“它是按值传递的”和“它是按引用传递的”。

####7.1 介绍4种引用类型。

- 强引用(StrongReference)  
强引用是使用最普遍的引用,我们平时申明变量使用的就是强引用。如果一个对象具有强引用，那垃圾回收器绝不会回收它。  
当内存空间不足，Java虚拟机宁愿抛出OutOfMemoryError错误，使程序异常终止，也不会靠随意回收具有强引用的对象来解决内存不足的问题。比如，String s = "Hello World",A a = new A();

- 软引用(SoftReference)  
如果一个对象只具有软引用，则内存空间足够，垃圾回收器就不会回收它；如果内存空间不足了，就会回收这些对象的内存。  
类似弱引用，只不过Java虚拟机会尽量让软引用的存活时间长一些，迫不得已才清理。

-  弱引用(WeakReference)  
弱引用与软引用的区别在于：只具有弱引用的对象拥有更短暂的生命周期。在垃圾回收器线程扫描它所管辖的内存区域的过程中，一旦发现了只具有弱引用的对象，不管当前内存空间足够与否，都会回收它的内存。  
弱引用可以和一个引用队列（ReferenceQueue）联合使用，如果弱引用所引用的对象被垃圾回收，Java虚拟机就会把这个弱引用加入到与之关联的引用队列中。

- 虚引用(PhantomReference)  
仅用来处理资源的清理问题.虚引用并不会决定对象的生命周期。  
如果一个对象仅持有虚引用，那么它就和没有任何引用一样，在任何时候都可能被垃圾回收器回收。  
虚引用**主要用来跟踪对象被垃圾回收器回收的活动**。虚引用与软引用和弱引用的一个区别在于：虚引用必须和引用队列 （ReferenceQueue）联合使用。当垃圾回收器准备回收一个对象时，如果发现它还有虚引用，就会在回收对象的内存之前，把这个虚引用加入到与之 关联的引用队列中。

###8、java中的>>>
“>>>”运算符所作的是无符号的位移处理，它不会将所处理的值的最高位视为正负符号，所以作位移处理时，会直接在空出的高位填入0。当我们要作位移的原始值并非代表数值时（例如：表示颜色图素的值，最高位并非正负号），可能就会需要使用此种无符号的位移。

`>>>` 右移，左边空出的位以0填充。  
`>>=` 右移赋值  
`>>>=` 右移赋值，左边空出的位以0填充  
`<<=` 左 移赋值  