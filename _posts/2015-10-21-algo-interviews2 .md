---
layout: post
title: 算法面试题集之好代码
category: algo
comments: false
---
代码之美
###1、Remove Duplicates from Sorted Array
【问题描述】  
Given a sorted array, remove the duplicates in place such that each element appear only once and return the new length.

Do not allocate extra space for another array, you must do this in place with constant memory.

For example,
Given input array nums = [1,1,2],

Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively. It doesn't matter what you leave beyond the new length.

【解答】
这道题主要考验人对问题考虑的是否全面，本人提交了10次，才把边界问题全面处理妥当。

然后在讨论里面看到一个回答，这段代码相比我的，要好n倍，也很巧妙：

	public class Solution {
		public int removeDuplicates(int[] nums) {
			if(nums.length==0)return 0;
			int j=1,index=1;
		    for(int i=0;i<nums.length-1;i++){
		        if(nums[i+1]!=nums[i]){
		           nums[j++]=nums[i+1]; 
		           index++;
		        }
		    }
		    return index;
		}
	} //去掉index变量，最后返回j也是可以的。

###2、计算n!末尾所包含0的个数
例如，5！=120，其末尾所含有的“0”的个数为1；10！= 3628800，其末尾所含有的“0”的个数为2；20！= 2432902008176640000，其末尾所含有的“0”的个数为4。

其计算公式为：
令f(x)表示正整数x末尾所含有的“0”的个数，则有： 

      当0 < n < 5时，f(n!) = 0; 

      当n >= 5时，f(n!) = k + f(k!), 其中 k = n / 5（取整）。

从而可以递归求解。

###3、计算从1到n，计算1出现的个数

例如：
N= 2，写下 1，2。这样只出现了 1 个“1”。
N= 12，我们会写下 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12。这样，1的个数是 5。

总结方法：

假设N表示为a[n]a[n-1]...a[1]，其中`a[i](1<=i<=n)`表示N的各位数上的数字。

c[i]表示从整数1到整数a[i]...a[1]中包含数字1的个数。

x[i]表示从整数1到10^i - 1中包含数字1的个数，例如，x[1]表示从1到9的个数，结果为1；x[2]表示从1到99的个数，结果为20；

当a[i]=1时，c[i] = a[i-1]*...*a[1] +1+ c[i-1]+x[i-1];

当a[i]>1时，c[i] = a[i]x[i-1]+c[i-1]+10^(i-1);

没怎么懂----
[计算0到N中包含数字1的个数](http://blog.sina.com.cn/s/blog_6933011901013cdb.html)


###4、非基于比较的排序算法（三种）
TBC