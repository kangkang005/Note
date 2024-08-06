# 端口(port)
## 什么是网络端口？

在网络技术中，*端口*包括**逻辑端口**和**物理端口**两种类型。

**物理端口**是用于连接物理设备之间的接口，如 ADSL Modem、集线器、交换机、路由器上用于连接其他网络设备的接口。

**逻辑端口**是指逻辑意义上用于区分服务的端口，比如用于浏览网页服务的 80 端口，用于 FTP 服务的 21 端口等。

我们这里讲的是逻辑端口。不是计算机硬件的 I/O 端口，而是**软件形式**上的概念。

工具提供服务类型的不同，端口分为两种: TCP 端口, UDP 端口。

计算机之间相互通信的时候，分为两种方式：

* 一种是发送信息以后，**可以确认信息是否到达**，也就是有应答的方式，这种方式大多采用 **TCP 协议**
* 一种是发送以后就不管了，**不去确认信息是否到达**，这种方式大多采用 **UDP 协议**。

对应这两种协议的服务提供的端口，也就分为 **TCP 端口**和 **UDP 端口**

## 端口的作用

端口号的主要作用是表示一台计算机中的**特定进程**所提供的服务。网络中的计算机是通过 IP 地址来代表其身份的，它只能表示某台特定的计算机，但是一台计算机上可以同时提供很多个服务，如数据库服务、FTP 服务、Web 服务等，我们就**通过端口号来区别相同计算机所提供的这些不同的服务**，如常见的端口号 21 表示的是 FTP 服务，端口号 23 表示的是 Telnet 服务，端口号 25 指的是 SMTP 服务等。

## 端口的特点
* 端口号是一个 2 字节 16 位的整数；
* 端口号用来标识一个进程，告诉操作系统，当前这个数据交给哪一个程序进行解析；
* IP 地址 + 端口号能标识网络上的某一台主机的某一个进程；
* 一个端口号只能被一个进程占用。

## 端口的分类

TCP 与 UDP 段结构中端口地址都是 **16 比特**，可以有在 0---65535 范围内的端口号。

**按照端口号分类：**

* **公认端口：0~1023**。它们紧密绑定于一些服务，通常这些端口的通讯明确表明了某种服务的协议，如：80 端口对应与 HTTP 通信，21 端口绑定与 FTP 服务，25 端口绑定于 SMTP 服务，135 端口绑定与 RPC（远程过程调用）服务。
* **动态端口: 1024~**:
之所以称为动态端口，是因为它 一般不固定分配某种服务，而是动态分配。动态分配是指当一个系统进程或应用 程序进程需要网络通信时，它向主机申请一个端口，主机从可用的端口号中分配 一个供它使用。当这个进程关闭时，同时也就释放了所占用的端口号。
	* **注册端口：1024~49151**。它们松散的绑定于一些服务，也就是说有许多服务绑定于这些端口，这些端口同样用于其他许多目的，如：许多系统处理端口从 1024 开始
	* **动态或私有端口：49152~65535**。理论上，不应为服务分配这些端口，通常机器从 1024 开始分配动态端口。例外：SUN 的 RPC 端口从 32768 开始。

**按照协议类型分类：** 按协议类型划分可分为 TCP 端口、UDP 端口、IP 端口、ICMP。

* **TCP 端口**：即传输控制协议端口，需要在客户端和服务器之间建立连接，这样可以提供可靠的数据传输。常见的包括 FTP 的 21 端口，Telnet 的 23 端口，SMTP 的 25 端口，HTTP 的 80 端口。
* **UDP 端口**：即用户数据报协议端口，无需在客户端和服务器端建立连接，安全性得不到保障。常见的 DNS 的 53 端口，SNMP（简单网络管理协议）的 161 端口，QQ 使用的 8000 和 4000 端口。
* **保留端口**：UNIX 有保留端口号的概念，只有超级用户特权的进程才允许给它自己分配一个保留端口号。这些端口号介于 1~1023 之间，一些应用程序将它作为客户与服务器认证的一部分。

## 端口使用的注意事项

* 不要使用端口号小于 1024 的端口。
* 端口号一般习惯为 4 位整数，在同一台计算机上端口号不能重复，否则，会产生端口号冲突。
* 客户端端口号因存在时间很短暂又称临时端口号，大多数 TCP/IP 实现给临时端口号分配 1024 ~ 5000 之间的端口号。大于 5000 的端口号是为其他服务器预留的 。

## 端口大全
https://cloud.tencent.com/developer/article/1897800

## 参考
https://blog.csdn.net/qq_21989927/article/details/109812089
https://cloud.tencent.com/developer/article/1897800