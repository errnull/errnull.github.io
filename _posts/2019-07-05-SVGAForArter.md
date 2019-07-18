---
layout: post
title: SVGA 设计使用指南
date: 2019-7-5 
tags: SVGA   
---
<br>

```
SVGA 设计使用指南
```

SVGA 提供了 AE 和 An 源文件导出 .svga 的插件，
方便设计师一键导出资源给开发使用，
以下是插件使用指南。

## 工作区

### 时间

SVGA 文件的动画时长，一般是由 Item 的工作区时长决定的:
![worktime](https://i.imgur.com/wXB7MFB.gif)

插件右上角的设置中可以选择预设值：
![worktimeSetting](https://i.imgur.com/NpZ82JV.gif)

如果选择 `以动画实际时长为准` 
导出的动画时长会等于创建 Item 时设置的时长：
![settingtime](https://i.imgur.com/pApdsFs.gif)

这个值随时可以修改。

**注意：**
SVGA 不支持修改动画的开始时间，
SVGA 只从时间轴原点开始读取动画，动画时长为设置的动画时长(Duration)。

### FPS

动效的 FPS 一般在 60 以内，
建议设置为 60 的约数：
`[1, 2, 3, 4, 5, 6, 10, 12, 15, 20, 30, 60]`

动效导出的时候会检查 FPS 是否合法，
如果不合法会自动就近修正，但不影响源文件。

合法 FPS 其实是个伪命题，
有这个规范主要是跟客户端屏幕刷新率有关，
客户端屏幕刷新帧率一般为 60 FPS，
播放动效跟这个节奏一致成本会低很多。

### 画布

每创建一个 Item 都会有一块预设画布，
可以在 Item 中设置画布的尺寸和背景颜色：
![canvas](https://i.imgur.com/sm5HGdk.gif)

画布的尺寸对应 SVGA 文件的 `width` 和 `height`,
浏览素材的时候可以看到：
![svgasize](https://i.imgur.com/vi3LH3f.png)
开发在播放 SVGA 的时候可以对动效进行等比缩放。

SVGA 动画没有预设背景色，
所以画布的背景颜色对 SVGA 动画没有影响。


### 图层

每创建一个图层，SVGA 动画中就会多一个动画元素，
它们通过图层名称和动画元素中的 `imageKey` 一一对应。

#### 替换

播放 SVGA 动画的时候，可以通过 `imageKey` 动态替换图层内容。 
需要提供给开发的信息:
* imageKey 
* 与图层一样尺寸的被替换素材


#### 蒙版

图层可以通过设置蒙版属性：
![mask](https://i.imgur.com/X4agStQ.gif)

控制图层的 alpha 通道，
达到只显示部分图案的效果。

蒙版一般为闭合路径，开放路径无法为图层创建透明区域。

#### 遮罩

遮罩是图层间的关系，通过图层 TrkMat 设置，

可以一对一，也可以一对多，
在 SVGA 动效中对应动画元素的 `matteKey`。

**注意：**将位图设置为遮罩图层的时候，
尽量使用 8-bpc 只带透明通道的图片以节约资源。

值得一提的是，位图遮罩的 imageKey 也是可以动态替换的，
就是说动效中的遮罩在播放的过程中是可变的。

## SVGA 中的动画内容
```
SVGA 其实不叫 SVGA，应该叫 BVGA。
                    --官方吐槽
```

BVGA 即 Bitmap Vector Graphic Animation，
从名字可以看出，SVGA 中动画内容主要是位图和矢量。

### 位图

制作 SVGA 动画时可以使用：
* png
* jpg
* psd

这三种格式，
但它们最终会被转成 png 素材。

**注意：**
SVGA 支持 psd 的图层样式，
导出 psd 文件的时候务必选择：
![importpsd](https://i.imgur.com/FegEq1m.gif)
`合成` -> `合并图层样式` -> `确定`

合并图层样式
合并图层样式
合并图层样式

重要的话说三遍，
否则会导致素材**尺寸**或者**样式**异常。

### 矢量

矢量是一组用来描绘图形的元数据，
在 AE 中可以使用：
* 钢笔工具
* 形状图形

来绘制，
但它们最终会被导成贝塞尔曲线。

**注意：**
SVGA 支持导入 .ai 文件
.ai 文件同样会被导成贝塞尔曲线：
![inportai](https://i.imgur.com/xNbXrKc.gif)

SVGA Converter 会自动执行转换，
不过更建议设计师导入 .ai 文件的时候自行转换，提前预览动画效果。

##### 颜色

颜色深度（或位深度）是用于表示像素颜色的每通道位数 (bpc)。每个 RGB 通道（红色、绿色和蓝色）的位数越多，每个像素可以表示的颜色就越多。

在 After Effects 中可以使用 8-bpc、16-bpc 或 32-bpc 颜色。

除色位深度之外，用于表示像素值的数字的另外一个特性是数字是整数还是浮点数。浮点数可以表示具有相同位数的更大范围的数字。在 After Effects 中，32-bpc 像素值是浮点值。

8-bpc 像素的每个颜色通道可以具有从 0（黑色）到 255（纯饱和色）的值。16-bpc 像素的每个颜色通道可以具有从 0（黑色）到 32,768（纯饱和色）的值。如果所有三个颜色通道都具有最大纯色值，则结果是白色。32-bpc 像素可以具有低于 0.0 的值和超过 1.0（纯饱和色）的值，因此 After Effects 中的 32-bpc 颜色也是高动态范围 (HDR) 颜色。HDR 值可以比白色更明亮。

[AE中的8bpc、16bpc、32bpc](https://www.bilibili.com/read/cv2168818/)



##### 路径
##### 修剪路径

路径修剪(TrimPath) 是一种矢量动效样式。
它一共有三个相关的属性：
```
trimPathStart,
trimPathEnd,
trimPathOffset，
```

它们分别表示 Path 从哪里开始，到哪里结束，距离起点多远。
在 AE 形状图层中可以添加：
![add-trimpath](https://i.imgur.com/s78bKig.jpg)


可添加在形状(Shape)属性中，也可以添加在 Shape 之外对多个 Shape 造成影响：
![muti-trimpath-1](https://i.imgur.com/hXjvlE4.jpg)
**注意：**SVGA 中现在还未支持外层修剪，
也不支持 trimPathOffset，
将在接下来的版本中完善。

##### 文本

SVGA 中不支持文本导出，
可以将静态的 Text 渲染成 PNG，
将有动效文本图层转换为形状图层使用：
![changetext](https://i.imgur.com/3Wz4amV.gif)

偶尔转换的图层会有问题，
不过转换是 AE 黑盒处理的，

咱也不知道咱也不敢问...

## SVGA 中的动画属性

### 动效使用和展示

动画随时间而变化。
在 AE 中设计师通过使图层或图层上效果的一个或多个属性随时间变化，
来创建动画效果。

#### 关键帧

关键帧用于设置动作、效果、音频以及许多其他属性的参数，
使这些参数随时间变化。

#### 属性动画

属性包括了缩放、旋转、位移、透明度、颜色等等，
只要右侧属性面板中带小菱形标志，
都归纳到了这一类型中。

SVGA 支持属性动画的关键帧定制炫酷的效果，
这也是 SVGA 核心的动画能力。

**注意：**
动画的属性，比如形状的透明度之类的，
最好直接设置在元素上，不要越级使用，
否则可能会合并异常。

## 最后

### 导出

* 打开插件
    ![extension](https://i.imgur.com/WkOq3yh.png)

* 点击 `选择位置` 选择 SVGA 文件生成位置 
   **注意：**这里可以同时选择多个合成导出。
    
* 点击 `开始转换`，SVGA 文件就会生成在对应目录。

* 右上角`设置`中可以切换 SVGA 版本、选择导出时长。


### 特性总览

AE 除了上面提到的众多属性动效，还支持使用很多特性，
SVGA 现在正在逐步完善中，
一下是特性总览表，
会逐步更新。

![640](https://i.imgur.com/zPm5aUn.jpg)


### FAQ


### 友情链接

[2D Manual](https://docs.2dimensions.com/support/)
[SVGA 踩坑日记](https://mp.weixin.qq.com/s/vbDRVJITTr3gVWKsvWD6oQ)
[After Effects Handbook](https://helpx.adobe.com/cn/after-effects/user-guide.html)
[README Board](https://zhuanlan.zhihu.com/p/45180728)

 
