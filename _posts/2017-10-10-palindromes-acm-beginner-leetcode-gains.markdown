---
layout:     post
title:      "Leetcode练习笔记(1) Strings&Palindromes 字符串与回文"
subtitle:   "Strings & Palindromes, gains of leetcode practice"
date:       2017-10-11 15:50:00
author:     "Derek Ken"
header-img: "img/in-post/post_studyjams_china2017/leetcode-gains-01.jpg"
header-mask: 0.64
catalog:    true
comment:    true
tags:
    - Leetcode
    - Palindromes
    - Algorithms
---

> 今天练了练《算法竞赛入门经典(第2版)》上的例题(实际上来自[UVa Online Judge](https://uva.onlinejudge.org/index.php))与[Leetcode](https://leetcode.com)上的问题。

# **字符串与回文(strings and palindromes)练习总结**

## **回文词(Palindromes, UVa401)**

- 题目Problem

输入一个字符串，判断它是否为回文串以及镜像串。输入字符串保证不含数字0。所谓
回文串，就是反转以后和原串相同，如abba和madam。所有镜像串，就是左右镜像之后和原
串相同，如2S和3AIAE。注意，并不是每个字符在镜像之后都能得到一个合法字符。在本题
中，每个字符的镜像如图1所示（空白项表示该字符镜像后不能得到一个合法字符）。

![1](http://owsep4p7v.bkt.clouddn.com/blog/posts/img/acm-beginner-mirrored-chars-3-3.jpg)
<div style="text-align:center"><b>Fig1.</b> alphanumeric镜像字符表 </div>

输入的每行包含一个字符串（保证只有上述字符。不含空白字符），判断它是否为回文
串和镜像串（共4种组合）。每组数据之后输出一个空行。

**样例输入**：

NOTAPALINDROME

ISAPALINILAPASI

2A3MEAS

ATOYOTA

**样例输出**：

NOTAPALINDROME -- is not a palindrome.

ISAPALINILAPASI -- is a regular palindrome.

2A3MEAS -- is a mirrored string.

ATOYOTA -- is a mirrored palindrome.

- 分析Analysis

由于题干中说明了输入不包含空白字符，所以可以使用scanf进行输入，不必担心其“吞掉”space、tab、CRLF(LF)等。
可以用一个常量数组来存储镜像字符("Reverse"一列下的字符，没有的需要用空格代替)，这样能够简化代码。
关于回文串的判断，可以先获取输入的字符串的长度len；由于不含空白字符，所以可以直接计算出字符串中左右对称字符的位置，
如果当前左边字符的索引为i，那么与其对称的字符的索引为(len - 1 - i)，其中(len - 1)是最右端字符的索引，减去‘i’可以理解
为往左数第i个字符，与左边的字符对应。类似地，借助常量数组，可以方便地判断一个字符是否为镜像字符。


- 代码Code

[在Github上获取代码/On Github](https://github.com/DerekKen/Algorithms-Coding-Practice/blob/master/practice/Palindromes-UVa401.c)

<div style="text-align:center"><b>Prog1.</b> Palindromes-UVa401 </div>

```c
#include <stdio.h>
#include <string.h>
#include <ctype.h>
const char  rev[] = "A   3  HIL JM O   2TUVWXY51SE Z  8 ";
//order of the following 4 strings could be tricky, see "msg[m *2 + p]"
const char* msg[] = { "not a palindrome", "a regular palindrome", "a mirrored string", "a mirrored palindrome" };

char get_rev(char ch)
{
	if (isalpha(ch))
		return rev[ch - 'A'];
	else //num
		return rev[ch - '0' + 25];//"25" is the offset of numbers in rev[]
}

int main()
{
	char s[32];
	int p, m;
	while (scanf("%s", s) == 1)//constantly waiting for input
	{
		int len = strlen(s);
		p = 1; m = 1;
		for (int i = 0; i < (len + 1) / 2; ++i)
		{
			if(s[i] != s[len - 1 - i]) p = 0;
			//if (rev[i] != get_rev(s[i])) m = 0; rev is a const array 
			if (s[len - 1 - i] != get_rev(s[i])) m = 0;
		}
		printf("%s -- is %s.\n", s, msg[m * 2 + p]);
	}
	return 0;
}
```

- 总结与收获Gains

函数get_rev()返回传入字符的镜像字符，头文件<ctype.h>中的函数isalpha()可以判断传入的字符是否为英文字母。
由于常量字符数组rev是按照A-Z、1-9的顺序进行初始化的，所以ch - ’A‘得到的结果就是字符ch的镜像位于数组rev的偏移(下标)；
类似地，ch - '0' + 25可以得到数字字符在rev数组中的下标。
变量p以及m既是判断字符串是否为回文及镜像串的标志，也是打印输出时，选择字符串的变量，(m * 2 + p)的结果作为下标恰好能选择
正确的字符串用于输出；注意常量字符串数组(i.e. 二维字符数组)msg的初始化顺序很重要，如果"a regular palindrome"与"a mirrored string"对调一下，
则输出时msg的下标值应为(p * 2 + m)。



- Tips

> 灵活运用常量数组可以起到简化代码的作用。定义常量数组时不需要指定大小，编译阶段会进行计算，不影响代码执行速度。


## **Leetcode 125. Valid Palindrome**

- 题目Problem

[See This Problem on Leetcode](https://leetcode.com/problems/valid-palindrome/description)

Given a string, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.

For example, 
**"A man, a plan, a canal: Panama"** is a palindrome.

**"race a car"** is not a palindrome.

**Note:**
Have you consider that the string might be empty? This is a good question to ask during an interview.

For the purpose of this problem, we define empty string as valid palindrome.

- 分析Analysis

如上所述，注意考虑字符串可能为空的情况，且本题定义空串为有效的回文。
1. 最开始的思路：由于本题忽略大小写、标点符号以及空格，最直接的想法就是将输入的字符串全部转换为小写（大写），去掉标点符号，
然后获取处理后字符串的长度len，最后比较对称的[i]与[len - 1 - i]处的字符是否相等，一旦发现不等，立即返回false; 否则返回true。

```cpp
#include <cctype>
#include <algorithm>
class Solution {
public:
    bool isPalindrome(string s) 
    {
        string lower_s;
        transform(s.begin(), s.end(), back_inserter(lower_s), ::tolower);
		string rst;
		//get rid of spaces and punctuations
		for(int i = 0; i < lower_s.length(); ++i)
		{
			if((lower_s[i] != ' ') && (!ispunct(lower_s[i])))
				rst += lower_s[i];
		}
		
		int len = rst.length();
        for(int i = 0; i < (len+1)/2; ++i)
            if(rst[i] != rst[len - 1 - i]) 
                return false;
        return true;
    }
};
```

通过<algorithm>中的transform()函数将输入的字符串全部转换为小写，<cctype>中的函数ispunct()可以判断字符是否为标点符号；
rst只拼接非标点、非空白的字符，从而得到只含数字、字母的字符串。如上代码提交后的运行时间在9ms左右，还有提升空间。

**值得说明的是**，对于空串，代码运行时不会进入循环体，从而直接返回true，符合题目要求。


2. 查看运行详情时发现，本题提交后最快的运行时间为6ms左右，范例代码的思路：对于输入的字符串，初始化两个索引i = 0，j = s.length() - 1，即分别位于字符串开头和结尾。
随后的重点是这两个索引同步变化：i不断加1直到当前位置的字符为数字或字母，j不断减1直到当前位置为数字或字母，然后比较[i]、[j]处的字符是否相等(如果是大写字母则先转换为小写)，一旦不等，则立即返回false；前述过程不断进行下去，直到i >= j。
与自己最开始的思路相比，这个算法去掉了去除空格、标点等字符的步骤，通过左右两个索引直接找到对称位置上的两个字符，更加简洁。
自己按照这个思路重写一遍后提交，发现运行时间不太稳定，最快6ms，最慢16ms，目前能想到的原因就是服务器负载不稳定。

- 代码Code

```cpp
class Solution {
public:
    bool isPalindrome(string s) 
    {
        for(int i = 0, j = s.length() - 1; i < j; ++i, --j)
		{
			//Find two counterparts
			while(!isValid(s[i]) && (i < j)) ++i;
			while(!isValid(s[j]) && (i < j)) --j;
			if(!compare(s[i], s[j])) return false;
		}
		return true;//applicable for empty string 
    }
    bool isValid(char& ch)
    {
        if(ch >= '0' && ch <= '9' || ch >= 'a' && ch <= 'z' || ch >= 'A' && ch <= 'Z')
            return true;
        else 
            return false;
    }
    bool compare(char& a, char& b)
    {
        if(a >= 'A' && a <= 'Z')
            a = a - 'A' + 'a';//to lower case
        if(b >= 'A' && b <= 'Z')
            b = b - 'A' + 'a';
        if(a == b) return true;
        else return false;
    }
};

```

<div style="text-align:center"><b>Prog2.</b> Leetcode 125. Valid Palindromes </div>

**值得说明的是**，对于空串，代码运行时不会进入循环体，从而直接返回true，符合题目要求。

## **Leetcode 9. Palindrome Number**

- 题目Problem

[See This Problem on Leetcode](https://leetcode.com/problems/palindrome-number/description)

Determine whether an integer is a palindrome. Do this without extra space.

**Some hints:**
Could negative integers be palindromes? (ie, -1)

If you are thinking of converting the integer to string, note the restriction of using extra space.

You could also try reversing an integer. However, if you have solved the problem "Reverse Integer", you know that the reversed integer might overflow. How would you handle such case?

There is a more generic way of solving this problem.


- 分析Analysis

1. 首先，负数一定不是回文，因为位于数字最左端的负号'-'不会跟右边的字符相等；
2. 其次，最直接的想法的将数字转化为字符串，然后就可以像之前一样方便地直接比较处于对称位置的[i]与[len - 1 - i]处的字符是否相等；**但是**，本题要求不能使用额外的空间
（不过"Do this without extra space."的表述多少还是有些不准确，因为在函数中定义局部变量也可以被评判系统接受）。
3. 可以考虑将数字翻转，然后与原数字比较，如果相等则该数字是回文数字；但是这样可能会有溢出的问题，比如2147483647翻转后就会溢出。
4. 为了应对溢出的问题，可以只翻转一半的数字。那么如何知道已经翻转了一半呢？当数字的左半部分小于等于右半部分的时候，说明已经翻转了一半的数字。


- 代码Code

```cpp
class Solution {
public:
    bool isPalindrome(int x) {
        // Non-zero numbers with their last digits equaling to ZERO 
        // and negative numbers are not palindromes.
        if(x < 0 || (x%10 == 0 && x != 0)) return false;
        int reverted_num = 0;
        while(x > reverted_num)
        {
            reverted_num = reverted_num * 10 + x % 10;
            x /= 10;
        }
        // Note that when the number of digits is odd(e.g. 78987, when the while loop ends,
        // reverted_num = 789 and x == 78), and obviously getting rid of the middle digit
        // does NOT matter.
        return (x == reverted_num) || (x == reverted_num/10);
    }
};
```

- 总结与收获Gains

x % 10得到原数字的个位，x /= 10的作用是去掉当前x的最后一位数字，reverted_num * 10起到进位的作用。
例如，x = 12321，循环体第一次执行完毕后， reverted_num = 1， x = 1232；第二次执行完毕后，reverted_num = 12， x = 123；
循环体最后一次执行完毕后， reverted_num = 123，x = 12，然后返回true(x == reverted_num/10为真)。
注意到传入的数如果有奇数个数字的话，翻转一半的数字后，得到的数会大于左半部分，**去掉中间的那位数字并不影响结果**。

---

[1]: https://leetcode.com "Leetcode homepage"

[2]: http://www.cnblogs.com/DerekKen/p/6819390.html "DerekKen的博客园"
