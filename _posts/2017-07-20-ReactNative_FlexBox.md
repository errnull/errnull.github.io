---
layout: post
title: ReactNative 轻松入门之 Flex Box 布局
date: 2017-07-10
tags:  ReactNative   
---

<br><br>

“好看的皮囊千篇一律?”<br>
那是因为你家的程序员哥哥没有把布局学扎实。<br>
只有 “懒” 程序员，没有丑 app，<br>
看完这篇文章，你会发现好看的皮囊也可以万种风情，千般变化。
<br><br>

### Flex Box 布局

Flex Box 完整名称为：the Flexible Box Module，旨在通过弹性的方式来对齐和分布容器中的组件。<br>
Flex 布局的主要思想是：让容器的子项目能够自动适应宽度|高度|顺序，以最佳方式填充可用空间。<br>
在布局中，首先得确定主轴方向 (flexDirection) ，主轴组件的对齐方式（justifyContent），侧轴组件的对齐方式 (alignItems) ，子元素弹性分布空间 (flex) ，通过以上四点可以基本确定布局。
<br><br>

" 旁白：作为一个 iOS 小白完全听不懂在讲啥啊啊啊啊啊！！！ "<br>
好吧其实我也不知道我在说什么😑
<br><br>

React Native 中的 FlexBox 和 Web CSS 上 FlexBox 工作方式是一样的。<br>
我们可以从这里开始讲。<br><br>

采用Flex布局的元素，称为Flex容器（flex Container），简称"容器"。它的所有子元素自动成为容器成员，称为Flex项目（flex item）。

首先我们要有主轴和侧轴的概念：
![xxx](/images/posts/jekyll/2017-07-20-ReactNative_FlexBox-01.jpg)<br>

容器默认存在两根轴：水平的主轴（main axis）和垂直的交叉轴（cross axis）。主轴的开始位置（与边框的交叉点）叫做 main start，结束位置叫做 main end；交叉轴的开始位置叫做 cross start，结束位置叫做 cross end。<br><br>

### Flex Box 属性

<br>
**flexDirection** 属性确定主轴方向

```
container: {
    flexDirection: enum('row',              // 从左向右排列。
                        'column',           // 从右向左排列。
                        'row-reverse',      // 从上向下排列。(默认)
                        'column-reverse'    // 从下向上排列。
)},
```
侧轴垂直于主轴，也叫交叉轴。
<br><br>
**justifyContent** 属性确定组件在主轴方向上的对齐方式

```
container: {
    justifyContent: enum('flex-start',      // 组件沿着主轴方向的起始位置靠齐。(默认)
                         'flex-end',        // 组件沿着主轴方向的结束位置靠齐。
                         'space-between',   // 组件在主轴方向上两端对齐，间隔相等。
                         'space-around'     // 组件会平均分配在主轴方向上。
)},
```
<br>
**flexWrap** 属性定义了子元素在父视图内是否允许多行排列

```
container: {
    flexWrap: enum('wrap',                   // 元素只排列在一行上，可能导致溢出。
                   'nowrap',                 // 元素在一行排列不下时，就进行多行排列。
                   'wrap-reverse'  　　       // 进行多行排列，第一行在顺序从下往上。
)},
```
<br>
**alignItems** 属性定义了组件在侧轴方向上的对齐方式

```
container: {
    alignItems: enum('flex-start',           // 元素只排列在一行上，可能导致溢出。
                     'flex-end',             // 组件沿着侧轴上的终点对齐。
                     'center',  　　          // 组价在侧轴方向上居中对齐。                     
                     'stretch'  　　          // 组件在侧轴方向上占满。(默认)
)},
```
<br>
**alignSelf** 属性定义了子元素在容器中的位置

```
container: {
    alignItems: enum('auto',  　　            // 元素继承其的父容器的 align-items 属性，如果没有父容器则为 'stretch 。
                     'flex-start',  　　      // 元素位于容器的开头。
                     'flex-end',  　　        // 元素位于容器的结尾。
                     'center',  　　          // 元素位于容器的中心。 
                     'stretch'               // 元素被拉伸以适应容器。                    
)},
```
<br>
**flex** 属性定义了一个可伸缩元素的能力

```
container: {
    alignItems: number                       // flex 属性定义了一个可伸缩元素的能力，默认为0。                    
)},
```
<br>
**position** 属性设置元素的定位方式，为将要定位的元素定义定位规则

```
container: {
    alignItems: enum('absolute',  　　        // 生成绝对定位的元素，元素的位置通过 “left”, “top”, “right” 以及 “bottom” 属性进行规定。
                     'relative',  　　        // 生成相对定位的元素，相对于其正常位置进行定位。        
)},
```
<br>

#### 以下属性是React Native所支持的除Flex以外的其它布局属性。

视图边框：

```
container: {
    borderBottomWidth: number,               // 底部边框宽度
    borderLeftWidth: number,                 // 左边框宽度
    borderRightWidth: number,                // 右边框宽度
    borderTopWidth: number,                  // 顶部边框宽度
    borderWidth: number                      // 边框宽度
},
```
<br>
尺寸：

```
container: {
    width: number,                           // 宽 
    height: number                           // 高
},
```
<br>
外边距：

```
container: {
    margin: number,                          // 外边距
    marginBottom: number,                    // 下外边距
    marginHorizontal: number,                // 左右外边距
    marginLeft: number,                      // 左外边距
    marginRight: number,                     // 右外边距
    marginTop: number,                       // 上外边距
    marginVertical: number                   // 上下外边距
},
```
<br>
外边距：

```
container: {
    padding: number,                         // 内边距
    paddingBottom: number,                   // 下内边距
    paddingHorizontal: number,               // 左右内边距
    paddingLeft: number,                     // 做内边距
    paddingRight: number,                    // 右内边距
    paddingTop: number,                      // 上内边距
    paddingVertical: number                  // 上下内边距
},
```
<br>
边缘：

```
container: {
    left: number,   // 属性规定元素的左边缘。该属性定义了定位元素左外边距边界与其包含块左边界之间的偏移。
    right: number,  // 属性规定元素的右边缘。该属性定义了定位元素右外边距边界与其包含块右边界之间的偏移
    top: number,    // 属性规定元素的顶部边缘。该属性定义了一个定位元素的上外边距边界与其包含块上边界之间的偏移。
    bottom: number  // 属性规定元素的底部边缘。该属性定义了一个定位元素的下外边距边界与其包含块下边界之间的偏移。
},
```
<br>


