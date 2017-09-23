---
layout:     post
comments:   true
title:      "1A课程笔记——StudyJamsChina2017"
subtitle:   "StudyJams China 2017-1A Course Note"
date:       2017-05-07 07:14:00
author:     "Derek Ken"
header-img: "img/in-post/post_studyjams_china2017/course_1a.jpg"
header-mask: 0.3
catalog:    true
tags:
    - Android
	- Google
    - StudyJams
    - 课程笔记
---

# **1A课程**

## **概述**
课程1A主要讲解了Android UI的三种基本控件：TextView、ImageView以及Button。笔记的主体内容主要根据课程内容的讲解顺序来组织，此外我对一些个人比较感兴趣的内容作了一些扩展的说明。希望我的分享能对大家有所帮助。
## **TextView**
- 设置TextView中的字体大小，**推荐使用dp(Density-Independent，(像素)密度无关)作为像素单位**，这样能够使字体大小与<u>[ 屏幕像素密度 ](http://baike.baidu.com/item/%E5%83%8F%E7%B4%A0%E5%AF%86%E5%BA%A6)</u>无关。即显示字体时会根据当前屏幕的像素密度来调整字体实际占据的像素数，像素密度越大的，占据的像素数相应也越大。这样做的最大的好处在于能够保证不同设备(具有不同像素密度的平板、手机、电脑等)上的字体的实际大不会改变，使得开发人员不必为了不同的设备编写不同的代码。
- sp(Scale-Independent，缩放无关)与dp的唯一区别在于：使用sp作为单位指定的字体大小，会使用户的字体尺寸大小("大"、"中"、"小")设置无效。如果你不想让字体大小受到用户设置的影响的话，那么就可以用sp作为像素的单位。
- 设置width、height属性，一般情况下都用wrap_content作为width、height的属性值，使得TextView自适应文本的宽度和高度，免去了手动指定宽高度的麻烦。
- [提示1] 关于字体选取，使用1-3种比较美观的字体即可，如果UI使用的字体太多，很有可能的后果就是用户招架不住，视觉上感到很疲劳。
- [提示2] 考虑**TextAppearance**属性的使用。为了在不同设备间保持界面外观的一致性，可以使用Android预定义好的TextAppearance属性的值。
    - 代码示例
        ```
        android:textAppearance="?android:textAppearanceLarge"
        android:textAppearance="?android:textAppearanceMedium"
        android:textAppearance="?android:textAppearanceSmall"
        ```
<br>

## **XML**
- 课程1A中只是简单提到了几个XML的语法，包括标签(tag)、自封闭(self-closing)标签、属性(attribute)等等。只要跟随课程进度走，勤加练习，掌握XML的基本语法应该是水到渠成的。
> 以下是我想分享的、关于XML的更多内容
- [定义] 可扩展标记语言，它被设计用来传输和存储数据，其焦点是数据的内容。
- [比较] XML与HTML(超文本标记语言)的对比：
        
      |   语言  | 设计思路                    | 角色定位                       |
      | :-----| :-----------------------| :------------------------- |
      |   HTML| 用来显示数据,关注的是数据的**外观**    | 对于XML，具有不可替代性              |
      |   XML | 用来传输和存储数据,关注的是是数据的**内容**| 对HTML的补充                   |
  &ensp; &ensp; &ensp; &ensp; XML与HTML都是标准通用标记语言的子集。

- [XML的应用&个人理解] 
     - XML的应用非常广泛，可以用来描述Android UI的(我认为，实际上就是符合Android规范的、与用户界面相关的结构化数据)；可以用来描述软件项目的结构。比如：JavaEE项目中的web.xml、Visual Studio C/C++项目的*.vcxproj(虽然文件扩展名不是xml，但这里的扩展名只是一件"外衣"罢了，用任何一个文本编辑器打开该文件，从内容上来，用到的语言就是XML)等等都是项目配置文件。
     - 如果足够熟悉的话，你可以通过直接编辑这些xml文件来更改项目属性来达到同样的效果，避免在可视化界面中进行一系列繁琐的操作。进一步地，你可以把一个与具体IDE(集成开发环境，课程1A有简单的介绍，可以对照 <u>[Android for All术语表](https://s3.cn-north-1.amazonaws.com.cn/static-documents/nd803/Android+for+All+%EF%BC%8D+Vocabulary+Glossary.pdf)</u> 来了解)相关的Preferences(首选项、用户偏好)项目配置文件迁移到一个新建的项目，省去重新设置用户偏好的麻烦。这个办法在Eclipse中特别方便实用。
     - 我个人认为，之所以XML广泛用于UI布局文件、项目配置文件的编写，很大程度上是因为XML本身就是被设计来存储和传输结构化数据的；而前述的这些文件恰恰就是需要维护一些UI相关或项目相关的结构化信息的。
<br>

## **ImageView**
 - 属性src指定图像来源(绝对路径、相对路径均可)，layout_width、layout_height指定了该控件的宽高。
 - 属性scaleType通常的取值可以有center和centerCrop。 centerCrop可以达到full-bleed显示的效果，大多数情况下都比较美观，所以裁剪(crop-off)是可以接受的。
<center> ![Fig1. centerCrop_cake的显示效果](http://images2015.cnblogs.com/blog/1161127/201705/1161127-20170507070509054-121512628.png)</center>
 <center>**图1.** centerCrop_cake的显示效果 </center>
<br><br>
<center> ![Fig2. center_cake的显示效果](http://images2015.cnblogs.com/blog/1161127/201705/1161127-20170507070352601-989666601.png)</center> 
<center> **图2.** center_cake的显示效果 </center>


可以看到centerCrop在这里是更合适的属性取值。

## **实用的学习实践资料**
- <u>[Google Material Design](https://material.io/guidelines/style/color.html#color-color-palette) </u>提供了对字体以及颜色选取等方面的参考，此外还有很多UI设计相关的材料。
- <u>[Android for All术语表](https://s3.cn-north-1.amazonaws.com.cn/static-documents/nd803/Android+for+All+%EF%BC%8D+Vocabulary+Glossary.pdf)</u> 对Android术语图文并茂的解释。