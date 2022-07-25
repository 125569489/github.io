# 1001 玩家发起交易订单

{% hint style="info" %}
**创建订单通知:** 在创建markOrder订单时会给配置了回调地址的厂商发送此通知
{% endhint %}

### 请求参数 <a href="#h1-1575107728215" id="h1-1575107728215"></a>

| 参数名称       | 必选(M)/可选(O) | 类型     | 是否参与验签 | 参数说明                                                                                                                                                        |
| ---------- | ----------- | ------ | ------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| type       | M           | int    | 是      | 回调类型 1001                                                                                                                                                   |
| contract   | M           | string | 是      | 合约地址                                                                                                                                                        |
| isOrderAsk | M           | int    | 是      | is\_order\_ask - 订单方向，1（卖），0（买）                                                                                                                             |
| signer     | M           | string | 是      | 签名者，就是创建订单者的地址                                                                                                                                              |
| amount     | M           | int    | 是      | 交易 NFT 的数量，ERC721 单次只能交易 1 个。ERC1155 合约可以批量交                                                                                                                |
| currency   | M           | string | 是      | <p></p><p>支付币种，0 代表是主网币 native coin，其它地址代表对应的 ERC20 代 币，USDC 或者 WETH</p>                                                                                    |
| price      | M           | string | 是      | 成交价                                                                                                                                                         |
| tokenId    | M           | long   | 是      | 订单的token\_id                                                                                                                                                |
| sign       | M           | string | 否      | <p>用于厂商服务器对通知消息进行验签的签名字符串，由链游平台服务器生成。<br>厂商服务器需要参考<a href="dui-xiang-ying-xiao-xi-yan-qian-de-fang-fa.md">对响应消息验的方法</a>对链游平台服务器发送的参数进行验签，验签通过后才能进行后续处理。</p> |

{% hint style="info" %}
说明：sign字段是由：其他字段排序完成之后，将所有参与签名的参数名和参数值的键值对以“&”字符连接成字符串，例如“a=xxxxxx\&b=xxxxxxx\&c=xxxxxxxxxxx...” 再进行MD5加密生成的延签字段，[生成方法示例](dui-xiang-ying-xiao-xi-yan-qian-de-fang-fa.md)
{% endhint %}

{% hint style="warning" %}
警告：以上“是否参与验签”列标识为“是”的参数，只有请求消息中携带且值不为null或""时才需要参与验签。
{% endhint %}

### &#x20;厂商需返回参数 <a href="#h1-1575107777227" id="h1-1575107777227"></a>

| 参数名称 | 必选(M)/可选(O) | 类型     | 参数含义                                                                                          |
| ---- | ----------- | ------ | --------------------------------------------------------------------------------------------- |
| code | M           | int    | <p>操作结果。取值范围如下：<br>● 1：成功。对于重复的订单，也要求返回1。<br>● 0：验签失败。<br>● 2：超时。</p><p>● 99：其他错误。</p><p></p> |
| msg  | M           | string | <p>返回消息。范围如下：<br>● SUCCESS：成功接收消息。</p><p><br>● 其他信息均为失败原因。</p>                                |



{% hint style="info" %}
警告：请厂商服务器在收到通知消息后，在完成最小必要处理后，立即返回响应消息，避免超时。返回结果请严格按照以上定义的返回码返回。
{% endhint %}

## 代码示例

厂商自行搭建web服务

{% swagger baseUrl="https://api.myapi.com/v1" method="post" path="/callback" summary="在项目信息中配置回调地址，用于接受链游平台的消息回调" %}
{% swagger-description %}
Creates a new pet.
{% endswagger-description %}

{% swagger-parameter in="body" name="name" required="true" type="string" %}
The name of the pet
{% endswagger-parameter %}

{% swagger-parameter in="body" name="owner_id" required="false" type="string" %}
The 

`id`

 of the user who owns the pet
{% endswagger-parameter %}

{% swagger-parameter in="body" name="species" required="false" type="string" %}
The species of the pet
{% endswagger-parameter %}

{% swagger-parameter in="body" name="breed" required="false" type="string" %}
The breed of the pet
{% endswagger-parameter %}

{% swagger-response status="200" description="Pet successfully created" %}
```javascript
{
    "name"="Wilson",
    "owner": {
        "id": "sha7891bikojbkreuy",
        "name": "Samuel Passet",
    "species": "Dog",}
    "breed": "Golden Retriever",
}
```
{% endswagger-response %}

{% swagger-response status="401" description="Permission denied" %}

{% endswagger-response %}
{% endswagger %}

{% hint style="info" %}
暂未提供
{% endhint %}

{% tabs %}
{% tab title="java" %}
```
```
{% endtab %}

{% tab title="Node" %}
```javascript
```
{% endtab %}

{% tab title="Python" %}
```python
```
{% endtab %}
{% endtabs %}
