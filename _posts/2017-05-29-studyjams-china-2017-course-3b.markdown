---
layout:     post
title:      "Android 面向对象编程(下):3B课程笔记 StudyJams China 2017"
subtitle:   "Android Object-oriented Programming:3B Notes of StudyJams China 2017"
date:       2017-05-29 17:03:00
author:     "Derek Ken"
header-img: "img/in-post/post_studyjams_china2017/course_3b.jpg"
header-mask: 0.45
catalog:    true
comment:    true
tags:
    - Android
    - StudyJams
---

> 本文首发于 [DerekKen的博客园](http://www.cnblogs.com/DerekKen/p/6918244.html)与[StudyJamsChina](https://www.studyjamscn.com/thread-21807-1-1.html)，旨在分享个人在参与Google StudyJams China 2017活动时的点滴收获，这也是StudyJams的精神所在。

# **课程3B-面向对象编程(下)**

## **概述**
- 课程3B的主要内容有：控制流、导航至其他App、支持其他语言(不是编程语言，是自然语言 {:10_443:} )、风格与主题。

## **练习**


- 练习在界面布局中增加一个CheckBox(复选框)，调用方法。我在练习这部分的时候使用了Nested ViewGroups的布局(一个CheckBox与一个TextView在LinearLayout的视图组中，且该视图组嵌套在之前设置的orientation="vertical"的LinearLayout视图组中)；但是后来才发现没必要，因为CheckBox本身就具有text属性，可以设置相关文本。**需要注意**的是，此时设置文本与"复选框"的图形之间的边距必须用padding(内边距)属性，因为文本与"复选框"图形都是属于同一个视图控件CheckBox的。

- boolean的数据类型，只有“真”、“假”两个取值。**只具有两个状态的实体(entity)都可以用boolean类型的变量来抽象**。

- 练习在订单汇总生成的界面加入“是否加入生奶油”的信息。 这里需要用到一个boolean类型的变量，我们通常使用Android开发中常用的Log类的各个方法(代表不同的日志等级)来输出我们期望的中间信息，极大地方便程序员调试程序。

- 读取复选框的状态，并增加到订单信息汇总(order summary)中。连接手机，使用Debug模式调试Just Java App，当复选框没有勾选时，单击"ORDER"按钮，我得到的LogCat的日志输出信息如图1所示。
日志级别我设置的时候info级别的(verbose的输出信息太多，看着晃眼......) 

```java
Log.i("MainActivity", "Has Whipped Cream: " + hasWhippedCream);
```


![Fig1. LogCat的输出信息:false](http://owsep4p7v.bkt.clouddn.com/3b_01_%E4%BD%BF%E7%94%A8Log%E8%BE%93%E5%87%BA%E5%A4%8D%E9%80%89%E6%A1%86%E7%9A%84%E7%8A%B6%E6%80%81.png)
<div style="text-align:center"><b>图1.</b> LogCat的输出信息:false </div>


在我手机上勾选复选框的效果图如图2所示。



![Fig2. 勾选复选框](http://owsep4p7v.bkt.clouddn.com/3b_02_%E6%89%8B%E6%9C%BA%E7%AB%AF%E5%8B%BE%E9%80%89%E5%A4%8D%E9%80%89%E6%A1%86.jpg)
<div style="text-align:center"><b>图2.</b> 勾选复选框 </div>


然后单击"ORDER"按钮，Android Studio中的logcat的输出信息如图3所示。


![Fig3. LogCat的输出信息:true](http://owsep4p7v.bkt.clouddn.com/3b_03_%E4%BD%BF%E7%94%A8Log%E8%BE%93%E5%87%BA%E5%A4%8D%E9%80%89%E6%A1%86%E7%9A%84%E7%8A%B6%E6%80%81_true.png)
<div style="text-align:center"><b>图3.</b> LogCat的输出信息:true </div>

- 练习屏幕画面滚动。当界面的内容超过屏幕大小时，LinearLayout并不会提供画面滚动的功能，而是会直接裁剪掉超出屏幕的部分界面。为了保证在横竖屏模式下均能完整地显示我们界面中的所有内容，需要使整个界面可以滚动。为了达到这一目的，需要用到ScrollView，把ScrollView作为整个界面的RootView即可。

**需要注意的是**，android在xml文件中的标签、属性等都来自于命名空间http://schemas.android.com/apk/res/android，所以需要把对xml中的Android命名空间的设置的代码
  
```xml 
xmlns:android="http://schemas.android.com/apk/res/android
```

**剪切**到当前新的RootView(即ScrollView中)。还有一个对tools命名空间属性的设置：

```xml 
xmlns:tools="http://schemas.android.com/tools"
```

tools命名空间供了额外的属性，它们能够帮助开发人员调试(Debug)与构建(Build)应用程序。实现画面滚动的逻辑后，Just Java App在手机上运行的效果如图4所示。



![Fig4. 测试屏幕画面滚动](http://owsep4p7v.bkt.clouddn.com/3b_04_%E7%94%BB%E9%9D%A2%E6%BB%9A%E5%8A%A8.jpg)
<div style="text-align:center"><b>图4.</b> 测试屏幕画面滚动 </div>



- 增加选择巧克力的复选框。实现逻辑与Whipped Cream的逻辑几乎一模一样，实现之后的运行效果如图5所示。


![Fig5. 测试巧克力复选框](http://owsep4p7v.bkt.clouddn.com/3b_05_%E5%A2%9E%E5%8A%A0%E5%B7%A7%E5%85%8B%E5%8A%9B%E5%A4%8D%E9%80%89%E6%A1%86.jpg)
<div style="text-align:center"><b>图5.</b> 测试巧克力复选框 </div>



- 练习增加文本编辑框，以增加名字输入并在订单汇总中显示的功能。新增的视图EditText，通过查阅Android的官方文档，我们知道通过设置Hint属性来设置文本框的默认提示文本，通过设置属性inputType

```xml 
android:inputType="textPersonName"
```

来设置文本输入的类型为人名。完成这一步后，在我手机上运行的效果如图6所示。


![Fig6. 名字的文本编辑框](http://owsep4p7v.bkt.clouddn.com/3b_06_%E5%A2%9E%E5%8A%A0%E8%BE%93%E5%85%A5%E5%90%8D%E5%AD%97%E7%9A%84_%E6%96%87%E6%9C%AC%E7%BC%96%E8%BE%91%E6%A1%86_EditText.jpg)
<div style="text-align:center"><b>图6.</b> 名字的文本编辑框 </div>

- Control Flow，控制流。在之前的编程练习中，所有的语句都是自上而下地顺序执行的，且写出的每一条语句都会执行。在代码逻辑中引入控制流后，不是写出的所有语句都会执行，而且程序的控制流也不再是顺序的了。
- if/else语句。if/else是Java中实现控制流跳转的基本方法，if与else关键字之后的括号中需要分别输入布尔表达式(boolean expression)，其后紧接的语句或语句块作为代码执行的分支。在程序执行时，只会执行那些满足布尔表达式为真的分支，为假的分支会直接跳过，不执行。if/else语句可以嵌套，以实现复杂的程序逻辑。 至于布尔表达式，可以由关系运算符、逻辑运算符、boolean值、int值等构成；
关于运算符(Operators)的更多介绍，可以参考[Java中的基本运算符](http://www.tutorialspoint.com/java/java_basic_operators.htm)  、 [Oracle 官方Java运算符教程](https://docs.oracle.com/javase/t ... tsandbolts/op2.html)  。

控制流的练习：在计算订单总价时考虑配料(奶油、巧克力)的价格，运行效果如图7所示。


![Fig7. 控制流的练习：在计算订单总价时考虑配料](http://owsep4p7v.bkt.clouddn.com/3b_07_%E6%8E%A7%E5%88%B6%E6%B5%81%E7%BB%83%E4%B9%A0%EF%BC%9A%E8%AE%A1%E7%AE%97%E6%80%BB%E4%BB%B7%E6%97%B6%E8%80%83%E8%99%91%E9%85%8D%E6%96%99%E7%9A%84%E4%BB%B7%E6%A0%BC.jpg)
<div style="text-align:center"><b>图7.</b> 控制流的练习：在计算订单总价时考虑配料 </div>



- Bound Checking，边界处理。软件开发中很重要的一点就是处理好边界条件。在Just Java App中，我们之前没有怎么考虑边界的问题：咖啡的输数量可能为负，很明显这并没有实际意义；另一方面，订购的咖啡数量太多(成百上千)也不现实。所以我们需要处理这种情况，使得Just Java中最少的咖啡订购数量为1，最大的订购数量为100。

```java
final int numMinCoffeeCups = 1, numMaxCoffeeCups = 100;
public void increment(View view)
{
    if(quantity == numMaxCoffeeCups)
        Toast.makeText(this, "You cannot order MORE than 100 cups of coffee.", Toast.LENGTH_LONG).show();
    else quantity += 1;
    display(quantity);
}
public void decrement(View view)
{
    if(quantity == numMinCoffeeCups)
        Toast.makeText(this, "You cannot order LESS than 1 cup of coffee.", Toast.LENGTH_LONG).show();
    else  quantity -= 1;
    display(quantity);
}
```
  边界情况处理之后，上界与下界的情况分别如图8、9所示。


![Fig8. 订购咖啡数量的上界](http://owsep4p7v.bkt.clouddn.com/3b_08_Upper_%E5%92%96%E5%95%A1%E6%95%B0%E9%87%8F%E7%9A%84%E8%BE%B9%E7%95%8C%E6%83%85%E5%86%B5.jpg)
<div style="text-align:center"><b>图8.</b> 订购咖啡数量的上界 </div>





![Fig9. 订购咖啡数量的下界](http://owsep4p7v.bkt.clouddn.com/3b_09_Lower_%E5%92%96%E5%95%A1%E6%95%B0%E9%87%8F%E7%9A%84%E8%BE%B9%E7%95%8C%E6%83%85%E5%86%B5.jpg)
<div style="text-align:center"><b>图9.</b> 订购咖啡数量的下界 </div>


- Intent，意图。在Android中，可以把要完成的活动用包装成Intent，然后调用外部的其他App来实现。常见的Intent有调用外部App实现打电话，发邮件，照相，查看图片，分享内容，查看地图等等。
不难看出Intent是Android框架中非常重要的一环，因为它可以灵活利用其他App的功能。
一个发送给其他Apps的Intent必须包含的内容有Action(表明此意图具体是要干什么，比如打电话、播放音乐等等)、Data URI(数据的统一资源标识符)。练习使用Intent，使用第三方邮件App来将订单汇总的信息发送给指定的收件人。

```java
Intent intent = new Intent(Intent.ACTION_SENDTO);
intent.setData(Uri.parse("mailto:")); // only email apps should handle this
//        intent.putExtra(Intent.EXTRA_EMAIL, addresses);
intent.putExtra(Intent.EXTRA_SUBJECT, "A New Just Java Order for " + yourName);

String orderSummary = createOrderSummary(price, hasWhippedCream, hasChocolate, yourName);
intent.putExtra(Intent.EXTRA_TEXT, orderSummary);

if (intent.resolveActivity(getPackageManager()) != null) startActivity(intent);
else Toast.makeText(this, "There's NO app capable of processing your EMAILING request!", Toast.LENGTH_LONG).show();
```

  由于OrderSummary的信息都随着intent传到了邮件正文中，所以可以在Just Java的界面中把OrderSummary的相关的Views删除掉。
实现通过Intent调用外部App在邮件中发送OrderSummary后，在我手机上运行的效果如图所示。 


![Fig10. 删除ORDER SUMMARY的显示逻辑](http://owsep4p7v.bkt.clouddn.com/3b_10_intent_%E9%82%AE%E4%BB%B6%E5%8F%91%E9%80%81%E8%AE%A2%E5%8D%95.jpg)
<div style="text-align:center"><b>图10.</b> 删除ORDER SUMMARY的显示逻辑 </div>


![Fig11. intent_选择一个App处理Intent的Action](http://owsep4p7v.bkt.clouddn.com/3b_11_intent_%E9%82%AE%E4%BB%B6%E5%8F%91%E9%80%81%E8%AE%A2%E5%8D%95.jpg)
<div style="text-align:center"><b>图11.</b> intent_选择一个App处理Intent的Action </div>



![Fig12. intent_订单汇总信息传到了邮件App中](http://owsep4p7v.bkt.clouddn.com/3b_12_intent_%E9%82%AE%E4%BB%B6%E5%8F%91%E9%80%81%E8%AE%A2%E5%8D%95.jpg)
<div style="text-align:center"><b>图12.</b> intent_订单汇总信息传到了邮件App中 </div>




- Style & Theme， 样式 & 主题。使用样式的一个好处在于，开发人员能够将View的设计(它的视感(Look & Feel)效果)与该View包含的实际内容分离开来，降低了界面设计与界面内容之间的耦合性，从而减少xml中样式代码的重复，提升了xml样式代码的复用性。可以再res/values/styles.xml中自定义styles。样式与主题都是App中以同样方式定义的资源，它们之间的区别在于，style应用于单个view，而theme应用于整个应用程序(application)或者活动(activity)，这意味着主题对于该application或者activity中的所有views都有效。
在版本低于Lollipop的安卓手机上使用theme，需要使用Theme.AppCompat支持库中的主题，而且定义一个Theme.AppCompat主题的语法也有些许的不同。

- 在Material Design Color&Material Design Palette中选取喜欢的颜色，自定义主题后，效果如图所示。

![Fig13. Just Java, Done! ](http://owsep4p7v.bkt.clouddn.com/3b_13_Just%20Java,Done%21.jpg)
<div style="text-align:center"><b>图13.</b> Just Java, Done! </div>


- 比较遗憾的是，colorPrimaryDark设置之后，界面最顶部的标题栏还是原来的颜色，API Level 19(4.4.2,kitkat)。Google了一下"colorPrimaryDark not working"之后找到了最适合自己情况的答案：Android系统版本低于5.0(Lollipop)的不支持自定义notifications bar的颜色。



![Fig14. 不起作用的colorPrimaryDark ](http://owsep4p7v.bkt.clouddn.com/3b_14_colorPrimaryDark%20not%20working.jpg)
<div style="text-align:center"><b>图14.</b> 不起作用的colorPrimaryDark </div>

---

[1]: https://classroom.udacity.com/me "Udacity Android Courses"

[2]: https://www.studyjamscn.com/thread-20263-1-1.html "Google StudyJams China 2017"

[3]: http://www.cnblogs.com/DerekKen/p/6819390.html "DerekKen的博客园"
