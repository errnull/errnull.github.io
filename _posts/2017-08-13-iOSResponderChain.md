---
layout: post
title: iOS 响应者链条 -- 响应者对象凭什么能够接收并处理事件
date: 2017-08-13 
tags:  iOS   
---

<br><br>

“在iOS中，只有继承了 UIResponder 的类的对象才能接收并处理事件，我们称之为’响应者对象‘。”<br>
只要搜一下响应者链条的相关问题，这句教科书式的回答便会充斥于各个搜索结果。<br>
作为小白难免心生疑惑:<br>
“继承了 UIResponder 的类的对象凭什么能接收并处理事件?”<br>
摊开讲之前，我们先了解一下跟响应者链条相关的 UITouch UIEvent UIResponder 这几个类。
<br><br>

### UIResponder

我们知道在 iOS 中 UIResponder 是专门用来响应用户的操作处理各种事件的，<br>
UIApplication、UIView、UIViewController 这几个类直接继承自 UIResponder，<br>
UIWindow 是继承自 UIView 的一个特殊的 View，这些类都可以响应事件。<br>
同样，我们自定义的继承自 UIView 的控件以及自定义的继承自 UIViewController 的控制器都可以响应事件。<br>
iOS里面通常将这些能响应事件的对象称之为响应者。<br><br>
目前在应用中常用事件基本上就这三种：<br>
　1.触摸事件(Touch Events)<br>
　2.加速计事件(Motion Events)<br>
　3.远程控制事件(Remote Control Events)<br>



