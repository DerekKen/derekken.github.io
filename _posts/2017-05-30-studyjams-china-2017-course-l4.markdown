---
layout:     post
title:      "Android Firebase实践:L4课程笔记 StudyJams China 2017"
subtitle:   "Android Firebase in Action:L4 Notes of StudyJams China 2017"
date:       2017-05-30 01:01:00
author:     "Derek Ken"
header-img: "img/in-post/post_studyjams_china2017/course_l4.jpg"
header-mask: 0.45
catalog:    true
comment:    true
tags:
    - Android
    - StudyJams
---

> 本文首发于 [DerekKen的博客园](http://www.cnblogs.com/DerekKen/p/6919416.html)与[StudyJamsChina](https://www.studyjamscn.com/thread-21855-1-1.html)，旨在分享个人在参与Google StudyJams China 2017活动时的点滴收获，这也是StudyJams的精神所在。

# **课程L4-Firebase**

## **Firebase简要介绍**

- Firebase的各个功能
  - **Firebase Analytics**对推送通知分析、运行性能分析、崩溃报告(兼容性分析)、受众群体、不同人群对APP的访问频率、平均盈利分析等报告进行了整合，方便开发人员了解所发布的App在市场上的推广效果、遇到的问题、用户反馈，并作出相应的改进。
	    ![1](http://owsep4p7v.bkt.clouddn.com/l4_0001_Analytics.png)


  - **Firebase Cloud Messaging**， Firebase云消息传递。 向Firebase的云服务器注册用户的应用实例 ---->  在服务器端用代码实现相应的消息传递逻辑(可按指定的类别，如ID、分组、主题等，来向用户应用发送消息) ---->  可以进一步实现消息传递的云服务器向开发人员反馈消息的功能。
  这项服务能够做到低延迟地传递绝大部分的消息，具有延迟低、吞吐量大(并发响应能力强)、可靠性高的特点。
		![2](http://owsep4p7v.bkt.clouddn.com/l4_0002_CloudMessaging.png)



  
  - **Firebase Remote Config**， Firebase远程配置。开发者可以在云端远程地配置所发布的应用，还可以对用户进行分组(user segmentation)，从而对不同类别的用户使用不同的应用配置。 用户分组使得开发者可以有针对性地对特定用户群体作出个性化的App配置，**同时**对一部分用户测试新功能(已决定该功能是否正式上线(对于所有用户))
		![3](http://owsep4p7v.bkt.clouddn.com/l4_0003_Remote_Congif.png)


  - **Firebase Test Lab for Android** 解决了不同的设备众多，难以全面测试的问题。使用Test Lab可以使用Firebase提供的云端的设备库来测试所开发的App，测试完毕后，Firebase会给出详细的测试报告(包括设备日志、测试截图、崩溃报告)。在Android Studio 2.0及以上的版本中，可以方便地直接安装Firebase的 Test Lab 功能。
		![4](http://owsep4p7v.bkt.clouddn.com/l4_0004_TestLab.png)


    
  - **Firebase Crash Reports**，Firebase错误报告按照crashes的相似度分组、并按照错误的严重程度排序，所以开发人员能够迅速知道应该最优先修复哪些错误以减少影响的用户人数，提升App的使用体验。
		![5](http://owsep4p7v.bkt.clouddn.com/l4_0005_CrashReport.png)


  
  - **Firebase Storage**， 同时可以通过Firebase Authentication设置该内容的查看权限(比如未登录的人不能查看)。为Firebase Storag提供支持的是Google Cloud Storage(谷歌云存储)，数据的存储量是PB级别的，所以完全不必担心用户分享的内容占用太多存储空间。
  此外还支持用户分享内容的断点续传功能。
		![6](http://owsep4p7v.bkt.clouddn.com/l4_0006_Storage.png)



  
  - **Firebase Realtime Database**，Firebase实时数据库可以做到毫秒级别的数据同步，在用户设备没有网络连接的时候使用本地缓存来为用户提供数据的相关服务，并且在联网之后自动地进行数据同步。开发者只需要几行代码就可以实现对安全策略的修改：控制用户对数据库的访问权限、最大的内容字符数。
		![7](http://owsep4p7v.bkt.clouddn.com/l4_0007_RealTimeDataBase.png)




  - **Firebase Authentication**，Firebase用户认证可以灵活自由地接入第三方的登录验证系统(Gmail、Facebook、Twitter等等)，甚至可以接入自己开发的登录验证服务，登录之后Firebase会为用户分配一个保证了唯一性的User ID，App使用该ID来决定当前用户对于后台的哪些数据具有访问权限。用户登录后，回调函数会返回该用户的特定信息，可以使用该信息来进行可定制化的欢迎界面设计。
		![8](http://owsep4p7v.bkt.clouddn.com/l4_0008_UserAuthentication.png)



  
  - **Firebase App Indexing**，Firebase应用索引服务可以帮助开发者的App被Google搜索引擎索引，提供在呈现给用户的搜索结果页面上，帮助你推广应用或者使得用户重新参与到你的应用中。

  
## **Firebase实践**

- 在Android上配置好Firebase的环境

  - 首先是前提条件：Android手机中Google Play Service的版本检查，Android Studio中的Google Play Service 与 Google Repository的版本检查。最低的版本要求为 **Android Studio:Google Play Service Rev30, Google Repository Rev9; 手机：Google Play Service Version 9**。
    
    ![1](http://owsep4p7v.bkt.clouddn.com/l4_01_Google%20Play%20Service%E4%B8%8EGoogle%20Repository%E7%89%88%E6%9C%AC%E6%A3%80%E6%9F%A5.png)
	<div style="text-align:center"><b>图1.</b> Android Studio上的版本检查 </div>



	![2](http://owsep4p7v.bkt.clouddn.com/l4_02_%E6%89%8B%E6%9C%BA%E7%AB%AFGoogle%20Play%20Service%E7%89%88%E6%9C%AC%E6%A3%80%E6%9F%A5.jpg)
	<div style="text-align:center"><b>图2.</b> 手机上的版本检查 </div>
    
    
  
  - 连接Firebase与Android App。当把Firebase 下载好的配置文件google-services.json移动至项目路径MyJustJava/app/下之后，就可以修改build.gradle文件来为App添加Firebase的客户端的库。 



	![3](http://owsep4p7v.bkt.clouddn.com/l4_03_%E5%88%B0Firebase%E4%B8%8A%E5%88%9B%E5%BB%BA%E9%A1%B9%E7%9B%AE%28%E8%B7%A8%E5%B9%B3%E5%8F%B0App%E7%9A%84%E5%AE%B9%E5%99%A8%29.png)
	<div style="text-align:center"><b>图3.</b> 下载项目配置文件google-services.json </div>



  - 分别修改项目级与应用级build.gradle文件以导入Firebase SDK(软件开发工具包)的步骤：在项目级build.gradle文件(位于项目根目录下)中，添加一个SDK的路径。

  
	![4](http://owsep4p7v.bkt.clouddn.com/l4_04_%E6%B7%BB%E5%8A%A0Firebase%E8%BD%AF%E4%BB%B6%E5%BC%80%E5%8F%91%E5%B7%A5%E5%85%B7%E5%8C%85%E8%87%B3%E4%BD%A0%E7%9A%84App.png)
	<div style="text-align:center"><b>图4.</b> Firebase配置引导 </div>



  
```java
//Config Firebase SDK package name
classpath 'com.google.gms:google-services:3.1.0'
```

  在应用级build.gradle文件中，新增语句 
```java 
compile 'com.google.firebase:firebase-core:9.6.1' 
``` 

添加引用的Firebase库的依赖关系， 
  在文件的最后添加语句
  
```java
apply plugin: 'com.google.gms.google-services' 
``` 

应用Firebase SDK。 如图5所示。
  
![5](http://owsep4p7v.bkt.clouddn.com/l4_05_%E5%9C%A8%E4%BD%A0%E7%9A%84App%E9%A1%B9%E7%9B%AE%E4%B8%AD%E5%BA%94%E7%94%A8Firebase%20SDK%20%E5%8C%85%28%E6%8F%92%E4%BB%B6%29.png)
<div style="text-align:center"><b>图5.</b> 修改gradle.build文件，以引入Firebase SDK </div>
  


![6](http://owsep4p7v.bkt.clouddn.com/l4_06_Firebase%E5%9C%A8App%E8%BF%90%E8%A1%8C%E6%97%B6%E6%88%90%E5%8A%9F%E5%88%9D%E5%A7%8B%E5%8C%96.png)
<div style="text-align:center"><b>图6.</b> 验证在Android上，Firebase的配置是否正确 </div>
  
  
  - 完成以上步骤后，连接手机进行测试，如果logcat中输出了**"I/FirebaseInitProvider: FirebaseApp initialization successful"**的信息，则说明Firebase成功地连接上了Android App。
  
  


  
- Firebase Notifications on Android，在Android上尝试Firebase的通知推送功能。 
  - 在之前的Firebase课程视频中，我们知道了可以到Firebase官网上查阅目前最新的库的包名，如图所示。
    

	![7](http://owsep4p7v.bkt.clouddn.com/l4_07_messaging_%E6%88%AA%E8%87%B3%E7%9B%AE%E5%89%8D%E6%9C%80%E6%96%B0%E7%9A%84Firebase%E5%BA%93.png)
	<div style="text-align:center"><b>图7.</b>  最新的Firebase库 </div>


  - 为了用Firebase实现通知推送功能，只需要在build.gradle文件的依赖(**见dependencies语句块**)中加入编译对应的库的指令即可。当然，增加此依赖项之后别忘了点击右上角的"Sync Now"来同步项目，如图所示。

	![8](http://owsep4p7v.bkt.clouddn.com/l4_08_%E5%BC%95%E5%85%A5Firebase%20messaging_%E5%BA%93.png)
	<div style="text-align:center"><b>图8.</b>  引入Firebase的云消息推送的库 </div>

  - 随后我们回到浏览器中的Firebase控制台，点击左侧的导航栏中的"Notifications"进入通知推送的界面，然后创建我的第一条通知消息并将其推送给所有使用MyJustJava应用程序的用户，接收到的信息会以通知的形式出现在通知栏中。


	![9](http://owsep4p7v.bkt.clouddn.com/l4_09_%E7%94%A8Firebase%E5%90%91%E4%BD%A0%E7%9A%84App%E5%8F%91%E9%80%81%E7%AC%AC%E4%B8%80%E6%9D%A1%E9%80%9A%E7%9F%A5.png)
	<div style="text-align:center"><b>图9.</b>  Firebase通知推送的欢迎界面 </div>


	![10](http://owsep4p7v.bkt.clouddn.com/l4_10_EditMsg_%E7%94%A8Firebase%E5%90%91%E4%BD%A0%E7%9A%84App%E5%8F%91%E9%80%81%E7%AC%AC%E4%B8%80%E6%9D%A1%E9%80%9A%E7%9F%A5.png)
	<div style="text-align:center"><b>图10.</b>  用Firebase向你的App发送第一条通知 </div>

	![11](http://owsep4p7v.bkt.clouddn.com/l4_11_messaging_%E6%B6%88%E6%81%AF%E5%8F%91%E9%80%81%E5%90%8E.png)
	<div style="text-align:center"><b>图11.</b>  发送消息后 </div>

---

[1]: https://classroom.udacity.com/me "Udacity Android Courses"

[2]: https://www.studyjamscn.com/thread-20263-1-1.html "Google StudyJams China 2017"

[3]: http://www.cnblogs.com/DerekKen/p/6819390.html "DerekKen的博客园"
