---
layout:     post
title:      "Android中的布局(下):1B课程笔记 StudyJams China 2017"
subtitle:   "Layouts in Android:Course 1B Notes of StudyJams China 2017"
date:       2017-05-07 22:22:00
author:     "Derek Ken"
header-img: "img/in-post/post_studyjams_china2017/course_1b.jpeg"
header-mask: 0.35
catalog:    true
comment:    true
tags:
    - Android
    - StudyJams
---

> 本文首发于 [DerekKen的博客园](http://www.cnblogs.com/DerekKen/p/6822625.html)与[StudyJamsChina](http://www.studyjamscn.com/thread-20363-1-1.html)，旨在分享个人在参与Google StudyJams China 2017活动时的点滴收获，这也是StudyJams的精神所在。

# **课程1B**

## **概述**

- 课程1B主要讲解了Android UI的ViewGroups(视图组)、LinearLayout(线性布局)、RelativeLayout(相对布局)，Portrait Mode(竖屏模式)、Landscape Mode(横屏模式)以及layout_weight(布局权重)在UI布局中的用处。
- 此外，本次课程简要提到了xml命名空间，能够方便变量名的管理和使用以及避免变量名字冲突。

## **ViewGroups**

- 视图组控件引出了parent view、child view以及sibling view的概念；它们分别指的是两个视图间的父、子、兄弟关系，是一个相对概念，至少有两个对象参与。
- 需要注意的是，也是在1B课程中反复强调过的，ViewGroups**本身也是一种视图**。
## **LinearLayout**
- 应用线性布局，首先应当设置布局中元素的朝向(orientation)：具体的取值有vertical、horizontal，分别指定布局中元素按**列**排列和按**行**排列：

```java
android:orientation="vertical"
android:orientation="horizontal"
```
## **RelativeLayout**
	
- 相对布局中的控件中的默认位置是屏幕的最左上方。
- 相对布局并不需要android:orientation属性。
- 相对布局能够以指定相对位置的方式来设置布局中各元素(控件)之间的相对位置，交给开发者自由定制的空间远比LinearLayout大，当然相应地也会拥有更多属性，变得更复杂一些。
- **需要强调**，在应用相对布局进行Android UI设计前，要能够理解相对布局中的"相对"在不同的代码上下文中可能会具有不同的含义。
<br>比如，<br>1. ”相对“指的是相对于父视图：

```java
	android:layout_alignParentTop=“true”
	android:layout_alignParentLeft="true"
	android:layout_alignParentRight="false"
	android:layout_alignParentBottom="false"
	android:layout_centerHorizontal="false"
	android:layout_centerVertical="false"
``` 
<br>

&ensp; &ensp;  &ensp;属性android:layout_centerHorizontal、android:layout_centerVertical也是相对于父视图的，分别设置控件位于父视图的水平居中以及垂直居中的位置。<br>
&ensp; &ensp;  &ensp; 2. ”相对“指的是相对于锚视图(anchor view)：锚视图是固定的，其它视图可以指定与锚视图的相对位置。

```java
	android:layout_toLeftOf=“@id/some_id1_prev_defined”
	android:layout_toRightOf=“@id/some_id2_prev_defined”
```
- [提示1] RelativeLayout的其他参数还有很多，搜索android RelativeLayout layout Params等关键字能够获取到关于相对布局的详细文档或者API参考手册。
开发者应该在平时注意锻炼自己查找资料，解决问题的能力，课程中介绍到的Android Developers就是很好的Android开发的参考网站。

<br>

## **Margin&Padding**

- 外边距(Margin)、内边距(Padding)的概念在UI设计中很早就出现了。
- Padding控制单个控件内部元素和该控件边界之间的距离。
  - 比如说，TextView中的文本与四周边界的距离的控制：
  
```java
android:padding="8dp" 
```
<br>
&ensp;&ensp;&ensp;&ensp;&ensp;	或者控制文本与某一边界之间的距离：

```java
android:paddingLeft="8dp" 
android:paddingRight="8dp"
android:paddingTop="8dp"
android:paddingBottom="8dp"
```
<br>
- Margin属性的使用的前提是，必须位于一个视图组中，否则就没有“外”边距的存在了。即外边距是相对两个父子(parent-child)控件之间而言的。
- 用外边距控制两个控件之间的相对位置：

```java
android:layout_margin="8dp" 
android:layout_marginLeft="8dp"
android:layout_marginRight="8dp"
android:paddingTop="8dp"
android:paddingBottom="8dp"
```
<br />
&ensp;&ensp;&ensp; 第一个表达式与后四个的效果是等价，都是设置两个父子控件之间的**四周**的边距。

- Margin与Padding之间的对比

> 下面这张自己画的图应该能够比较清晰地示意二者的区别，蓝色方块是一个ViewGroups控件，也就是说它是绿色方块的父视图(Parent View)，
这是外边距存在的前提。

<br />
![Fig1.Margin与Padding的对比](http://owsep4p7v.bkt.clouddn.com/Margin&Padding__Cropped.png)
<div style="text-align:center"><b>图1</b>.Margin与Padding的对比</div>

---

[1]: https://classroom.udacity.com/me "Udacity Android Courses"

[2]: https://www.studyjamscn.com/thread-20263-1-1.html "Google StudyJams China 2017"

[3]: http://www.cnblogs.com/DerekKen/p/6819390.html "DerekKen的博客园"
