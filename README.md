
---简明Java IO---
# 理解IO PPT思路
    - 简明通信原理
        - 网络通信架构图
        - 什么是互联网

        互联网和公司内部的局域网都是基于 TCP/IP 的思路来设计的， 所以我们先来了解 TCP/IP 的基本思路。 TCP/IP 的结构如图 1.8 所示， 就是由一些小的子网，通过路由器 A 连接起来组成一个大的网络。 这里的子网可以理解为用集线器 B 连接起来的几台计算机 C，我们将它看作一个单位，称为子网。将子网通过路由器连接起来， 就形成了一个网络 D

        - 集线器，交换机，路由器，猫（调制解调），无线AP
        - wan,lan,vlan

    - 操作系统
        - Linux操作系统架构
        - 操作系统中断机制
        - 文件描述符
        - 标准输入输出
        - 网卡的工作方式

    - 进程通信方式
        - TCP/IP

    - 网络编程
        - Linux网络编程
        - select,poll,epoll

    - Java IO发展史
        - 代码体现各种IO的工作方式

    - java NIO





# 进程之间是如何通信的
- [常见的通信方式](https://www.cnblogs.com/LUO77/p/5816326.html)
- [程序间通信的各种途径及解析](https://www.cnblogs.com/wskaihd/archive/2009/07/22/1528471.html)

# 计算机网络简明教程
- [计算机网络简明教程及仿真实验](https://www.bilibili.com/video/av34135819/?p=5)


# IO中断
- 网卡中断



# question
- response 什么时间返回
- socket 返回过程
- 网卡工作原理


# linux
- 文件描述符

# accept
- jvm accept实现方式
    - Linux for
    - Linux accept

# 操作系统IO操作

# tcp/ip

# 理解 
- Java NIO就是对IO使用的封装，实现内核函数的调用

- 非阻塞I/O有一个缺点
    如果所有设备都一直没有数据到达，调用者需要反复查询做无用功，如果阻塞在那里，操作系统可以调度别的进程执行，就不会做无用功了。select(2) 函数可以阻塞地同时监视多个设备，还可以设定阻塞等待的超时时间，从而圆满地解决了这个问题。


- 搞懂select,poll,epoll区别
    - [聊聊IO多路复用之select、poll、epoll详解-区别](https://www.jianshu.com/p/dfd940e7fca2)
    - [Linux下的I/O复用与epoll详解](https://www.cnblogs.com/lojunren/p/3856290.html)



# Socket 编程中，TCP 流的结束标志与粘包问题(https://www.cnblogs.com/kirito-c/p/8670078.html)
```
因为 TCP 本身是无边界的协议，因此它并没有结束标志，也无法分包。

socket和文件不一样，从文件中读，读到末尾就到达流的结尾了，所以会返回-1或null，循环结束，但是socket是连接两个主机的桥梁，一端无法知道另一端到底还有没有数据要传输。
socket如果不关闭的话，read之类的阻塞函数会一直等待它发送数据，就是所谓的阻塞。

如果发送的东西非常多必须要用循环读，可以有以下解决方案：

调用socket的 shutdownOutput 方法（Java）关闭输出流，该方法的文档说明为，将此套接字的输出流置于“流的末尾”，这样另一端的输入流上的read操作就会返回-1。
约定结束标志，当读到该结束标志时退出不再read。 （Http 的 Transfer-Encoding: Chunked 首部，表示将以一个 length 为 0 的 chunk 做结束标志）
设置超时（timeout），会在设置的超时时间到达后抛出SocketTimeoutException异常而不再阻塞。
双方定义好通信协议，在协议头部约定好数据的长度。当读取到的长度等于这个长度时就不再继续调用read方法。（Http 的 content-length 首部，会给出主体的长度）
而如果需要发送多个相互独立的内容，内容之间就需要有明确的分界，方法有：

像 multipart-form 一样，使用 boundary 字串做分割，使用 Content-Type 等首部做内容标识。
用二进制帧做分割，在帧首部定义好帧的长度和其他信息。
```


# references
- [操作系统IO操作模式](https://blog.csdn.net/u012474535/article/details/80733118)
- [网络编程中Socket和TCP连接过程-学习笔记](https://blog.csdn.net/la745739773/article/details/91385275)
- [https://www.bilibili.com/video/av50961486](https://www.bilibili.com/video/av50961486)
- [Java NIO之Selector（选择器）](https://www.cnblogs.com/snailclimb/p/9086334.html)
- [Java BIO,NIO与AIO的区别](https://www.cnblogs.com/barrywxx/p/8430790.html)
- [一文让你彻底理解 Java NIO 核心组件](https://blog.csdn.net/javaxuexi123/article/details/81910644)
- [阿里面试必备之分析IO及NIO的底层原理](https://www.bilibili.com/video/av23594034/?spm_id_from=333.788.b_7265636f5f6c697374.4)
- [《操作系统》总结五（I/O管理）](https://blog.csdn.net/bigpudding24/article/details/48901473#t3)
- [操作系统IO模式整理](https://juejin.im/entry/5a72d7f36fb9a01ca8724e36)
- [C++网络通信中write和read的为什么会阻塞](https://blog.csdn.net/bian_qing_quan11/article/details/77853701)
- [Unix/Linux中的read和write函数](https://www.cnblogs.com/xiehongfeng100/p/4619451.html)
- [如何学习Java的NIO？](https://www.zhihu.com/question/29005375/answer/667616386)
- [理解socket connect和accept的实现细节](http://xiaorui.cc/2016/05/04/%E7%90%86%E8%A7%A3socket-connect%E5%92%8Caccept%E7%9A%84%E5%AE%9E%E7%8E%B0%E7%BB%86%E8%8A%82/)
- [从操作系统内核看Java非阻塞IO事件检测](https://blog.csdn.net/wangyangzhizhou/article/details/52573310)
- [Linux Socket编程（不限Linux）](https://www.cnblogs.com/skynet/archive/2010/12/12/1903949.html)
- [socket API 实现（四）—— accept 函数](http://blog.guorongfei.com/2014/10/29/socket-accept/)
- [浅谈Linux内存管理](https://zhuanlan.zhihu.com/p/67059173)
- [【Linux 内核网络协议栈源码剖析】accept 函数剖析](https://blog.csdn.net/wenqian1991/article/details/46794647)
- [linux阻塞和非阻塞原理](https://ezbcw.iteye.com/blog/2164778)
- [12.Redis的事件驱动（IO多路复用）](https://blog.csdn.net/u014590757/article/details/79860766)
- [Java IO多路复用技术详解](https://blog.csdn.net/weililansehudiefei/article/details/70885515)
- [系统间通讯方式之（Java NIO多路复用模式）（四）](https://blog.csdn.net/u010963948/article/details/78507255)
- [Java编程的艺术-NIO的原理](https://www.bilibili.com/video/av55255759?from=search&seid=9541834285236327097)
- [Java架构之一线互联网公司面试必问之NIO【咕泡学院】](https://www.bilibili.com/video/av29590429?from=search&seid=9541834285236327097)
- [深入分析 Java I/O 的工作机制](https://www.ibm.com/developerworks/cn/java/j-lo-javaio/index.html)
- [数据从网卡到应用的过程](https://chenyongjun.vip/articles/108)
- [集线器，交换机，路由器的区别](https://www.bilibili.com/video/av34083775?from=search&seid=16031193203558461900)
- [计算机网络——OSI模型究竟忽悠了多少人](https://www.cnblogs.com/6DAN_HUST/archive/2012/03/24/2415148.html)
- [TCP/IP与OSI之思想试比较 ](http://www.elias.cn/oldweb/bbs/viewtopicc54a.html?t=6)
- [BIO-NIO-AIO.md](https://github.com/Snailclimb/JavaGuide/blob/master/docs/java/BIO-NIO-AIO.md#13-%E4%BB%A3%E7%A0%81%E7%A4%BA%E4%BE%8B)
- [也说TCP/IP之计算机网络发展史（一）](https://blog.csdn.net/dengminghli/article/details/81491153)
