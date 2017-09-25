---
layout:     post
title:      "Android 面向对象编程(上):3A课程笔记 StudyJams China 2017"
subtitle:   "Android Object-oriented Programming:3A Notes of StudyJams China 2017"
date:       2017-05-28 23:53:00
author:     "Derek Ken"
header-img: "img/in-post/post_studyjams_china2017/course_3a.jpg"
header-mask: 0.45
catalog:    true
comment:    true
tags:
    - Android
    - StudyJams
---

> 本文首发于 [DerekKen的博客园](http://www.cnblogs.com/DerekKen/p/6917043.html)与[StudyJamsChina](https://www.studyjamscn.com/thread-21766-1-1.html)，旨在分享个人在参与Google StudyJams China 2017活动时的点滴收获，这也是StudyJams的精神所在。

# **课程3A-面向对象编程(上)**

## **概述**
- 面向对象的思想在当今的软件开发中占据着主导地位。
- Java是一门完全面向对象的语言，是一种天然的分布式互联网软件的开发语言，在当今企业级应用中占据绝对领先地位，也是开源世界的顶梁柱。
- 课程3A的内容主要是介绍面向对象编程思想的一些基本概念。

## **Warm-Up：准备活动**

- 练习定义方法，调用方法。这个练习首先修改了MainActivity.java中的display()方法的名字，然后修复代码中的语法错误：修改之前所有对于display()方法的调用为当前的方法名。这个练习的目的主要是想让学生熟悉方法定义和调用的过程以及这两者之间的一一对应的关系。

  - 在 Android Studio 中打开方法声明的键盘快捷键为：Mac：command+b，Windows：control + b。
  
  - 定义一个方法的需要哪些部分？<br />
   a) Access Modifier(Accessibility Specifier)，访问控制修饰符。经常使用的是"private"与"public"，当使用前者时，表明此方法是私有方法，只能在当前类的上下文(在这里，即为MainActivity)中被调用；当使用后者时，表明当前方法具有全局的可访问性，即在代码中的任何位置都可以调用。<br />
   b) Return Data Type，返回值类型。这部分指定当前方法的返回值类型。<br />
   c) Method Name，方法名称。与我们之前使用变量名来引用一个变量类似，我们也可以使用方法名(和传入参数)来调用定义好的方法。<br />
   d) Matched Parentheses，匹配的圆括号。匹配的圆括号中的是实参列表(声明或定义方法时)与形参列表(调用方法时)，调用方法时，必须要有匹配的圆括号，否则编译时会提示语法错误。<br />
   e) Parameter List，参数列表，以逗号分隔，实参列表中的变量名可以在整个当前函数的范围内使用，出了该范围，这些变量都不可以再被引用。形参列表中的传入参数需要具有相同或者是相容的类型(以便编译器能够自动进行隐式类型转换)，变量名不必与对应的实参变量相同。<br />
   f) Matched Curly Braces，匹配的花括号，表示当前函数的范围。
   g) Method Signature，方法签名。方法签名由方法名、参数列表构成。Method Signature与方法重载的概念紧密相关：只有具有不同方法签名的方法能够同时存在于一个上下文中，仅仅只是返回值类型不同的方法不能够重载。
   
- 使用方法的流程： 确定方法签名以及返回值类型，作为方法的声明 ----> 在成对的花括号代表的语句块中实现当前方法的逻辑 ----> 在需要的地方调用方法 ----> 如果需要利用被调方法的返回值，则对该返回值进行处理。

- 进行了以上练习后，JustJava程序在手机上运行的效果如图1所示。<br /> 

![Fig1. JustJava：生成订单信息小结](http://owsep4p7v.bkt.clouddn.com/3a_00__createOrderSummary%EF%BC%8C%E7%84%B6%E5%90%8E%E5%9C%A8%E5%B1%8F%E5%B9%95%E4%B8%8A%E6%98%BE%E7%A4%BA%E8%AE%A2%E5%8D%95%E6%B1%87%E6%80%BB.jpg)
<div style="text-align:center"><b>图1.</b>  JustJava：生成订单信息小结 </div>
<br /><br />


## **Android项目的资源文件**

- 资源文件包括图片、音频、XML文件(布局和项目配置)、字符串文件等等。

- 使用资源文件可以将程序的逻辑与程序具体展现形式分离开来。比如想要做APP的国际化时，就可以在各个语言各自的字符串文件之间切换， 非常方便；想要适应高清屏幕时，只需加载同一资源(图像、视频)的更高清版本。

- 另一方面，Java代码负责程序逻辑的实现，与资源文件之间是松耦合的关系，提升了代码及资源文件的复用性。如果把资源都硬编码在代码中，整个项目会显得比较混乱，不利于缩短开发周期，也不利于项目的维护和迭代。

- 在使用Java来开发Android项目时，会生成一个R.java文件，其中对res资源文件中的资源进行了编号，方便在Java代码中访问这些资源。对于string字符串类型的资源，访问的语法为**R.string.*** (“\*”即为对应的资源文件名)；对于layout布局类型的资源，访问的语法为**R.layout.***。

- 在Java文件与xml文件中都可以访问资源文件，具体方式如图2所示。<br />
![Fig2. 访问资源文件](http://owsep4p7v.bkt.clouddn.com/3a_01__%E5%9C%A8xml%E6%96%87%E4%BB%B6%E4%B8%8Ejava%E6%96%87%E4%BB%B6%E4%B8%AD%E8%AE%BF%E9%97%AEresources.png)
<div style="text-align:center"><b>图2.</b> 访问Android项目资源文件 </div>
<br /><br />

## **对象、类、继承**

- 当在onCreate()方法中调用setContentView()方法时，

```java
setContentView(R.layout.activity_main);
```

我们通过R这个对当前所有的项目资源的抽象的类来访问布局资源activity_main.xml，Android程序执行到这一语句时会解析此xml文件，分析各个Views之间的层级关系并据此生成对应的Java对象。

- **Java对象**：可以拥有成员(变量或方法)，其整体是对State的封装，外界(凡是无法直接访问此对象内部的，对于该对象而言都可称为“外界”)可以使用此对象提供的一些方法(比如说，setter方法与getter方法)来修改其成员变量，从而改变此对象的状态。外界可能根据对象状态的改变进而采取不同的操作，实现期望的逻辑。

- **Java类**
 1. member variable == field == state，成员变量、域、状态等术语在当前语境(Java Class)下的含义相同。<br />
 2. 成员变量的命名规范(naming conventions)：成员变量的名字以"m"或者"m_"作为前缀。<br />
 3. 与之前说过的定义变量类似，定义一个Java Class时，也需要指定(不指定的话，我记得访问控制默认是protected级别的)当前类的访问控制修饰符(Acess Modifier)。<br />
 4. Constructor，构造函数。构造函数是为了实例化(instantiate)Java类为一个实际存在于内存中的对象，构造函数与普通函数类似，也有参数列表；定义构造函数与定义普通函数的过程类似，但不需要指定返回值类型，其语法格式为“类名 + 参数列表 + 实现类实例化的代码块”。<br />
 5. 如果一个类的定义中没有显式地指定任何构造函数，那么实例化该类时对调用默认构造函数。 需要注意区别无参构造函数默认(default，缺省的)构造函数：当一个类的定义中显式地定义了一个不接受任何参数的构造函数时，那么在不传入参数地实例化这个类时，调用的就是无参构造函数，而不是默认(缺省)构造函数。<br />
 6. Factory Method，工厂方法。除了使用构造函数来创建对象，我们也可以使用工厂方法。更详细地来讲，工厂方法是一种对象创建型的设计模式，其意图在于定义一个用于创建对象的接口，让子类决定实例化哪一个类；效果就是一个类的实例化被延迟到其子类。<br />
 &ensp; 6.1 Factory Method的适用范围： 当一个类不知道它所必须创建的对象的类的时候；当一个类希望由它的子类来指定它所创建的对象的时候；当类将创建对象的职责委托给多个Helper子类中的某一个，且你希望将哪一个Helper子类是代理者这一信息局部化的时候。 如下的代码即应用Factory Method把Toast类的实例化延迟了：等待有具体文本信息的时候再实例化出Toast对象。<br />
 
```java
Toast toast = Toast.makeText(context, text, duration);
```

 <br />

 7. 注意，在一个class内部与外调用方法的区别: **a)**class之外无法访问private方法；**b)**语法上的区别。类中调用方法可以不指定当前对象(this)，而在类外调用则必须指定。如图3所示。<br />
 ![Fig3. 在类的内部与外部调用类方法的区别](http://owsep4p7v.bkt.clouddn.com/3a_02__%E5%9C%A8class%E5%86%85%E5%A4%96%E8%B0%83%E7%94%A8%E6%96%B9%E6%B3%95%E7%9A%84%E5%8C%BA%E5%88%AB.png)
<div style="text-align:center"><b>图3.</b> 在类的内部与外部调用类方法的区别 </div>
<br /><br />


 8. Object Method，对象方法。 通过调用对象方法(object method)在Java代码中改变Views的属性，使得我们可以**运行时**根据用户的交互，动态地改变Views的外观。这对于交互式的APP来说十分重要。<br />
 
 9. Inheritance，继承。当一个类A继承另一个类B时，默认地，A就会拥有B的所有public方法与成员(无法继承private的方法与成员变量)。子类可以复用继承而来的方法、变量，也可以重写(override)父类的方法。 通过继承，可以实现多态性，使得程序设计更加灵活、强大。继承是OOP(Object Oriented Programming，面向对象编程)中非常重要的一环；用类图可以展现整个软件系统的继承层次关系，现代软件项目的设计基本上没有脱离了类图的。 <br />
 
 10. Casting，转型。 方法findViewById()返回的对象类型是View；但如果传入的id是一个View的子类的id，为了正确使用该方法的返回值，我们需要进行转型，将findViewById()的返回值转型成为该id对应的实际的对象类型(可以通过查看xml源文件来得到该信息)。关于Java中转型的更多知识，可以参考 [ORACLE官方文档_Inheritance](https://docs.oracle.com/javase/tutorial/java/IandI/subclasses.html) (请参阅“Casting Objects”部分)。 <br />

---

[1]: https://classroom.udacity.com/me "Udacity Android Courses"

[2]: https://www.studyjamscn.com/thread-20263-1-1.html "Google StudyJams China 2017"

[3]: http://www.cnblogs.com/DerekKen/p/6819390.html "DerekKen的博客园"
