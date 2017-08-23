---
layout: post
title: 《图解 HTTP》阅读笔记(立 flag)
date: 2017-08-23 
tags:  Internet   
---

<br><br>

之前草草读了一遍《图解 HTTP》这本书<br>
很多东西都似懂非懂，所以重新读一遍，整理一些笔记。<br>

### HTTP 基础

#### **·简述**

HTTP (HyperText Transfer Protocol, 超文本**传输**协议) 是 Web 信息共享的规范和基础。<br>
值得注意的是，HTTP 并**不是**被设计为一种**传输协议**（transport protocol），它是一种**转移协议**（transfer protocol）。<br><br>
非常不幸，HTTP 刚刚传入我国时，即被错误翻译为“超文本传输协议”，<br>
因为 “transport” 和 “transfer” 在中文中都具有 “传输” 的含意，之后以讹传讹贻害无穷。(摘自[百度百科](https://baike.baidu.com/item/超文本转移协议/1675080?fr=aladdin))<br><br>
在 [IETF](https://baike.baidu.com/item/互联网工程任务组/707674?fr=aladdin&fromid=2800318&fromtitle=IETF) 的 [RFC](https://baike.baidu.com/item/RFC/1840) 中 (某组织的某文件中)<br>
**“transport”（传输）的含义是指**：从端到端（例如从 ip1:port1 到 ip2:port2 ）可靠地搬运比特，也就是TCP/IP协议栈中的第3层传输层（transport layer）协议所做的那些事情。<br>
**“而 transfer”（转义） 的含义是**：通过在客户端-服务器端之间转移一些带有操作语义的操作原语，来执行某种操作。<br>
“transfer”是TCP/IP协议栈中的第4层应用层的概念，而不是第3层传输层的概念。“transfer”所转移的是带有明确操作语义的操作原语，而不是没有操作语义的比特流。<br><br>
HTTP 三个版本：**0.9、1.0、1.1** (更新慢)。
<br><br>

#### **·网络基础**

网络是在 TCP/IP 协议族的基础上运作的，HTTP 是它的子集。<br>
TCP/IP 是在 IP 协议的通讯过程中，使用到的协议族的统称。<br>
它被分为四层：<br>
　　1.应用层：决定了向用户提供应用服务时的通信活动，如FTP，DNS和HTTP等；<br>
　　2.传输层：提供处于网络连接中的两台计算机之间的数据传输，TCP，UDP；<br>
　　3.网络层：用来处理网络上流动的数据包，IP协议；<br>
　　4.链路层：网络连接的硬件部分。<br>
<br>
数据在各层中封装后进行传输
![](/images/posts/jekyll/2017-08-23-TuJieHTTPReadingNote-01.jpg)


