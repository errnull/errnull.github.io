---
layout: post
title: ENMetadataCleaner 实测
date: 2017-05-28 
tags:  Watarmy   
---

<br><br>

上个星期一个设计妹子在群里面问为什么她的 PSD 文件异常大，群里讨论得挺热闹。<br>
导师说：詹同学，你来解决这个问题吧！<br>
在一旁吃西瓜看热闹的我一脸😳比。“蛤？”

接着群里面的大神就开始科普：<br>
　“应该是元数据过多造成的。”<br>
　...... 此处省略10000字<br><br>
　
在导师的指导下写了这个脚本，基本的思想是：<br>
　　1. 将所有 layer 遍历一遍，找出所有智能对象。<br>
　　2. 将符合条件的智能对象逐个设为 activeLayer，清除其 RowData。<br>
　　3. 保存。<br><br>
<hr><br>

接下来进入实际测试：<br>
　　1. 测试的文件是妹子提供的一个 PSD 文件：
![](/images/posts/jekyll/2017-05-28-ENMetadataCleanerTest-01.jpg)

　　有 900M 这么大，果然没有预览效果。
　　<br><br>
　　再看看元数据：
![](/images/posts/jekyll/2017-05-28-ENMetadataCleanerTest-02.jpg)
<br><br>
　　够勤(dan)快(teng)的话，你还可以逐个打开智能对象，它们各自的元数据。
　　
<br><br>　
　知道问题出在哪里，就好做事多了。<br>
　　『文件』 >>> 『脚本』 >>> 『浏览』
![](/images/posts/jekyll/2017-05-28-ENMetadataCleanerTest-03.jpg)
<br>
选择下载好的 [ENMetadataCleaner.jsx](https://github.com/yyued/ENMetadataCleaner.git)

然后 PS 开始逐个清理。<br>
这时可能会有一点卡顿。<br><br>

跑完之后会自动保存，这时候元数据所剩无几。<br>
用起来也不卡了。<br><br>

再看看文件：
![](/images/posts/jekyll/2017-05-28-ENMetadataCleanerTest-04.jpg)
<br>
只剩下惊人的 10.5M，预览效果果然也出来了，操作也不卡了。



