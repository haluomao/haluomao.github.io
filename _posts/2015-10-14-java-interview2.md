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