---
layout:     post
title:      "Android 创建计分牌应用:2C课程笔记 StudyJams China 2017"
subtitle:   "Scoreboard App:2C Notes of StudyJams China 2017"
date:       2017-05-28 15:27:00
author:     "Derek Ken"
header-img: "img/in-post/post_studyjams_china2017/course_2c.jpg"
header-mask: 0.45
catalog:    true
comment:    true
tags:
    - Android
    - StudyJams
---

> 本文首发于 [DerekKen的博客园](http://www.cnblogs.com/DerekKen/p/6915800.html)与[StudyJamsChina](https://www.studyjamscn.com/thread-21735-1-1.html)，旨在分享个人在参与Google StudyJams China 2017活动时的点滴收获，这也是StudyJams的精神所在。

# **课程2C-实践：创建交互式应用**

## **概述**
- 课程2C的内容主要是练习巩固2A、2B中讲解的内容，并设计实现一款篮球比赛的计分板应用及其界面的美化。

## **Warm-Up：准备活动**

- 新建项目PracticeSet2(包名android.example.com，Minimum SDK：API 15，Empty Activity)，主要练习了int型变量的声明和初始化。

- 这部分练习要想实现的功能是计算一个人一周的睡眠时间与推荐值之间的差距。课程中的代码计算过程有一个逻辑错误：只计算了一个工作日(weekday)的睡眠时间，而漏掉了剩下4天工作日的睡眠时间。<br />
课程中介绍：通过手动模拟程序运行(hand simulation)的方法，可以帮助程序员避免逻辑错误。主要的思路是比较"what the program does"与"what we actually do"

- 接下来的一些练习有计算通勤者花在路上的时间、计算购物清单总价等等，它们都是为了帮助初学者修复或者避免代码中的逻辑错误。

- 第三部分(Part 3)的练习的主题是作用域(scope)。在HealthyLiving(健康生活)这一块儿的练习中，解释了为什么不使用全局变量：a)使用到当前变量的地方并没有跨方法(即该变量只在一个方法中用到)；b)该变量存储的是一些中间值，更新的频率很高，不适于共享，因此也就不适于使用全部变量；3)可以避免错误：滥用全局变量的话，有可能引入副作用(side effects，在程序设计的语境中，表示发生了程序员不知道且不期望的行为)。即全局变量的值可能在其他地方“不小心”地被更改了，从而引入BUG。<br />
关于全局变量与局部变量的选取问题，有一个基本原则：仅在必要的时候使用全局变量。一个简单的判断方法是，当你发现不用全局变量无法实现期望的功能时，就说明此时全局变量的使用应该是必要的。



## **CourtCounter：篮球计分板应用**

&ensp;&ensp;&ensp; a) 首先介绍了一些新的Android XML属性，TextView控件的gravity属性：指定文本的对齐方式，如“水平居中”、“垂直居中”等。<br />
&ensp;&ensp;&ensp; b) 关于padding(内边距)的提示：在Button控件中，如果指定了过大的padding值，那么按钮本身也会变大! 所以，最好使用margin(外边距)属性来控制界面布局中控件之间的边距。<br />
&ensp;&ensp;&ensp; c) 引入按钮单击事件的响应函数：把.xml与.java文件联系起来。<br />
&ensp;&ensp;&ensp; d) 开启Android Studio中的Auto Import功能：可以自动在写代码的时候引入相关的Java Package，提高开发效率。<br />
&ensp;&ensp;&ensp; e) 实现更新队伍得分的逻辑：推荐先写一写伪代码，理清思路再动手写代码，往往比想清楚之前直接coding更有效率(虽然这样的结论看起来有些反直觉)。<br />
做完了以上的步骤，我们得到了Team A的计分板界面，在Android Studio中的界面预览如图1所示，在手机上运行的效果如图2所示。<br />
![Fig1. Android Studio界面A的Preview](http://owsep4p7v.bkt.clouddn.com/2c_Fig1.png)
<div style="text-align:center"><b>图1.</b>  Android Studio界面A的Preview</div>
<br /><br />


![Fig2. Team A的界面](http://owsep4p7v.bkt.clouddn.com/2c_Fig2.jpg)
<div style="text-align:center"><b>图2.</b> Team A的界面</div>
<br /><br />

&ensp;&ensp;&ensp; f) 增加另一个队伍Team B之后的界面，用到了嵌套视图组来实现，要是想不清楚如何嵌套，可以先画画层级关系的树状图。新增的Team B的界面在层级关系上与Team A的界面是兄弟关系(siblings)。<br />
![Fig3. Preview增加Team B的界面](http://owsep4p7v.bkt.clouddn.com/2c_Fig3.png)
<div style="text-align:center"><b>图3.</b> Preview增加Team B的界面</div>
<br /><br />

![Fig4. 增加Team B的界面](http://owsep4p7v.bkt.clouddn.com/2c_Fig4.jpg)
<div style="text-align:center"><b>图4.</b> 增加Team B的界面</div>
<br /><br />

![Fig5. 增加Team A、B的比分](http://owsep4p7v.bkt.clouddn.com/2c_Fig5.jpg)
<div style="text-align:center"><b>图5.</b> 增加Team A、B的比分</div>
<br /><br />


&ensp;&ensp;&ensp; g) 重置记分牌：在界面底部居中的位置，增加一个重置记分牌的比分的按钮，需要再次嵌套视图组。从View Groups层级关系上来讲，这里的Button所在的视图组与前Team A、B的视图组也是兄弟关系(siblings)。


&ensp;&ensp;&ensp; h) 美化界面：通过直接在XML中指定16进制的颜色值，增加Team A、B的分隔线，调整padding与margin，修改使用的字体等方法，来美化之前的界面。由于我手机的API Level 为19，无法运行界面美化后的程序，这里只放出界面Preview。<br />

![Fig6. 美化计分板界面](http://owsep4p7v.bkt.clouddn.com/2c_Fig6.png)
<div style="text-align:center"><b>图6.</b> 美化计分板界面 </div>
<br /><br />


![Fig7. 调整分隔线的长度](http://owsep4p7v.bkt.clouddn.com/2C_Fig7.png)
<div style="text-align:center"><b>图7.</b>  调整分隔线的长度 </div>
<br /><br />

---

[1]: https://classroom.udacity.com/me "Udacity Android Courses"

[2]: https://www.studyjamscn.com/thread-20263-1-1.html "Google StudyJams China 2017"

[3]: http://www.cnblogs.com/DerekKen/p/6819390.html "DerekKen的博客园"
