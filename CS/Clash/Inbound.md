# Inbound 入站

Clash 支持多种入站协议，包括:

* SOCKS5
* HTTP(S)
* Redirect TCP
* TProxy TCP
* TProxy UDP
* Linux TUN 设备 (仅 Premium 版本)

任何入站协议的连接都将由同一个内部规则匹配引擎处理。也就是说，Clash 目前不支持为不同的入站协议设置不同的规则集.

## 配置

```yaml
# HTTP(S) 代理服务端口
# port: 7890

# SOCKS5 代理服务端口
socks-port: 7891

# HTTP(S) 和 SOCKS4(A)/SOCKS5 代理服务共用一个端口
mixed-port: 7890

# Linux 和 macOS 的透明代理服务端口 (TCP 和 TProxy UDP 重定向)
# redir-port: 7892

# Linux 的透明代理服务端口 (TProxy TCP 和 TProxy UDP)
# tproxy-port: 7893

# 设置为 true 以允许来自其他 LAN IP 地址的连接
# allow-lan: false
```

## Mixed 混合端口

混合端口是一个特殊的端口，它同时支持 HTTP (S) 和 SOCKS5 协议。您可以使用任何支持 HTTP 或 SOCKS 代理的程序连接到这个端口