# Rules 规则
## 规则格式

```bash
# 类型,参数,策略(,no-resolve)
TYPE,ARGUMENT,POLICY(,no-resolve)
```

`no-resolve` 选项是可选的，它用于跳过规则的 DNS 解析。当您想要使用 `GEOIP`、`IP-CIDR`、`IP-CIDR6`、`SCRIPT` 规则，但又不想立即将域名解析为 IP 地址时，这个选项就很有用了.

## 策略(POLICY)

目前有四种策略类型，其中:

* `DIRECT`: 通过 `interface-name` 直接连接到目标 (不查找系统路由表)
* `REJECT`: 丢弃数据包
* `Proxy`: 将数据包路由到指定的代理服务器
* `Proxy Group`: 将数据包路由到指定的策略组

## 常见的规则类型
以下部分介绍了每种规则类型及其使用方法:

### DOMAIN 域名
`DOMAIN,www.google.com,policy` 将 `www.google.com` 路由到 `policy`.

### DOMAIN-SUFFIX 域名后缀

`DOMAIN-SUFFIX,youtube.com,policy` 将任何以 `youtube.com` 结尾的域名路由到 `policy`.

在这种情况下，`www.youtube.com` 和 `foo.bar.youtube.com` 都将路由到 `policy`.

### DOMAIN-KEYWORD 域名关键字
`DOMAIN-KEYWORD,google,policy` 将任何包含 `google` 关键字的域名路由到 `policy`.

在这种情况下，`www.google.com` 或 `googleapis.com` 都将路由到 `policy`.

### IP-CIDR IPv4 地址段
IP-CIDR 规则用于根据数据包的目标 IPv4 地址路由数据包.

> WARNING
> 使用这种规则时，Clash 将域名解析为 IPv4 地址。如果要跳过 DNS 解析，请使用 no-resolve 选项.

`IP-CIDR,127.0.0.0/8,DIRECT` 将任何目标 IP 地址为 `127.0.0.0/8` 的数据包路由到 `DIRECT`.

### PROCESS-NAME 源进程名
PROCESS-NAME 规则用于根据发送数据包的进程名称路由数据包.

`PROCESS-NAME,nc,DIRECT` 将任何来自进程 `nc` 的数据包路由到 `DIRECT`.

### PROCESS-PATH 源进程路径
PROCESS-PATH 规则用于根据发送数据包的进程路径路由数据包.

`PROCESS-PATH,/usr/local/bin/nc,DIRECT` 将任何来自路径为 `/usr/local/bin/nc` 的进程的数据包路由到 `DIRECT`.

### 配置文件
```yaml
proxies:
	- { name: 美国USLA-T-GPT, type: trojan, server: usla.mjt000.com, port: 443, password: 4bd2af94-79cd-490b-88e7-b984d3648359, udp: true, sni: usla.mjt000.com }
	- { name: 卢森堡LUX-T, type: trojan, server: lux.mjt000.com, port: 443, password: 4bd2af94-79cd-490b-88e7-b984d3648359, udp: true, sni: lux.mjt000.com }
	...

proxy-groups:
	- { name: 节点选择, type: select, proxies: [自动选择, 故障转移, 境内使用, 海外使用, '剩余流量：61.73 GB', 套餐到期：长期有效, 日本-优化]}
    - { name: ChatGPT, type: select, proxies: [节点选择, 美国USLA-T-GPT, 美国LA-优化-GPT, 美国LA-优化2-GPT, 美国LA-优化3-GPT] }
	- { name: 磁力下载, type: select, proxies: [DIRECT, 卢森堡LUX-T] }
	...

rules:
    - 'DOMAIN,api.mojie.ws,DIRECT'
	- 'DOMAIN-SUFFIX,openai.com,ChatGPT'
    - 'DOMAIN-KEYWORD,openai,ChatGPT'
    - 'DOMAIN-SUFFIX,coze.com,ChatGPT'
	- 'PROCESS-NAME,Thunder,磁力下载'
    - 'PROCESS-NAME,DownloadService,磁力下载'
    - 'PROCESS-NAME,qBittorrent,磁力下载'
	- 'IP-CIDR,127.0.0.1/32,REJECT,no-resolve'
	...
```

## 参考
https://clash.wiki/configuration/rules.html