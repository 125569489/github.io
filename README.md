---
description: 更新时间 2022-07-22
---

# 厂商回调接口文档

## 调用场景

如果厂商在创建项目时配置回调地址，则会收到相关通知

重发机制：共48小时，前3次每30秒尝试一次，4-20次每300秒尝试一次，之后每3小时尝试一次。

{% hint style="info" %}
说明： 为保证可靠性，系统具备补偿机制，所以可能出现重发的通知比预期的多。
{% endhint %}

## 接口原型

| 承载协议  | HTTP/HTTPS POST                                                                       |
| ----- | ------------------------------------------------------------------------------------- |
| 接口方向  | 链游平台服务器->厂商服务器                                                                        |
| 接口URL | URL: 由厂商在创建项目时配置回调地址                                                                  |
| 数据格式  | <p>请求消息：Content-Type:   application/json<br>响应消息：Content-Type:   application/json</p> |

{% hint style="info" %}
说明：本接口采用的是Content-Type:   application/json格式，接收端代码框架需要支持自动解码。
{% endhint %}

## 接口功能

用于给厂商同步项目相关消息包含以下消息类型

{% content-ref url="1001-wan-jia-fa-qi-jiao-yi-ding-dan.md" %}
[1001-wan-jia-fa-qi-jiao-yi-ding-dan.md](1001-wan-jia-fa-qi-jiao-yi-ding-dan.md)
{% endcontent-ref %}

{% content-ref url="1002-wan-jia-que-ren-jiao-yi-ding-dan.md" %}
[1002-wan-jia-que-ren-jiao-yi-ding-dan.md](1002-wan-jia-que-ren-jiao-yi-ding-dan.md)
{% endcontent-ref %}

{% content-ref url="1003-he-yue-shang-lian-cheng-gong.md" %}
[1003-he-yue-shang-lian-cheng-gong.md](1003-he-yue-shang-lian-cheng-gong.md)
{% endcontent-ref %}

{% content-ref url="1004-transfer721-he-yue.md" %}
[1004-transfer721-he-yue.md](1004-transfer721-he-yue.md)
{% endcontent-ref %}

{% content-ref url="1005-transfer20-he-yue.md" %}
[1005-transfer20-he-yue.md](1005-transfer20-he-yue.md)
{% endcontent-ref %}

{% content-ref url="1006-transfer1155-he-yue.md" %}
[1006-transfer1155-he-yue.md](1006-transfer1155-he-yue.md)
{% endcontent-ref %}

{% content-ref url="1007-shou-quan-approve721-he-yue.md" %}
[1007-shou-quan-approve721-he-yue.md](1007-shou-quan-approve721-he-yue.md)
{% endcontent-ref %}

{% content-ref url="1008-shou-quan-approve20-he-yue.md" %}
[1008-shou-quan-approve20-he-yue.md](1008-shou-quan-approve20-he-yue.md)
{% endcontent-ref %}

{% content-ref url="1009-shou-quan-approve1155-he-yue.md" %}
[1009-shou-quan-approve1155-he-yue.md](1009-shou-quan-approve1155-he-yue.md)
{% endcontent-ref %}

{% content-ref url="1010-chang-shang-hash-mi-yue-tong-zhi.md" %}
[1010-chang-shang-hash-mi-yue-tong-zhi.md](1010-chang-shang-hash-mi-yue-tong-zhi.md)
{% endcontent-ref %}

## 接口约束

不允许厂商服务器设置IP允许清单用于限制链游平台侧的出口IP地址。IP允许清单本身并不能提高安全性且会给业务发展带来约束，在消息层面已有更安全的签名机制条件下，没有存在价值。不遵守该约定而导致的后果将由厂商自行承担。
