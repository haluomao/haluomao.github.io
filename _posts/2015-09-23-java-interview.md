---
layout: post
title: Java 面试题（不定期更新）
category: Algorithm
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
   

	