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
