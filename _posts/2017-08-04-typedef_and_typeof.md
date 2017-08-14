---
layout: post
title: iOS typedef 和 typeof 小结[转]
date: 2017-08-01
tags:  iOS   
---

<br><br>

typeof & typedef 咋一看上去老像了，但是两者区别可是很大的哦
<br><br>

### 一、理解

* typeof 是一个一元运算，放在一个运算数之前，运算数可以是任意类型。
可以理解为：我们根据typeof（）括号里面的变量，自动识别变量类型并返回该类型。
* typedef：定义一种类型的别名，而不只是简单的宏替换。
<br><br>

### 二、iOS 中的用处

#### 2-1、typeof 常见运用于Block中，避免循环引用发生的问题。

```
__weak __typeof(self) weakSelf = self;
```

```
[weakSelf addFooterWithRefreshingBlock:^{
    //do something
     [weakSelf.footer endRefreshing];
}
```

注意： typeof 括号中的值和等于后面的值是相同的类型。
另外有时偷懒也可以用到的,但是我不用，哈哈

```
__weak typeof(self.contentView) ws = self.contentView;
```

然后后面就直接用ws这样写啦...

**ps:**  ```typeof```、 ```__typeof__``` 、```__typeof``` 的区别

其实它们是没有区别的，只是它们只是针对不同的 c语言编译版本 有所不同的。
typeof是现代GNU C++的关键字；
从Objective-C的根源说，它其实来自于C语言，所以很多地方使用了继承自C的关键字。
看到AFNetworking 中，用的都是__typeof()；

#### 2-2、typedef 常用于命名（枚举和Block）

```
typedef NS_ENUM(NSInteger, UITableViewStyle) {
    UITableViewStylePlain,          // regular table view
    UITableViewStyleGrouped         // preferences style table view
}
```
```
typedef void(^YTKRequestCompletionBlock)(__kindof YTKBaseRequest *request);
```

iOS这块我们主要是用于枚举和Block，其他详细用途可参考：typedef 用法总结。

总之，细心感受它们，不要写错了

<br><br><br>
转自[简书:天空中的球](http://www.jianshu.com/p/f1c0f4aaa63a)


