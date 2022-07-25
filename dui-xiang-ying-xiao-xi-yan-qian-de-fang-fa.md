---
description: >-
  在接口调用过程中，请求方在获取接收方的响应结果后，如果响应结果中包含了接收方返回的签名字符串，请求方可以对签名字符串进行验签，确认响应结果是否被篡改，保证接口调用的安全性。
---

# 对响应消息验签的方法

### 在厂商服务器验签规则 <a href="#h1-1582622204457" id="h1-1582622204457"></a>

示例代码如下：

```
    /**
     * 生成sign
     * @return
     */
    public static String generateCPSign(Map<String,Object> requestParams, final String cpAuthKey)
    {
        // 对消息体中查询字符串按字典序排序并且进行URLCode编码        |  Sort the request parameters in the message body based on the ASCII codes of their names and URL encode the parameter values.
        String baseStr = format(requestParams, cpAuthKey);
        // 用CP侧签名私钥对上述编码后的请求字符串进行签名      |  Sign the encoded request parameter string using the CP-side signature generation private key.
        //MD5加密,结果转换为大写字符
        String sign = encodeByMD5(baseStr).toUpperCase();
        return sign;
    }

    /**
     * 根据参数Map构造排序好的参数串        | Construct a string of sorted parameters based on the parameter map.
     *
     * @param params
     * @return
     */
    private static String format(Map<String, Object> params, String key)
    {
        StringBuffer base = new StringBuffer();
        Map<String, Object> tempMap = new TreeMap<String, Object>(params);
        // 获取计算nsp_key的基础串        | Obtain the base string for calculating nsp_key.
        try
        {
            for (Map.Entry<String, Object> entry : tempMap.entrySet())
            {
                String k = entry.getKey();
                String v = String.valueOf(entry.getValue());
                base.append(k).append("=").append(URLEncoder.encode(v, "UTF-8")).append("&");
            }
        }
        catch (UnsupportedEncodingException e)
        {
            e.printStackTrace();
        }
        base = base.append("key=" + key);
        String body = base.toString().substring(0, base.toString().length() - 1);

        // 空格和星号转义      | Escape spaces and asterisks (*).
        body = body.replaceAll("\\+", "%20").replaceAll("\\*", "%2A");
        return body;
    }


    /**
     * 对字符串进行MD5加密
     *
     * @param str 需要加密的字符串
     * @return 小写MD5字符串 32位
     */
    public static String encodeByMD5(String str) {
        MessageDigest digest;

        try {
            digest = MessageDigest.getInstance("MD5");
            digest.update(str.getBytes());
            return new BigInteger(1, digest.digest()).toString(16);
        } catch (NoSuchAlgorithmException e) {
            e.printStackTrace();
            return null;
        }
    }
```
