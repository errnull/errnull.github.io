---
layout: post
title: 个人博客搭建（Jekyll + Github Page + 域名关联）
date: 2016-5-20
tags: BlogCourse   
---
<br><br>
本博客是使用 Jekyll 搭建的，以下是零基础的搭建教程。


### 介绍

[Jekyll 中文文档](http://jekyll.bootcss.com/)、[Jekyll 英文文档](https://jekyllrb.com/)、[Jekyll 主题列表](http://jekyllthemes.org/)。

　Jekyll 是一个简单的 博客形态的 静态站点 生成器。

　它通过 Markdown（或者 Textile）以及 [Liquid](http://www.jianshu.com/p/b11bc7b3306c) 生成一个完整的静态网站。

　你可以将它发布到任何服务器，包括 Github Page，这是完全免费的，当然你得有这个权限。使用 Jekyll 搭建博客之前要配置本机环境，需要安装的工具包括：

```
Git (用于部署到远端)
Node.js
Jekyll 。
```

　MacOS 可以打开终端使用下面的命令进行检查，根据自己的实际情况使用下面的安装教程。

```
$ git --version
$ node -v
$ jekyll -v    　
```


### 安装

安装教程根据上面三个工具分为三步。
<br><br>

#### 1.安装 Git

```
// 如果已安装 HomeBrew 无需执行此行
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
$ brew install git // 安装 Git  
```

　你也可以通过下载安装程序来安装。
　<br><br>

#### 2.安装 Node.js
　先安装 nvm， 这是 Node.js 版本管理器， 可以轻松切换 Node.js 版本。

```
$ brew install nvm //安装完成之后一定记得重启终端 //一定记得重启终端 //重启终端
```

　安装之后， **重启终端** 并执行下列命令即可安装 Node.js。

```
$ nvm install 4
```
<br>

#### 3.安装 Jekyll

```     
$ gem install jekyll     
```
<br>
    
#### 4.生成一个最简单的页面

　把下面的 yourName 替换成你的名字

```
$ jekyll new yourName.github.io
$ cd yourName.github.io
$ jekyll serve
# => Now browse to http://localhost:4000
```

### 目录结构
　
　Jekyll 的核心其实是一个文本转换引擎。它的概念其实就是：你用你最喜欢的标记语言来写文章，可以是 Markdown，也可以是 Textile，或者就是简单的 HTML, 然后 Jekyll 就会帮你套入一个或一系列的布局中。在整个过程中你可以设置URL路径, 你的文本在布局中的显示样式等等。这些都可以通过纯文本编辑来实现，最终生成的静态页面就是你的成品了。

 一个基本的 Jekyll 网站的目录结构一般是像这样的：

```
.
├── _config.yml
├── _includes
|   ├── footer.html
|   └── header.html
├── _layouts
|   ├── default.html
|   ├── post.html
|   └── page.html
├── _posts
|   └── 2016-10-08-welcome-to-jekyll.markdown
├── _sass
|   ├── _base.scss
|   ├── _layout.scss
|   └── _syntax-highlighting.scss
├── about.md
├── css
|   └── main.scss
├── feed.xml
└── index.html

```

这些目录结构以及具体的作用可以参考 [官网文档](http://jekyll.com.cn/docs/structure/) 

进入 _config.yml 里面，修改成你想看到的信息，重新 jekyll server ，刷新浏览器就可以看到你刚刚修改的信息了。

到此，博客初步搭建算是完成了。

### 部署博客
　
我这里讲的是部署到 Github Page 上。个人网站请自行搜索 🔍  。

#### 1.创建 Github

　首先你需要注册一个 Github 账号，注意 username，这会影响到你的域名，你的域名将会是 username.github.io ，所以认真的取个名字吧。

![](/images/posts/jekyll/2016-05-20-jekyll-01.jpg)
　注册的过程中可能需要验证邮箱， 其他的就不再赘述。

#### 2.创建仓库

　然后需要创建一个仓库（repository） 来存储我们的网站。
<br><br>

![](/images/posts/jekyll/2016-05-20-jekyll-02.jpg)
<br>
　点击首页任意位置出现的 New repository 按钮。
<br>
　Respository name 中的 username.github.io 的 username 一定与前面的 Owner 一致，记住你的 username 下面会用到。
<br>
![](/images/posts/jekyll/2016-05-20-jekyll-03.jpg)
<br>
　Create reponsitory

#### 3.部署博客到刚创建仓库

```
$ cd yourName.github.io
$ git init
$ git add .
$ git commit -m "first commit"
$ git remote add origin https://github.com/yourName/yourName.github.io.git
$ git push -u origin master
```
　这时，你只需要在浏览器输入

```
http://yourName.github.io
```
　就能看到你刚刚创建的博客啦。

### 绑定域名到 Github Page

　这个教程是在阿里云上操作的，不过其他平台大同小异。

#### 1.购买域名

　买买买，大家都会吧，购买之后要认证，按照要求上传身份证就行啦。然后进入控制台 - 域名列表。
![](/images/posts/jekyll/2016-05-20-jekyll-04.jpg)

#### 2.CNAME 绑定域名

默认使用阿里云提供的万网 DNS 服务器，点击解析。
在域名解析中，A 记录就是直接指定一个 IP，CNAME 就是重命名，指向另一个域名。
<br><br>

**1.** 点击添加解析

```
记录类型：A
主机记录：www
解析线路：默认
记录值是：192.30.252.153
```

　其中192.30.252.153是 Github Pages 服务器指定的 IP 地址，访问该 IP 地址即表示访问 Github Pages。
<br><br>

**2.** 点击添加解析

```
记录类型：A
主机记录：www
解析线路：默认
记录值是：192.30.252.154
```

<br>
**3.** 点击添加解析

```
记录类型：CNAME
主机记录：@
解析线路：默认
记录值是：yourName.github.io.
```

**在这里千万不要忘记记录值中 .io 后面还有一个点 .  ！！！！！**
<br><br>

**4.** 等待 DNS 服务器刷新， 你可以 ping 一下，看看设置是否正确。

至此你的域名可以被访问。

### 撰写博客
　
在目录结构介绍中说明过，所有的文章都在 _posts 文件夹中。 这些文件可以用 Markdown 编写， 也可以用 Textile 格式编写。
<br>
现在，在 _posts 下创建一个名为 FitstArticle.md 的文件，用 Markdown 开始**策马奔腾**吧！
    
如：

```
---
title: First Night
---
> 我有一头**小毛驴**，可是我从来都不骑。

```
　**测试**

```
$ jekyll server
# => Now browse to http://localhost:4000
```

　**部署**
    
效果满意的话就可以将项目 push 到 github 上了。
    
这里要注意， .gitignore 文件中添加

```
_site/
.sass-cache/
*.DS_Store
.idea
*.swp
.Trashes
```

其中 _site/ 中存放的是每次  build 之后生成的页面文件，可以忽视。 

### 鸣谢

文章部分材料摘自以下网站
<br>
[潘柏信博客](http://baixin.io/2016/10/jekyll_tutorials1/)
<br>
[5分钟快速搭建免费个人博客](http://www.5icool.org/a/201604/a17159_2.html)
<br>
[yuan3065的博客](http://blog.csdn.net/yuan3065/article/details/51594454)




