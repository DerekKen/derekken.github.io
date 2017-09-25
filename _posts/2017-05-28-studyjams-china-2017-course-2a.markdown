---
layout:     post
title:      "Android 创建交互式应用:2A课程笔记 StudyJams China 2017"
subtitle:   "Android Interactive App:Course 2A Notes of StudyJams China 2017"
date:       2017-05-28 00:32
author:     "Derek Ken"
header-img: "img/in-post/post_studyjams_china2017/course_2a.jpg"
header-mask: 0.35
catalog:    true
comment:    true
tags:
    - Android
    - StudyJams
---

> 本文首发于 [DerekKen的博客园](http://www.cnblogs.com/DerekKen/p/6914826.html)与[StudyJamsChina](https://www.studyjamscn.com/thread-21719-1-1.html)，旨在分享个人在参与Google StudyJams China 2017活动时的点滴收获，这也是StudyJams的精神所在。

# **课程2A**

## **概述**
- 课程2A、2B的内容主要是关于创建交互式应用的基础知识。之前的L1课程主要是Android UI的基础设计知识，基本上没涉及到编程。 2A的讲解主要包括：使用变量来更新欲显示在屏幕上的内容，为按钮添加事件响应(联系XML属性与Java方法)逻辑等。
- 从2A开始，后续的课程会逐步深入地讲解使用Java开发基本Android程序需要掌握的语言知识、数据库知识、编程技巧以及面向对象编程思想等等，大家一起加油!

## **交互**
- 为了在Java方法中与视图布局中的UI对象进行交互，最好在XML文件中定义该对象的id。这样，在Java代码中就可以直接通过访问这些UI对象，非常方便。


## **变量**
- 顾名思义，变量(variables)的作用是存储可变的"量"，方便程序员实现开发的目标。作为编程语言中一个十分基本的概念，变量在编程中不可或缺。 与字面值(literals)相比，变量具有灵活的特点，而且很多时候只有变量才能满足正确实现程序逻辑的需要。
- 变量 vs 字面值：当需要更改值的时候，所有相同的字面值都需更改；而对于变量来说，只需在变量赋值处更新该值。
- 执行创建变量的代码后，内存中会开辟出一段空间(视变量的类型而定)，用以存储变量中的值，程序员可以在需要的时候更改该值，用以实现正确的程序逻辑。
- 变量的声明与定义。对于强类型的编程语言，声明变量的基本语法为：类型 变量名；声明的同时还可以初始化变量，这两个操作合起来即为变量的定义：

```java
int numberOfCoffees = 2;
```

&ensp;&ensp;&ensp; 注意运算符"="的左右都有空格的细节，这涉及到代码风格的问题。一个良好的代码风格应该具有合适的缩进、运算符左右的空格、适时的换行等，这样可以使得代码更加清晰，可读性更强。在平时编程中，应该注意养成良好的代码风格。清晰的代码对于减少BUGs，降低调试难度也有一定帮助。
 
 
## **练习**	
- 选择视图：<br>
&ensp;&ensp;&ensp; 1. 列出自己打算使用的所有视图；<br>
&ensp;&ensp;&ensp; 2. 确定视图位置(比较关键的是确定使用哪种视图组作为根视图)；<br>
&ensp;&ensp;&ensp; 3. 设置视图样式(textSize，FontFamily等属性)；<br>

- 为按钮添加事件响应函数：对于单击事件，在XML的某个按钮标签中引入属性onClick，属性取值为Java代码中对应的方法的名字。这样，就可以把单击事件处理函数与该按钮绑定，实现交互。

- 使用伪代码，使自己的思路可以更加清晰。 **不至于迷失在代码实现的繁琐细节之中**。

- 调试练习：<br>
&ensp;&ensp;&ensp; 1. DEBUG：指消除程序中的BUG的调试过程。<br>
&ensp;&ensp;&ensp; 2. Compile Time Error：编译时错误，包括常见的语法错误(代码不符合语言的语法规定，比如未匹配的括号、一条语句的最后缺少分号等等)、语义错误(比如操作符与操作数类型不匹配)等；还包括找不到所引用的文件(C++中的.h文件、lib静态库、dll动态库，Java中的Jar包)的错误。<br>
&ensp;&ensp;&ensp; 3. Runtime Time Error：运行时错误，包括由逻辑错误、数组访问越界、空指针等在运行时引起的错误。此类错误一般比编译时错误更难解决，特别是逻辑错误。所以，在写具有较复杂逻辑的代码前，程序员自身必须把整个程序执行的流程想清楚。否则，调试代码的时间会远远超过想清楚之前直接写代码"节省"下的时间。<br>
&ensp;&ensp;&ensp; 4. System Log: 系统日志，Android开发中常用logcat这个工具来分层次、分类型地显示不同等级的日志，方便程序员查找感兴趣的信息(错误信息或者更琐碎、更底层的信息)。<br>
&ensp;&ensp;&ensp; 5. Stacktrace: 调用栈的追踪，非常有用的一个特性，能够显示函数的调用关系(按照栈的数据结构，最后调用的函数显示在栈顶，即最上方)。 Stacktrace常常用来分析异常链，查找错误的源头，能够直接定位到代码中引起错误的行。<br>

- 全局变量 or 局部变量？：<br> 
&ensp;&ensp;&ensp; 1. global variable：全局变量，在整个源文件中都有效。<br>
&ensp;&ensp;&ensp; 2. local variable：局部变量，在定义该变量的上下文范围内有效；在该范围之外，该变量的生命周期结束，不能够再被引用。<br>
&ensp;&ensp;&ensp; 3. variable scope：变量作用域，分为全局的与局部的，具体解释如上。<br>
注意：在Android Studio中，默认编辑器设置下，全局变量名会加粗显示，便于程序员区分。了解这一点之，可以减少了使用同名局部变量覆盖(override,hide)全局变量而引入BUG的可能。

---

[1]: https://classroom.udacity.com/me "Udacity Android Courses"

[2]: https://www.studyjamscn.com/thread-20263-1-1.html "Google StudyJams China 2017"

[3]: http://www.cnblogs.com/DerekKen/p/6819390.html "DerekKen的博客园"
