---
layout:     post
title:      "Leetcode练习笔记(0) Tex Quotes & WERTYU 字符替换"
subtitle:   "Tex Quotes & WERTYU, gains of coding practice, a novice's point of view"
date:       2017-10-08 22:00:00
author:     "Derek Ken"
header-img: "img/in-post/coding_practice_notes/practice-gains-00.jpg"
header-mask: 0.50
catalog:    true
comment:    true
tags:
    - Algorithms
    - ACM
---

> 今天练了练《算法竞赛入门经典(第2版)》上的字符串替换的题目(实际上来自[UVa Online Judge](https://uva.onlinejudge.org/index.php))，发现有一些零碎的知识点需要总结。

# **字符替换题目练习总结**

## **Tex Quotes(Tex中的引号, UVa 272)**

> Tex中的引号：连按两次“ESC”键下方的按键，输入左双引号“``”；连按“Enter”键左边的按键两次，输入右双引号“''”。

- 题目 Problem

在TeX中，左双引号是“``”，右双引号是“''”。输入一篇包含双引号的文章，你的任务是
把它转换成TeX的格式。

样例输入：
"To be or not to be," quoth the Bard, "that
is the question".

样例输出：
\`\`To be or not to be,'' quoth the Bard, \`\`that
is the question''.

- 分析 Analysis
1. 对于本题，读取输入不能使用scanf("%s")来读取字符串，因为scanf这个函数遇到空白符(space、Tab、LF以及CRLF等)便会停下来；
虽然再次调用scanf时可以顺利读取下一段字符串，但是无法知道这之间有多少个空白符。

* 可以使用fgetc(fin)读取一个打开的文件，读取一个字符，然后返回一个int值。其返回值类型为int而不是char的原因在于，当文件结束时，fgetc将返回
一个特殊的int值EOF，用于与其他返回值区分，如果返回值为char则无法区分。

* 或者也可以使用getchar，它等价于fgetc(stdin)。

2. 另一个问题在于判断一个引号是左引号还是右引号，方法其实很简单，用一个标志变量的奇偶性即可判断。

- 提示 Hints

> 使用fgetc(fin)可以从打开的文件fin中读取一个字符。一般情况下应当在检查它不是EOF后再将其转换成char值。
从标准输入读取一个字符可以用getchar，它等价于fgetc(stdin)。

* 用scanf("%d", &n)读取整数n，如果在输入123后不小心多输入了一个回车换行符，则getchar会读取到该回车换行符，
但是问题在于不同操作系统的回车换行符是不一样的，Windows平台上的是CR LF(Carriage Return、Line Feed，即回车、换行)，Linux平台上是LF("\n")，MacOS上是CR("\r")；
在Windows平台上用getchar或fgetc读取文件时，会跳过"\r\n"中的"\r"，而**直接**读取到"\n"，但如果在Linux平台下读取**同样一份文件**，
则会首先读取到"\r"，再次读取时才会读取到"\n"。

> 在使用fgetc和getchar时，应该避免写出和操作系统相关的程序。

> "fgets(buf, maxn, fin)"将读取完整的一行放在字符数组buf中。应当保证
buf足够存放下文件的一行内容。除了在文件结束前没有遇到“\n”这种特殊情况外，buf总是以“\n”结尾。当一个字符都没有读到时，fgets返回NULL。

* 与fgetc类似，fgets也有一个“标准输入版”的对应函数gets，但是gets函数只接受一个参数（char * gets ( char * str );），并没有指明最多读取多少字符。
即gets将不管str的可用空间有多大，只要被调用就会往str中存储字符串，这样就可能导致缓冲区溢出。

> C语言并不禁止程序读写"非法内存"。例如，声明的是char s[100]，完全可以赋值s[10000] = 'a'（甚至-Wall也不会警告），但后果自负。

> C语言中的gets(s)存在缓冲区溢出漏洞，不推荐使用。在C11标准里，该函数已被正式删除。


- 代码 Code

[On Github](https://github.com/DerekKen/Algorithms-Coding-Practice/blob/master/practice/Tex-Quotes-Uva272.c)

<div style="text-align:center"><b>Prog1.</b> Tex-Quotes-Uva272 </div>

```c
#include<stdio.h>
int main()
{
	int ch, quote = 1;
	while((ch = getchar()) != EOF)
	{
		if (ch == '"') { printf("%s", quote ? "``" : "''"); quote = !quote; }
		else printf("%c", ch);
	}
	return 0;
}
```

- 总结与收获Gains

本题可以边读边处理，于是选择使用getchar函数，标志变量quote在每次遇到引号时变换奇偶性，以判断当前是左引号还是右引号。
三目运算符":?"的使用可以使代码更加简洁，同时不失可读性。


## **WERTYU(WERTYU, UVa 10082)**

- 题目 Problem

把手放在键盘上时，稍不注意就会往右错一
位。这样，输入Q会变成输入W，输入J会变成输
入K等。键盘如图3-2所示。
输入一个错位后敲出的字符串（所有字母均
大写），输出打字员本来想打出的句子。输入保
证合法，即一定是错位之后的字符串。例如输入中不会出现大写字母A。

 ![1](http://owsep4p7v.bkt.clouddn.com/blog/posts/img/acm-beginner-3-2-min.jpg) 
<div style="text-align:center"><b>Fig1.</b> QWERTY键盘布局 </div>

样例输入：
O S, GOMR YPFSU/

样例输出：
I AM FINE TODAY

- 分析 Analysis

1. 与上一题类似，本题也可以边读边处理，因此getchar适合用于读取输入，至于输出，用putchar最简洁。

2. 如何处理输入呢，一种方法是使用if或者switch语句进行字符的映射，比如if(c == '1') putchar('`')。但这样的实现方式会导致代码膨胀，
看上去十分臃肿，而且很有可能写错字符间的对应关系。更简洁的方法是使用常量数组，如下所示。

- 代码 Code

[On Github](https://github.com/DerekKen/Algorithms-Coding-Practice/blob/master/practice/WERTYU-UVa10082.c)

<div style="text-align:center"><b>Prog2.</b> WERTYU, UVa 10082 </div>

```c
#include <stdio.h>

//note that counter slash "\" is an escape character "\\"
char key_mapping[] = { "`1234567890-=QWERTYUIOP[]\\ASDFGHJKL;'ZXCVBNM,./" };

int main()
{
	char c;
	int i;
	while ((c = getchar()) != EOF)
	{
		for (i = 0; key_mapping[i] && key_mapping[i] != c; ++i);
		if (key_mapping[i]) putchar(key_mapping[i - 1]);
		else putchar(key_mapping[i]);
	}
	return 0;
}
```

**注意**反斜杠'\'在常量数组中需要进行转义（“\\\”）。


- 提示 Hints

> 善用常量数组往往能简化代码。定义常量数组时无须指明大小，编译器会计算。

---

[1]: https://leetcode.com "Leetcode homepage"

[2]: http://www.cnblogs.com/DerekKen/p/6819390.html "DerekKen的博客园"
