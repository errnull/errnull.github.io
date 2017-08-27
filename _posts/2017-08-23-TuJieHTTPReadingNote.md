---
layout: post
title: 《图解 HTTP》阅读笔记 一
date: 2017-08-23 
tags:  Net   
---

<br><br>

之前草草读了一遍《图解 HTTP》这本书<br>
很多东西都似懂非懂，所以重新读一遍，整理一些笔记。
<br><br>

### HTTP 基础

#### **·简述**

HTTP (HyperText Transfer Protocol, 超文本**传输**协议) 是 Web 信息共享的规范和基础。<br>
值得注意的是，HTTP 并**不是**被设计为一种**传输协议**（transport protocol），它是一种**转移协议**（transfer protocol）。<br><br>
非常不幸，HTTP 刚刚传入我国时，即被错误翻译为“超文本传输协议”，<br>
因为 “transport” 和 “transfer” 在中文中都具有 “传输” 的含意，之后以讹传讹贻害无穷。(摘自[百度百科](https://baike.baidu.com/item/超文本转移协议/1675080?fr=aladdin))<br><br>
在 [IETF](https://baike.baidu.com/item/互联网工程任务组/707674?fr=aladdin&fromid=2800318&fromtitle=IETF) 的 [RFC](https://baike.baidu.com/item/RFC/1840) 中 (某组织的某文件中)<br>
**“transport”（传输）的含义是指**：从端到端（例如从 ip1:port1 到 ip2:port2 ）可靠地搬运比特，也就是 TCP/IP 协议栈中的第3层传输层（transport layer）协议所做的那些事情。<br>
**“而 transfer”（转移） 的含义是**：通过在客户端-服务器端之间转移一些带有操作语义的操作原语，来执行某种操作。<br>
“transfer” 是 TCP/IP 协议栈中的第4层应用层的概念，而不是第3层传输层的概念。“transfer” 所转移的是带有明确操作语义的操作原语，而不是没有操作语义的比特流。<br>
这里有一篇文章解释得非常好：[西门吹牛的博客](http://www.cnblogs.com/gudi/p/6959715.html)
<br><br>

HTTP 三个版本：**0.9、1.0、1.1** (更新慢)。
<br><br>

#### **·网络基础**

网络是在 TCP/IP 协议族的基础上运作的，HTTP 是它的子集。<br>
TCP/IP 是在 IP 协议的通讯过程中，使用到的协议族的统称。<br>
它被分为四层：<br>
　　1.应用层：决定了向用户提供应用服务时的通信活动，如 FTP，DNS 和 HTTP 等；<br>
　　2.传输层：提供处于网络连接中的两台计算机之间的数据传输，TCP，UDP；<br>
　　3.网络层：用来处理网络上流动的数据包，IP 协议；<br>
　　4.链路层：网络连接的硬件部分。<br>
<br>
数据在各层中封装后进行传输
![](/images/posts/jekyll/2017-08-23-TuJieHTTPReadingNote-01.jpg)
<br><br>

IP 协议的作用是把各种数据包传送给接收方，其中 IP 地址和 MAC 地址用于确定接收方的位置。<br>
IP 地址可以通过 ARP 协议 (Adress Resolution Protocol) 反查出对应的MAC地址。
![](/images/posts/jekyll/2017-08-23-TuJieHTTPReadingNote-02.jpg)
<br><br>

TCP 协议能够将数据准确可靠地传输给接收方,(三次握手)。
![](/images/posts/jekyll/2017-08-23-TuJieHTTPReadingNote-03.jpg)
<br><br>

DNS 服务位于应用层。它提供域名到IP地址之间的解析服务<br>
域名易于人类理解，IP 地址易于计算机理解
![](/images/posts/jekyll/2017-08-23-TuJieHTTPReadingNote-04.jpg)
<br><br>

下面是一个 HTTP 请求的总体过程：
![](/images/posts/jekyll/2017-08-23-TuJieHTTPReadingNote-05.jpg)
<br><br>

#### **·URI、URL 和 URN**

**URI** 是统一资源标识符、**URL** 是统一资源定位符，而 **URN** 是统一资源名称。<br>
URL、URN 是 URI 的子类。
<br><br>

#### **·简单结构**

http 协议用于客户端与服务端之间的通信，是一种无状态协议 (stateless)。<br>
通过在请求和响应**报文**中写入 Cookie 信息来控制客户端状态。<br>
![](/images/posts/jekyll/2017-08-23-TuJieHTTPReadingNote-06.jpg)

一开始，每进行一次 HTTP 通讯就要断开一次 TCP 连接。<br>
为了节省通讯流量，减轻服务器负担， HTTP/1.1 和一部分 HTTP/1.0 开始使用持久连接。<br>
**持久连接：**只要一端没有明确提出断开连接，则保持 TCP 连接状态。<br>
![](/images/posts/jekyll/2017-08-23-TuJieHTTPReadingNote-10.jpg)
在持久连接基础上可以实现管线化，可以同时发送多个请求。
![](/images/posts/jekyll/2017-08-23-TuJieHTTPReadingNote-11.jpg)
<br><br>

#### **·HTTP 方法**

HTTP 方法中我们常用 POST，GET<br>
那 **"GET 和 POST 有什么区别呢？"**<br>
![](/images/posts/jekyll/2017-08-23-TuJieHTTPReadingNote-08.jpg)
<br>
这个问题网上流传着诸多 “标准答案”，但那些大多数都不是我们需要的。<br><br>
HTTP 的底层是 TCP/IP，所以 GET 和 POST 的底层也是 TCP/IP，也就是说，GET/POST 都是 TCP 链接。<br>
GET 和 POST 能做的事情是一样的，<br>
你要给 GET 加上 request body，给 POST 带上 URL 参数，技术上是完全行的通的。<br><br>
万维网中，TCP 就像汽车，我们用 TCP 来运输数据，它很可靠，极少发生丢件少件的现象。<br>
HTTP 作为交通规则，给汽车运输设定了好几个服务类别，有 GET, POST, PUT, DELETE 等等。<br>
HTTP 规定，当执行 GET 请求的时候，要给汽车贴上 GET 的标签(设置 method 为 GET)，而且要求把传送的数据放在车顶上(URL 中)以方便记录。<br>
如果是POST请求，就要在车上贴上 POST 的标签，并把货物放在车厢里。<br>
当然，你也可以在GET的时候往车厢内偷偷藏点货物，但是这是很不光彩，也可以在 POST 的时候在车顶上也放一些数据，让人觉得傻乎乎的。<br>
HTTP 只是个行为准则，而 TCP 才是 GET 和 POST 实现的基本。
<br><br>
而我们用来发送和接收请求的浏览器，可以看成交通中的负责装货和卸货运输公司，<br>
它们的一些限制，导致不同请求产生差别。<br>
比如，(大多数)浏览器通常都会限制 URL 长度在 2k 字节，而(大多数)服务器最多处理 64K 字节大小的URL，超过的部分，恕不处理。<br>
比如，如果你用 GET 服务，在 request body 偷偷藏了数据，有些服务器会帮你卸货，读出数据，有些服务器直接忽略，所以，虽然 GET 可以带 request body，也一定能保证会被接收。<br><br>
总的就一句话：<br>
GET 和 POST 本质上就是 TCP 链接，并无差别。但是由于 HTTP 的规定和浏览器/服务器的限制，导致他们在应用过程中体现出一些不同。<br><br>

#### **·In addition**

GET 和 POST 还有一个重大区别，<br><br>
简单来说：<br>
GET 产生一个 TCP 数据包，POST 产生两个 TCP 数据包。<br><br>
长的说：<br>
对于 GET 方式的请求，浏览器会把 http header 和 data 一并发送出去，服务器响应200(返回数据);<br>
而对于 POST，浏览器先发送 header，服务器响应 100 continue，浏览器再发送 data，服务器响应 200 ok(返回数据)。<br>
也就是说，GET 只需要汽车跑一趟就把货送到了，而 POST 得跑两趟，第一趟，先去和服务器打个招呼“嗨，我等下要送一批货来，你们打开门迎接我”，然后再回头把货送过去。<br><br>
在网络环境好的情况下，发一次包和发两次包的时间差别基本可以无视。<br>
而在网络环境差的情况下，两次包的 TCP 在验证数据包完整性上，有非常大的优点。<br>
而且 GET 与 POST 都有自己的语义，尽量不要随便混用。<br><br>
最后放上方法表：
![](/images/posts/jekyll/2017-08-23-TuJieHTTPReadingNote-09.jpg)
<br><br>

回到上文，为了弄明白报文是什么东西，我们需要进一步了解 HTTP 包含的信息。

### HTTP 信息

#### **·报文信息**

用于 HTTP 协议交互的信息被称为 HTTP 报文，使用 CR+LF (\r\n) 作为换行符。<br>
客户端的 HTTP 报文叫做请求报文，服务器端的 HTTP 报文叫响应报文，<br>

报文分为报文首部和报文主体,报文首部一般有四种：通用首部，请求首部，响应首部和实体首部；<br>
在客户端与服务器之间进行通信过程中，无论是请求首部还是响应首部都能起到传递额外重要信息的作用，<br>
如报文主体大小，所使用的的语言和认证信息等等。<br>
一般通过 CPU 编码提升传输效率，也会对报文进行压缩、分割。<br>
![](/images/posts/jekyll/2017-08-23-TuJieHTTPReadingNote-07.jpg)
<br><br>

**·通用字段**<br>
　Cache-Control:　　　用于操作缓存的工作机制，如缓存时间，是否必须向服务器确认等;<br>
　Connection：　　　　控制不再转发给代理的首部字段和持久连接，http1.1 版本默认的连接都是持久连接;<br>
　Date:　　　　　　　　表明创建 Http 报文的日期和时间;<br>
　Transfer-Encoding:　规定传输报文主体时采用的编码方式;
<br><br>

**·请求首部**<br>
　Accept:　　　　　　通知服务器客户端可以处理的媒体类型以及媒体类型的相对优先级，如 application/json、text/html、image/jpeg 等，<br>
　　　　　　　　　　优先级使用q=来表示权重，最大值为1，默认权重为1.0;<br>
　Accept-Language：通知服务器客户端可以处理的语言集以及相对优先级;<br>
　Authorization：　　用于高速服务区客户端的认证信息。通常在接收到服务器返回的401状态码后，客户端将 Authorization 加入请求中;<br>
　Host:　　　　　　　http1.1 规范中唯一一个必须包含在请求内的首部字段，可为空;<br>
　User-Agent：　　　创建请求的浏览器名称等信息;<br>
<br>

**·响应首部**<br>
　Location:　　提供重定向的资源地址;<br>
　Server:　　　服务器上安装的http服务器应程序信息为Cookie服务的首部字段;<br>
　Set-Cookie：开始状态管理所使用的Cookie信息(响应首部)，管理服务器端设置的cookie信息，<br>
　　　　　　　如 expires 过期时间，domain 所属域名和 httponly 等;<br>
　Cookie：　　服务器端收到的Cookie信息(请求首部);
<br><br>

#### **·状态码**

服务器通过状态码告知客户端请求结果状态，正常、错误还是其他。<br>
![](/images/posts/jekyll/2017-08-23-TuJieHTTPReadingNote-12.jpg)
状态码如 200 OK，以 3 位数字和原因短语组成。<br>
数字中的第一位指定了响应类别，后两位无分类。<br><br>
常用的状态码有：<br>
　200 (OK): 服务器正常处理了请求;<br>
　204 (No Content): 请求处理成功，但是没有内容返回，客户端不需要刷新;<br>
　206 (Partial Content): 客户端进行范围请求，服务端返回部分内容;
　<br><br>
　304 (Not Modified): 资源未发生变动，一般浏览器会使用已经缓存过的资源;<br>
　401 (UNauthorized): 第一次返回表示需要认证，第二次则是表示认证失败;<br>
　403 (Forbidden): 请求资源的访问被服务器拒绝;<br>
　404 (Not Found): 服务器上不存在请求的资源;<br>
　500 (Internal Server Error): 服务器内部错误;
<br><br>

### HTTP 与 Web 服务器

一般，在互联网上域名通过DNS服务器域名解析后映射到IP地址再访问目标网站。<br>
由于虚拟主机的功能，在相同的IP地址下可以部署多个不同域名的Web站点，因此在发送HTTP请求时必须在Host首部内完善域名。
<br><br>

#### **通信数据的转发**

**1.代理**：扮演位于服务器与客户端中间人的角色，它接受客户端的请求转发给服务器，同时也接受服务器的返回结果并转发给客户端。
![](/images/posts/jekyll/2017-08-23-TuJieHTTPReadingNote-13.jpg)
<br>

**缓存代理**：预先将服务器上的资源副本缓存在代理服务器上，当客户端对这些已经缓存过了的资源发出请求时，代理不会对服务器发出请求，而是直接返回缓存的资源。
<br><br>
**2.网关**：接收客户端发送过来的请求，并自行进行处理，利用网关可以将 http 请求转化为其他通讯协议，可以提高通信的安全性。
![](/images/posts/jekyll/2017-08-23-TuJieHTTPReadingNote-14.jpg)
<br>

**3.隧道**：用于保持客户端与服务器端通信连接的应用程序，会使用 SSL 等加密手段进行通信，用于保证客户端与服务器之间通信的安全。
![](/images/posts/jekyll/2017-08-23-TuJieHTTPReadingNote-15.jpg)
<br><br>
第七章开始进入 HTTPS 部分，<br>
篇幅太大，所以在下一篇文章中摊开来讲。

<br><br>

### 参考

简书：[转交遇见陈绮贞](http://www.jianshu.com/u/5a89cd7d45c9)<br>
文章：[51 cto ](http://www.techweb.com.cn/network/system/2016-10-11/2407736.shtml)


