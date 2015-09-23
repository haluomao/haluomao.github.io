---
layout: post
title: Java 面试题（不定期更新）
category: Java
comments: false
---
### 代码阅读
1. 下面代码的运行结果是？  

  
		class Person{
			public Person(){
				System.out.println("A person");
			}
		}
	
		public class Teacher extends Person {
		
			private String name="tom";
			
			public Teacher(){
				System.out.println("A teacher");
				super();
			}
			
			public static void main(String[] args) {
				Teacher teacher = new Teacher();
				System.out.println(this.name);
			}
		}

【答案】  
	 有两处错误：  
	 1. super()--Constructor call must be the first statement in a constructor.  
	 2. this--Cannot use this in a static context.

2. 有没有看过Java数据结构源代码？
  
 必须得回答看过啊。事先看。
 1. 先了解Set接口：
 
	public interface Set<E> extends Collection<E>{
		int size();
		boolean isEmpty();
		Iterator<E> iterator();
		//其他的函数
		boolean equals(Object o);
		int hashCode();
	}

  再看一个实现类，HashSet:

	public class HashSet<E>
    extends AbstractSet<E>
    implements Set<E>, Cloneable, java.io.Serializable
	{
		private transient HashMap<E,Object> map;
	
	    // Dummy value to associate with an Object in the backing Map
	    private static final Object PRESENT = new Object();
	
	    /**
	     * Constructs a new, empty set; the backing <tt>HashMap</tt> instance has
	     * default initial capacity (16) and load factor (0.75).
	     */
	    public HashSet() {
	        map = new HashMap<>();
	    }
	
		//神奇的操作: 默认大小是16，负载因子（load factor)默认值为0.75
	 	public HashSet(Collection<? extends E> c) {
	        map = new HashMap<>(Math.max((int) (c.size()/.75f) + 1, 16));
	        addAll(c);
	    }

		public boolean add(E e) {
       		return map.put(e, PRESENT)==null;
    	}
	
		...
   	}
	
  然后会发现一些有趣的事情：

  1. HashSet竟然是用HashMap来实现的。新加入的元素是加入了map中key，value都是同一个Object。

  2. 理解负载因子：  
loadFactor可以看成是容量极限(threshold)/实际容量(capacity)=键值最高对数/实际容量

例如：  
如果负载因子是0.75，hashmap(16)最多可以存储12个元素，想存第16个就得扩容成32。  
如果负载因子是1，hashmap(16)最多可以存储16个元素。

   关于负载因子的问题： 
 
1. 为什么增大负载因子可以减少Hash表所占用的内存空间，但会增加查询数据的时间开销。  
回答：对于存储同样数目的值，负载因子为0.75和1所占的内存空间，是0.75的要多；为1的时候，虽然空间利用率高，但是由于需要解决哈希冲突，需要的额外的开销，增加了查询时间。
  
2. 为什么减少负载因子可以提高查询数据的性能，但会减低Hash表所占用的内存空间。  
   类似于上面的回答。


站内有一篇介绍哈希表的文章：[Hash 哈希的神奇之处](/algorithm/2015/09/23/java-dataStruct.html)
	