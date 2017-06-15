---
layout: post
title: AE & Animate 动效秒变 SVGA 动画 --- 小白也能放心食用的 SVGAConverter
date: 2017-06-06 
tags:  Watarmy   
---

<br><br>

SVGAConverter 是一款可运行在 **After Effects** & **Animate CC** 上的插件，可以将设计师画板上的精彩之作轻松转换成 SVGA 动画源文件。<br>
你还不知道 SVGA 是啥？<br><br>

### SVGAPlayer

SVGAPlayer 是 YY 开源的一个支持 iOS、Android、Web 以及 ReactNative 的动画框架，<br>
将每幅画卷 “精灵化”，记录每个 Spirit 的运动轨迹从而避免重复渲染。<br><br>

#### **为啥要使用 SVGAPlayer**

当一个 iOS 动画需求摆在我们眼前时，我们有什么途径去实现呢？<br>

　 1. 帧动画：使用帧动画无疑是最轻松的，但是帧动画的每一帧都是一张图片，再加上不同的设备需要适配，不知不觉间 ipa 文件会变得很大，而且动画跑起来也会带来可观的内存开销。<br>
　 2. 使用 GIF：使用 GIF 本质上跟帧动画差不多，甚至有些地方会教我们把 GIF 拆成一帧一帧去播放，GIF 本身占用空间较大，虽然现在我们可以对 GIF 动画做一些操作，但是使用成本还是挺高的。<br>
　 3. Core Animation：CA 确实是一组非常强大的动画处理API，使用 CA 加上图片辅助确实可以实现一些动画需求，如果你想做梦还梦见自己在计算动画的话，可以继续使用它去完成你的动画需求。<br>

<hr>
使用 SVGAPlayer 上面所有的问题都会烟消云散，用几句代码就可以实现复杂的动画，你会有更多的时间去写梦寐以求的 BUG 。<br><br>

#### **怎么使用 SVGAPlayer**

直接上链接，毕竟人家的 Reandme 和源码比我详细得多：<br><br>
SVGAPlayer iOS： [https://github.com/yyued/SVGAPlayer-iOS](https://github.com/yyued/SVGAPlayer-iOS)<br>
SVGAPlayer Android： [https://github.com/yyued/SVGAPlayer-Android](https://github.com/yyued/SVGAPlayer-Android)<br>
SVGAPlayer Web： [https://github.com/yyued/SVGAPlayer-Web](https://github.com/yyued/SVGAPlayer-Web)<br><br><br>

### 说好的小白也能放心食用呢？！！

这里的小白当然是指我们帅帅美美不食人间 ”代码“ 的设计师们啦~~<br>
为了尽可能减低设计师的使用成本，开发者们简化了插件的安装和使用，在这里我也铺开来讲一下吧！<br><br>

#### **安装 SVGAConverter**

* Windows：
* MacOS：


