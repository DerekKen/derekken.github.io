---
layout:     post
title:      "Leetcode练习笔记(1) Reverse Integer 反转数字"
subtitle:   "Leetcode No.7 Reverse Integer. Gains of leetcode practice, a novice's point of view"
date:       2017-10-17 17:00:00
author:     "Derek Ken"
header-img: "img/in-post/coding_practice_notes/practice-gains-02.jpg"
header-mask: 0.60
catalog:    true
comment:    true
tags:
    - Algorithms
    - ACM
    - Leetcode
    - OJ
---

> Practice makes perfect.

# **反转数字**

## **Leetcode 7. Reverse Number**

### 题目 Problem

[See This Problem on Leetcode](https://leetcode.com/problems/reverse-integer/)

Reverse digits of an integer.

Example1: x = 123, return 321
Example2: x = -123, return -321

Have you thought about this?
Here are some good questions to ask before coding. Bonus points for you if you have already thought through this!

If the integer's last digit is 0, what should the output be? ie, cases such as 10, 100.

Did you notice that the reversed integer might overflow? Assume the input is a 32-bit integer, then the reverse of 1000000003 overflows. How should you handle such cases?

For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows.

**Note**:
The input is assumed to be a 32-bit signed integer. Your function should return 0 when the reversed integer overflows.

### 分析 Analysis

**我自己的思路**：

1. 对于负数，统一变成正数后再处理。

2. 首先考虑反转后溢出的问题，题目中的"overflow"应该包含了上溢与下溢(underflow)两种情况。
32位有符号整数的范围为(-2^31) ~ (2^31 - 1)，同时注意到发生溢出时数的符号会发生改变，可以利用这一点判断是否发生溢出。
[Update]注意到9646324351反转后溢出，但是不会改变符号!!
有效的解决办法：设置一个阈值threshold (2^31 - 1) / 10，在执行rev_num * 10前判断rev_num是否大于threshold。

[//]: # (This may be the most platform independent comment) 但是这样还不完备(删除)/完备的？， 假如rev_num恰好等于214748364，此时是否可能发生溢出呢？设原数的最高位为x，则x不可能为8或9(原数形如x46384721)，实际上x只能等于1，否则就已经发生溢出了(如果x大于1，则原数一定大于2^31 - 1 = 2147483647)。

**由于已经将所有负数转换成了正数，所以下面只讨论rev_num > 0的情况：**

* case 1: 若 rev_num < threshold， 则(rev_num * 10 + num % 10)不可能溢出；
* case 2: 若 rev_num = threshold， 则原数 = 146384721，即原数最高位不能大于1；否则原数会发生上溢，而这与|rev_num| = |threshold|矛盾。
于是可知rev_num = 2147483641 < (2^31-1)，不会溢出；
* case 3: 若 rev_num > threshold，则rev_num一定会发生溢出，此时按照题目要求直接返回0即可。

综上可知，这种判断方法在逻辑上是完备的。

3. 如果一个整数的最后一位数字为0，那么反转后忽略处于高位的那些无效的‘0’；例如，100反转后返回1。

4. 通过mod 10的操作首先获得原数字num的个位，赋给变量rev_num，然后num /= 10去掉最后一位并再次mod 10获取十位上的数字，
即(num % 10 + rev_num * 10)，这样即可获取num最后两位数字反转后的结果；重复之前的步骤，直到 num = 0为止。

按照如上思路写出的代码如下：

```cpp
class Solution 
{
public:
    int reverse(int x) 
	{
        bool neg = false;
        if(x == 0) return 0;
        else if(x < 0) { x = -x; neg = true; }//change negative nums to postive
        int rev_num = 0, num = x;
        int threshold = ((1 << 31) - 1) / 10; //note that ((1 << 31) / 10) overflows!
        while(num > 0)
        {
            if(rev_num > threshold) return 0;
            rev_num = rev_num * 10 + num % 10;
            num /= 10;
        }
        if(neg) { x = -x; rev_num = -rev_num; } //change back
        return rev_num;
    }
};
```

<div style="text-align:center"><b>Prog. 1</b> Leetcode 7. Reverse Number </div>

我发现最近同一段程序提交后在Leetcode上的运行时间非常不稳定，甚至好几次提交耗时最短的sample code时都发现实际的运行时间远远超过了最短耗时。
经过多次测试，发现以上代码的最短运行耗时为12ms，排在前20%左右。
 ![1](http://owsep4p7v.bkt.clouddn.com/blog/posts/img/leetcode7_time_elapsed-min.png) 
<div style="text-align:center"><b>Fig. 1</b> Prog. 1的耗时 </div>


之后我查看了一段声称耗时8ms并进行了溢出检查的C++代码，发现其总体思路与我的差不多，**但是对于溢出的处理非常neat**，这段代码是在(rev_num * 10)之后再进行溢出检查的：
通过引入一个临时变量t来记录翻转后的数，然后直接比较(t/10)是否等于翻转前的数rev_num。
若两者相等，则继续翻转；否则，直接返回0。
同样地，这段样本代码的执行时间也非常不稳定，而且其耗时也超过宣称的8ms......多次提交后发现运行时间在15ms左右。

P.S. 是不是交钱订阅Leetcode的增值服务就可以获得一个负载更少或者计算资源更多的服务器？

### 代码 Code

```cpp
class Solution 
{
public:
    int reverse(int x) 
	{
        int rev_num = 0, t = 0;
        while(x)
        {
            t = rev_num * 10 + x % 10;
            if((t/10) != rev_num) return 0; //overflow: true
            x /= 10;
            rev_num = t; 
        }
        return rev_num;
    }
};
```

<div style="text-align:center"><b>Prog. 2</b> 8ms C++ Sample Code </div>

### 反思总结 Reflections

回过头来看，自己写的溢出检测流程冗长，其实只要运用好“如果一个数发生了溢出，那么便一定不会等于之前的值”这个简单却很实用的性质即可。

---

[1]: https://leetcode.com "Leetcode homepage"

[2]: http://www.cnblogs.com/DerekKen/p/6819390.html "DerekKen的博客园"
