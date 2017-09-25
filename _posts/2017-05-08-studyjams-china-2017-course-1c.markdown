---
layout:     post
title:      "Android 生日贺卡应用:1C课程笔记 StudyJams China 2017"
subtitle:   "Android Birthday Card App:Course 1C Notes of StudyJams China 2017"
date:       2017-05-08 02:42
author:     "Derek Ken"
header-img: "img/in-post/post_studyjams_china2017/course_1c.jpg"
header-mask: 0.35
catalog:    true
comment:    true
tags:
    - Android
    - StudyJams
---

> 本文首发于 [DerekKen的博客园](http://www.cnblogs.com/DerekKen/p/6822625.html)与[StudyJamsChina](http://www.studyjamscn.com/thread-20363-1-1.html)，旨在分享个人在参与Google StudyJams China 2017活动时的点滴收获，这也是StudyJams的精神所在。

# **课程1C**

## **概述**
- 课程1C是创建一个生日贺卡应用的实践课程，所以本篇笔记分享主要记录个人的实践过程，此外分享一些比较零散的知识点。

## **Drawable文件夹**
- Drawable文件夹是Android项目统一管理绘图资源的文件夹。为了在不同分辨率的设备上保持各元素显示大小的一致性，可以在Drawable文件夹下设置对应不同分辨率图片的各个子文件夹。当加载图片资源时，根据设备的分辨率去选择合适的图片加载。
- 在XML布局文件中引用Drawable文件夹下的资源的语法：

```java
android:src="@drawable/your_resrc_file_name_without_file_extension"
```

## **安装Android Studio**
- Android Studio基于Java开发工具箱(Java Development Kit，JDK)提供的运行时环境，在安装Android Studio之前务必装好JDK。
- 一步步按照课程中的步骤来安装，应该不会遇到什么问题。

## **在手机上运行 Hello World**	
- 首先新建项目(注意选择Empty Activity)：

![Fig1](http://owsep4p7v.bkt.clouddn.com/1C_1_%E6%96%B0%E5%BB%BA%E7%94%9F%E6%97%A5%E8%B4%BA%E5%8D%A1%E9%A1%B9%E7%9B%AE.png)

<div style="text-align:center"><b>图1.</b>新建生日贺卡应用的项目</div>

- 开启USB调试，连接手机后，点击Android Studio界面中的运行按钮，弹出如下的对话框，提示开发者选择运行程序的设备。这里选择连接的手机而不是模拟器。<br>

&ensp; &ensp;  &ensp; 运行效果：


![Fig2](http://owsep4p7v.bkt.clouddn.com/1C_2_%E5%9C%A8%E6%89%8B%E6%9C%BA%E4%B8%8A%E8%BF%90%E8%A1%8CHelloWorld.png)


<div style="text-align:center"><b>图2.</b>在手机上运行Empty Activity</div>


- 比较有意思的是，显示"Hello World!"的过程中我并没有编写一行代码。这是因为现在的Android开发IDE(Eclipse、Android Studio)，对于Empty Activity的项目创建设置，一般都会自动在布局xml文件中生成一个文本为"Hello World!"的TextView。
- Android Studio会默认自动在布局xml文件中生成设置padding属性的代码。不需要的话，可以自行删除。
	
## **设置贺卡中文本的位置**
- 用到的属性**layout_alignParentRight**、**layout_alignParentBottom**、**layout_width**、**layout_height**。
- layout_alignParentRight与layout_alignParentBottom合起来能够将元素设置到父视图右下角的位置。这个比较容易理解。
- 注意，属性**layout_width**、**layout_height**在这里是**必要**的，因为这两个属性能够影响元素占据的屏幕空间。<br>
举例来说，如果一个TextView的宽度属性被设置为match_parent，那么你是**不能**将此TextView中的文本(占据的屏幕空间不到一行)设置到一行的最右边的：

 ![Fig3](http://owsep4p7v.bkt.clouddn.com/1C_3_layout_width&height%E5%9C%A8%E8%AE%BE%E5%AE%9A%E5%85%83%E7%B4%A0%E4%BD%8D%E7%BD%AE%E6%97%B6%E7%9A%84%E5%BF%85%E8%A6%81%E6%80%A7.png)
<div style="text-align:center"><b>图3.</b>layout_width&height在设定元素位置时的必要性 </div>

## **设置贺卡中的图片**
- 为了使图片占满整个手机屏幕，对应的ImageView的宽高都设置成wrap_content
- 自己找了一张图片放到drawable下，文件名为androidcake.jpg
- 设置图片的代码：

```xml
<ImageView
	android:layout_width="match_parent"
	android:layout_height="match_parent"
	android:scaleType="centerCrop"
	android:src="@drawable/androidcake" />
```


## **在styles.xml中自定义颜色**
- 在Material Design Sepc上挑选了自己比较满意的颜色(以16进制的数值表示)，为了在Android UI的布局xml文件中引用这些颜色，需要在项目文件下到**/res/values/styles.xml**文件中添加这些颜色：

```xml
    <color name="lightred">#ef5350</color>
    <color name="darkred">#b71c1c</color>
```

<br>

## **设置字体、文本风格**
- 定义好满意的颜色后，接下来设置文本的颜色、文本风格以及字体：

```xml
<TextView
...
android:fontFamily="sans-serif-medium"
android:textColor="@color/lightred"
android:text="Happy Birthday R9!"
android:textStyle="bold"
... />
<TextView
...
android:textColor="@color/darkred"
android:fontFamily="sans-serif-medium"
android:text="From DerekKen"
android:textStyle="bold"
... />
```

## **效果展示**
- 完成以上的步骤之后，最后自己完成的生日贺卡应用在手机上运行的效果如图所示：
 
 ![Fig4](http://owsep4p7v.bkt.clouddn.com/1C_4_%E8%BF%90%E8%A1%8C%E6%95%88%E6%9E%9C%E5%B1%95%E7%A4%BA.jpg)

<div style="text-align:center"><b>图4.</b>生日贺卡App运行效果展示</div>

---

[1]: https://classroom.udacity.com/me "Udacity Android Courses"

[2]: https://www.studyjamscn.com/thread-20263-1-1.html "Google StudyJams China 2017"

[3]: http://www.cnblogs.com/DerekKen/p/6819390.html "DerekKen的博客园"
