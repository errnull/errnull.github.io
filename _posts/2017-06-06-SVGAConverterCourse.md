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
它将每幅画卷 “精灵化”，记录动画中每个 Spirit 的运动轨迹从而避免重复渲染。<br><br>

#### **为啥要使用 SVGAPlayer**

举个栗子：<br>
当一个 iOS 动画需求摆在我们眼前时，我们有什么途径去实现呢？<br>

　 1. 帧动画：使用帧动画无疑是最轻松的，但是帧动画的每一帧都是一张图片，再加上不同的设备需要适配，不知不觉间 ipa 文件会变得很大，而且动画跑起来也会带来可观的内存开销。<br>
　 2. 使用 GIF：使用 GIF 本质上跟帧动画差不多，甚至有些地方会教我们把 GIF 拆成一帧一帧去播放，GIF 本身占用空间较大，虽然现在我们可以对 GIF 动画做一些操作，但是使用成本还是挺高的。<br>
　 3. Core Animation：CA 确实是一组非常强大的动画处理API，使用 CA 加上图片辅助确实可以实现一些动画需求，如果你想做梦还梦见自己在计算动画的话，可以继续使用它去完成你的动画需求。<br><br>

在其他平台当然也会有类似问题。<br>

<hr>
使用 SVGAPlayer 上面所有的问题都会药到病除，用几句代码就可以实现复杂的动画，你会有更多的时间去写梦寐以求的 BUG 。<br><br>

#### **怎么使用 SVGAPlayer**

直接上链接，毕竟人家的 Reandme 和源码比我详细得多：<br><br>
SVGAPlayer iOS：　 　 [https://github.com/yyued/SVGAPlayer-iOS](https://github.com/yyued/SVGAPlayer-iOS)<br>
SVGAPlayer Android： [https://github.com/yyued/SVGAPlayer-Android](https://github.com/yyued/SVGAPlayer-Android)<br>
SVGAPlayer Web：　　 [https://github.com/yyued/SVGAPlayer-Web](https://github.com/yyued/SVGAPlayer-Web)<br><br><br>

### 说好的小白也能放心食用呢？！！

这里的小白当然是指我们帅帅美美不食人间 ”代码“ 的设计师们啦~~<br>
为了尽可能减低设计师的使用成本，开发者们简化了插件的安装和使用，在这里我也铺开来讲一下吧！<br><br>

#### **安装 SVGAConverter**

* Windows：<br>
　 下载 windows 的专用安装器：[SVGAConverter_FL]() || [SVGAConverter_AE]();<br>
　 解压并且运行得到的 **install.exe** <br>
　 ![](/images/posts/jekyll/2017-06-06-SVGAConverterCourse-01.jpg)<br>
　 点击 **Install Now**<br>
　 稍等片刻，安装完成<br><br>
　 这里有几点要注意一下:<br>
　 　 1. 杀毒软件可能会误报有毒，切记点击**允许所有操作**。<br>
　 　 2. 和(po)谐(jie)的 Animate CC 可能会无法使用插件，安装器会自动修复这个问题。<br>
　 　　 **注意：**如果安装器找不到 Animate CC 的安装位置，会让用户手动选择，这时只要选择 Animate CC 的安装根目录即可。<br><br>
　 
安装完成后，在 **Animate CC** || **After Effects** 的 ```菜单 > 窗口 > 扩展``` 中可以打开插件。<br><br>
![](/images/posts/jekyll/2017-06-06-SVGAConverterCourse-02.jpg)<br>
　 
　
* MacOS：<br>
　 下载并安装 Adobe 的插件安装程序 [ZXP Installer](http://updates.aescripts.com/zxp-installer/mac/update-mac.zip)。<br><br>
![](/images/posts/jekyll/2017-06-06-SVGAConverterCourse-03.jpg)<br>

选择 ```菜单 > 文件 > 打开``` <br>
选择下载好的 [SVGAConverter_FL]() || [SVGAConverter_AE]() 安装包。<br>
按照安装器指引完成安装。

　 


