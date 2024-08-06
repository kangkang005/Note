# 子网掩码
## 什么是子网掩码
IP 地址本身不再记录划分信息，而是通过一个独立的数字序列来辅助标记，这就是子网掩码。

这个序列同样由 32 位二进制组成，例如：

```javascript
11111111 11111111 11111111 00000000
```

连续的 1 代表网络位，连续的 0 代表主机位。

但在展示时通常转化为十进制形式，例如上面的转化为十进制后：

```javascript
255.255.255.0
```

转换后前三组的 255，就表示一个 IP 地址中前三组数是网络号，而最后一组的 0 表示一个 IP 地址中后一组是主机号。比如我这里有一个 IP 地址以及它对应的子网掩码：

```javascript
// IP：
192.168.33.112
// 子网掩码：
255.255.255.0
```

说明这个 IP 地址 `192.168.33` 是**网络位**，`112` 是**主机位**。这就子网掩码的功能之一。

接着来介绍子网掩码的另外一个作用：判断设备是否在同一个子网！

## 什么是子网
比如两台笔记本电脑连接同一个 WIFI，那么他们就在同一个子网中或者说是同一个局域网中，即使路由器断开外网连接，这两台电脑仍能够相互通讯。

## 如何判断是否在同一个子网
前面提到子网掩码可以判断设备是否在同一个子网，怎么判断呢？

假如我们有一台 A 笔记本，一台 B 笔记本，不知道连接的是不是同一个 WIFI，可以通过查询我们得知：

A 笔记本的信息如下：

```javascript
// IP：
192.168.33.112
// 子网掩码：
255.255.255.0
```

B 笔记本的信息如下：

```javascript
// IP：
192.168.33.223
// 子网掩码：
255.255.255.0
```

通过 IP 地址的二进制格式与子网掩码的二进制格式进行 and 运算，如果相等，说明 AB 笔记本处于同一个子网，同一个 WIFI，可以直接通信。

来来来，我们来算下，先算 A 笔记本：

```javascript
11000000 10101000 00100001 01110000 // IP
&
11111111 11111111 11111111 00000000 // 子网掩码
// and运算理解为位相乘就可以了，上下每一位都相乘得
=
11000000 10101000 00100001 00000000
// 转成十进制为
192.168.33.0
```

同理 B 运算完并转成十进制后为：

```javascript
192.168.33.0
```

A 和 B 笔记本的运算结果相等，证明在同一个子网。

当然我们不会每次比较两个设备的时候都去这么计算，有子网掩码的分类快速去判断。

## 子网掩码的分类
首先子网掩码有如下分类：

* A 类：`255.0.0.0`
* B 类：`255.255.0.0`
* C 类：`255.255.255.0`

如果一个 IP 地址 `192.172.3.64` 配套的子网掩码是 `255.255.255.0`，那么这个 IP 就是属于 C 类，也就是说 IP 的最后一组是主机位，那么可能在同个子网下所有设备的 IP 地址范围为 `192.172.3.0 ~ 192.172.3.255`。

但在这个范围内：

* `192.172.3.0` 是**网络地址**，用于标识子网本身，不分配给任何设备。
* `192.172.3.255` 是**广播地址**，用于发送到该子网内所有设备的广播消息。
* 其余的地址（`192.172.3.1` 到 `192.172.3.254`）可以分配给子网内的设备。

当然，比之前的 IP 分类灵活的地方在于每一类还可以继续划分子网，被称为**可变长子网掩码**

## 可变长子网掩码
比如 C 类中，我想再划分出子网，可以通过网络位的扩展，占用主机位：

* `255.255.255.128 (/25)` - 二进制表示：`11111111.11111111.11111111.10000000`
* `255.255.255.192 (/26)` - 二进制表示：`11111111.11111111.11111111.11000000`
* `255.255.255.224 (/27)` - 二进制表示：`11111111.11111111.11111111.11100000`
* `255.255.255.240 (/28)` - 二进制表示：`11111111.11111111.11111111.11110000`
* `255.255.255.248 (/29)` - 二进制表示：`11111111.11111111.11111111.11111000`
* `255.255.255.252 (/30)` - 二进制表示：`11111111.11111111.11111111.11111100`
* `255.255.255.254 (/31)` - 二进制表示：`11111111.11111111.11111111.11111110`
* `255.255.255.255 (/32)` - 二进制表示：`11111111.11111111.11111111.11111111`

有点懵？我们慢慢来，就拿第二个举例好了，通过二进制表示我们可以看出，原本主机位前两个 00 变成了 11，这是因为网络位扩展了，占用了 2 个主机位。此时网络位个数为 8+8+8+2=26，主机位为 8-2=6 个。

所以 `255.255.255.192 (/26)` 就表示这个是个可变长子网掩码，且网络位为 26。当然真正电脑里展示的子网掩码只会是 `255.255.255.192`。

一般我们写 IP 地址为了突出子网掩码的信息，可以这么写：`192.168.11.30/26`，从后面这个 `/26` 就能够看出是一个 C 类的可变长子网。

注意了！子网掩码必须是连续的 1 后面跟着连续的 0，在二进制中不能有 1 和 0 交错的情况。例如不能是：`11111111.11111111.11111111.00111111`

那 `255.255.255.192` 究竟划分了几个子网呢？只需要看被占用的主机位有多少种组合，例如 `00，10，01，11`，也就是划分了 4 个子网。对应到 IP 地址的最后一组分别为

* 00 情况下的 `00000000-00111111` 转为 `0-63`
* 01 情况下的 `01000000-01111111` 转为 `64-127`
* 10 情况下的 `10000000-10111111` 转为 `128-191`
* 11 情况下的 `11000000-11111111` 转为 `192-255`

假设我有个 IP 地址的主机位是 `192.163.1`，子网的地址范围将是：

* 第一个子网：`192.163.1.0` 到 `192.163.1.63`
* 第二个子网：`192.163.1.64` 到 `192.163.1.127`
* 第三个子网：`192.163.1.128` 到 `192.163.1.191`
* 第四个子网：`192.163.1.192` 到 `192.163.1.255`

在每个子网中：

* 第一个地址（如 `192.163.1.0`, `192.163.1.64`, 等）是子网的网络地址，用于标识子网，不分配给设备。
* 最后一个地址（如 `192.163.1.63`, `192.163.1.127`, 等）是子网的广播地址，用于发送到该子网内所有设备的广播消息。
* 其余的地址（如 `192.163.1.1` 到 `192.163.1.62`, `192.163.1.65` 到 `192.163.1.126`, 等）可以分配给子网内的设备。

## 总结
* 将一个 IP 地址划分为网络位和主机位
* 判断 IP 是否在同一个子网以及划分子网