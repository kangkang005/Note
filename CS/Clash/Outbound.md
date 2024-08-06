# Outbound 出站

Clash 中有几种类型的出站。每种类型都有自己的特点和使用场景。在此，我们将介绍每种类型的通用特点以及如何使用和配置它们.

## Proxies 代理节点

Proxies 代理节点是您可以配置的一些出站目标。就像代理服务器一样，您在这里为数据包定义目的地.

### Shadowsocks
Clash 支持以下 Shadowsocks 的加密方法:

| 系列 | 加密方法                                                                               |
| :--- | :------------------------------------------------------------------------------------- |
| AEAD | aes-128-gcm, aes-192-gcm, aes-256-gcm, chacha20-ietf-poly1305, xchacha20-ietf-poly1305 |
| 流式 | aes-128-cfb, aes-192-cfb, aes-256-cfb, rc4-md5, chacha20-ietf, xchacha20               |
| 块式 | aes-128-ctr, aes-192-ctr, aes-256-ctr                                                  |

### ShadowsocksR
Clash 也支持声名狼藉的反审查协议 ShadowsocksR.

支持以下 ShadowsocksR 的加密方法:

| 系列 | 加密方法                                                                 |
| :--- | :----------------------------------------------------------------------- |
| 流式 | aes-128-cfb, aes-192-cfb, aes-256-cfb, rc4-md5, chacha20-ietf, xchacha20 |

支持的混淆方法:

* plain
* http_simple
* http_post
* random_head
* tls1.2_ticket_auth
* tls1.2_ticket_fastauth

支持的协议:

* origin
* auth_sha1_v4
* auth_aes128_md5
* auth_aes128_sha1
* auth_chain_a
* auth_chain_b

### Vmess
Clash 支持以下 Vmess 的加密方法:

* auto
* aes-128-gcm
* chacha20-poly1305
* none

### Socks5
此外，Clash 还支持 Socks5 代理.

### HTTP
Clash 也支持 HTTP 代理.

### Snell
作为可选的反审查协议，Clash 也集成了对 Snell 的支持.

### Trojan
Clash 内置了对流行协议 Trojan 的支持:

## Proxy Groups 策略组
Proxy Groups 策略组用于根据不同策略分发规则传递过来的请求，其可以直接被规则引用，也可以被其他策略组引用，而最上级策略组被规则引用.

### relay 中继
请求将依次通过指定的代理服务器进行中继，目前不支持 UDP. 指定的代理服务器不应包含另一个 relay 中继.

### url-test 延迟测试
Clash 会周期性地通过指定的 URL 向列表中的代理服务器发送 HTTP HEAD 请求来测试每个代理服务器的延迟. 可以设置最大容忍值、测试间隔和目标 URL.

### fallback 可用性测试
Clash 会周期性地通过指定的 URL 向列表中的代理服务器发送 HTTP HEAD 请求来测试每个代理服务器的可用性. 第一个可用的服务器将被使用.

### load-balance 负载均衡
相同 eTLD+1 的请求将使用同一个代理服务器.

### select 手动选择
Clash 启动时默认使用策略组中的第一个代理服务器。用户可以使用 RESTful API 选择要使用的代理服务器。在此模式下，您可以在配置中硬编码服务器或使用 Proxy Providers 代理集 动态添加服务器.

无论哪种方式，有时您也可以使用直接连接来路由数据包。在这种情况下，您可以使用 DIRECT 直连出站.

要使用不同的网络接口，您需要使用包含 DIRECT 直连出站的策略组，并设置 `interface-name` 选项.

```yaml
- name: "My Wireguard Outbound"
  type: select
  interface-name: wg0
  proxies: [ 'DIRECT' ]
```