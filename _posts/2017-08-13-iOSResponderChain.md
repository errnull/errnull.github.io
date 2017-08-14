---
layout: post
title: iOS 响应者链条 -- 响应者对象凭什么能够接收并处理事件(未完)
date: 2017-08-13 
tags:  iOS   
---

<br><br>

“在iOS中，只有继承了 UIResponder 的类的对象才能接收并处理事件，我们称之为’响应者对象‘。”<br>
只要搜一下响应者链条的相关问题，这句教科书式的回答便会充斥于各个搜索结果。<br>
作为小白难免心生疑惑:<br>
“继承了 UIResponder 的类的对象凭什么能接收并处理事件?”<br>
摊开讲之前，我们先了解一下跟响应者链条相关的 UIResponder UITouch UIEvent 这几个类。
<br><br>

### UIResponder

我们知道在 iOS 中 UIResponder 是专门用来响应用户的操作处理各种事件的，<br>
UIApplication、UIView、UIViewController 这几个类直接继承自 UIResponder，<br>
UIWindow 是继承自 UIView 的一个特殊的 View，这些类都可以响应事件。<br>
同样，我们自定义的继承自 UIView 的控件以及自定义的继承自 UIViewController 的控制器都可以响应事件。<br>
iOS里面通常将这些能响应事件的对象称之为响应者。<br><br>
目前在应用中常用事件基本上有三种：<br>
　1.触摸事件(Touch Events)<br>
　2.加速计事件(Motion Events)<br>
　3.远程控制事件(Remote Control Events)<br>

其中触摸事件是我们最常用的事件，例如单击、长按、滑动等等。<br>
触摸事件中我们需要了解：

#### UITouch
手指每一次点击屏幕，都会形成一个 UITouch 对象，直到离开销毁。<br>
UITouch对象记录了当前手指触碰的屏幕位置、时间、阶段、状态等信息。

#### UIEvent

从第一个手指触摸屏幕开始到最后一个手指离开屏幕，我们称之为一次触摸事件。<br>
UIEvent 实际包括了多个 UITouch 对象。有几个手指触碰，就会有几个 UITouch 对象。<br><br>

概念铺了这么多，那么到底为什么这些响应者对象能接收并处理事件呢？<br>
又是谁来创建并发送 Event 和 Touch 对象呢？<br>
当用户点击屏幕，再到处理回调。整个过程经历了什么，又需要什么样的原则呢？我们需要从头来讲。
<br><br>

### 发生点击事件

当用户触摸屏幕时, 会创建一个包含 UITouch 对象的 UIEvent 对象，<br>
系统会将这个 UIEvent 对象加入到一个由 UIApplication 管理的 FIFO 事件队列中。<br>
UIApplication 对象处理事件时，会从队列头部取出一个 UIEvent 对象进行分发。<br>
通常，UIApplication 会首先把事件交给应用程序的主窗口 (keyWindow)。<br><br>
这里需要注意的是:<br>
Window 会先将事件交给 UIGestureRecognizer ，<br>
如果 UIGestureRecognizer 识别了传递过来的事件，则交给相对应的 target 去处理，事件就此停止传递。<br>
如果 UIGestureRecognizer 没有识别传递过来的事件，事件会传递到视图树形结构，<br>
此时系统会将事件响应过程拆分成两部分：<br>
先将事件通过某种规则来分发，找到处理事件的控件。然后将事件传递分发，响应；
<br>

#### 1.寻找响应链

在 iOS 视图树形结构中找到最终的接收者，也就是触摸事件发生的那个最上层的 View 上，<br>
这一过程称为 hit-testing(测试命中)，通过一层层的遍历找到最终的命中视图称为 hit-test view。<br>
UIView 中有两个方法用来确定 hit-test view。<br>

```
- (UIView *)hitTest:(CGPoint)point withEvent:(UIEvent *)event; 
- (BOOL)pointInside:(CGPoint)point withEvent:(UIEvent *)event;
```

<br><br>

#### 2.事件响应。

<br><br>


<br><br><br><br><br><br><br><br><br><br><br><br><br>

### 谁来监听用户点击

当一个硬件事件(触摸/锁屏/摇晃等)发生后，首先由 IOKit.framework 生成一个 IOHIDEvent 事件并由 SpringBoard 接收。这个过程的详细情况可以参考这里。SpringBoard 只接收按键(锁屏/静音等)，触摸，加速，接近传感器等几种 Event，随后用 mach port 转发给需要的App进程。随后苹果注册的那个 Source1 就会触发回调，并调用 _UIApplicationHandleEventQueue() 进行应用内部的分发。<br>

_UIApplicationHandleEventQueue() 会把 IOHIDEvent 处理并包装成 UIEvent 进行处理或分发，其中包括识别 UIGesture/处理屏幕旋转/发送给 UIWindow 等。通常事件比如 UIButton 点击、touchesBegin/Move/End/Cancel 事件都是在这个回调中完成的。

### then

为了使系统能更加鲜明符合用户的操作逻辑，iOS系统将事件相应过程拆分成两部分：1.寻找响应链；2.事件响应。先将事件通过某种规则来分发，找到处理事件的控件。其次是将事件传递分发,响应。


