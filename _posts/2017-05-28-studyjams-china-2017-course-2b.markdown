---
layout:     post
title:      "Android 创建交互式应用(下):2B课程笔记 StudyJams China 2017"
subtitle:   "Android Creating an Interactive App:2B Notes of StudyJams China 2017"
date:       2017-05-28 02:15:00
author:     "Derek Ken"
header-img: "img/in-post/post_studyjams_china2017/course_2b.jpg"
header-mask: 0.3
catalog:    true
comment:    true
tags:
    - Android
    - StudyJams
---

> 本文首发于 [DerekKen的博客园](http://www.cnblogs.com/DerekKen/p/6914885.html)与[StudyJamsChina](https://www.studyjamscn.com/thread-21721-1-1.html)，旨在分享个人在参与Google StudyJams China 2017活动时的点滴收获，这也是StudyJams的精神所在。

# **课程2B-创建交互式应用(下)**

## **概述**
- 课程2B的内容主要包括：使用变量来更新欲显示在屏幕上的内容，为按钮添加事件响应(联系XML属性与Java方法)逻辑等。
- 后续的课程会逐步深入地讲解使用Java开发基本Android程序需要掌握的语言知识、数据库知识、编程技巧以及面向对象编程思想等等，大家一起加油!

## **Polishment-修饰原有布局**

- 课程2B首先着眼于改进2A中"蜷缩"在屏幕左上部分的咖啡订购布局。

- 从这种狭窄的垂直长条形布局"解脱"出来有两个好处 <br />
&ensp;&ensp;&ensp;  1) 用户能够更快地速览(scan over)整个布局，而之前的长条形布局在纵向上的内容太多；<br />
&ensp;&ensp;&ensp;  2) 能够更多地利用水平方向上的空间，减少视觉上的突兀感，使得界面更加美观。<br />

- 按照之前讲过的界面设计"三部曲"(选择视图->放置视图->设置视图风格)的套路：<br />
&ensp;&ensp;&ensp;  1) 选择视图：保持原有的视图控件不变；<br />
&ensp;&ensp;&ensp;  2) 设置视图的位置：即Header、Button以及TextView之间的位置；<br />
&ensp;&ensp;&ensp;  3) 设置视图风格：除了设置各种Views控件的align属性，还需注意TextView与Button控件之间的间距(用padding或者margin实现，但最好用margin，**因为过大的padding可能会增大按钮的宽高**)等细节。<br />

- Nested ViewGroups-嵌套视图组的使用<br />
&ensp;&ensp;&ensp;  a) 一个ViewGroup中可以嵌套另外的ViewGroup，开发人员可以灵活使用嵌套视图组，以达到预期的视觉效果；<br />
&ensp;&ensp;&ensp;  b) 理论上，可以做无数层的ViewGroups嵌套，但是，最好不要滥用视图组的嵌套：仅在必要的时候使用视图组的嵌套。因为过多的嵌套层数对程序性能来说十分不利：Android会花费较长时间来(递归地)计算每个控件的精确位置。<br />
- **建议**：为了正确地使用并不直观的XML代码中视图组嵌套的方法来达到期望的视觉效果，可以使用事先画出视图层级草图的办法来帮助理清视图组嵌套的层次关系。<br />
**步骤**：设计界面布局 ----> 画出界面的Views的树状图 ----> 搭建XML中视图组层次关系的"骨架"(skeleton)
 
## **String类型的变量**

- 在Java代码中使用String类型的变量，可以**避免字符串硬编码(hard-coded)**于XML源文件中。硬编码的字符串，一旦需要更改，则所有具有相同字面值的字符串都需要更改。

- 声明String类型的变量 <br />
&ensp;&ensp;&ensp;  a)变量取名：尽量做到“见名知意”; <br />
&ensp;&ensp;&ensp;  b)转义字符(escape sequence)：如果想在字符串字面值中显示一些特殊的字符(换行、回车、制表符等)，需要在字面值中使用转义字符，如图1所示。<br />
<center> ![Fig1. 转义字符](http://images2015.cnblogs.com/blog/1161127/201705/1161127-20170528021359266-198222842.png)</center>
 <center>**图1.** 转义字符 </center>
<br /><br />

- String Concatenation_字符串拼接： <br />
 &ensp;&ensp;&ensp;  a)字符串与字符串之间的拼接，可以是String类型的变量，也可以是字符串字面值; <br />
 &ensp;&ensp;&ensp;  b)字符串与其他类型变量的拼接：比如字符串与int类型的变量之间的拼接： <br />
 
```java
String str = "String Concatenation";
int num = 666;
System.out.println(str + " with an interger:\t" + num);
```

&ensp;&ensp;&ensp; 以上代码会输出**String Concatenation with an interger:&nbsp;&nbsp;&nbsp;&nbsp;666**并换行。在将以上Java代码编译成字节码(Byte Code)时，编译器对变量num进行了隐式自动类型转换：将其转换成了String类型的变量。

---

[1]: https://classroom.udacity.com/me "Udacity Android Courses"

[2]: https://www.studyjamscn.com/thread-20263-1-1.html "Google StudyJams China 2017"

[3]: http://www.cnblogs.com/DerekKen/p/6819390.html "DerekKen的博客园"
