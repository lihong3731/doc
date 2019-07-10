# 支付对接文档

### 预下单
* 请求接口 `POST http://${domain}/pay/prepay`
* 请求参数

|请求参数 | 是否必须 | 说明 | 示例值 | 描述 |
|------|---|---|---|---|
|appId | 是 | 应用ID | zw200313430203613184 | 商户后台可以查看 | 
|name | 是 | 订单名称 | 测试订单名称 | 最大长度为64 | 
|amount | 是 | 金额（分） | 300 | 金额单位为分 | 
|payType | 是 | 支付方式 | pdd_weixin | pdd_weixin： 微信 pdd_alipay: 支付宝 | 
|nonceStr | 是 | 随机字符 | 123456 | 最大长度为32 | 
|sign | 是 | 签名 | 123456 | 签名算法看后面 | 
|orderNo | 是 | 订单号 | 123456 | 必须唯一 | 
|notifyUrl | 是 | 回调url | http://www.test.com/notify | 回调方式post | 
|signType | 是 | 签名方式 | md5 | 直接填写md5 | 
|body | 是 | 商品描述 | iphone 1 | 商品描述，不要太长就行 | 
|remark | 否 | 备注 | 买东西 | 备注，不要太长就行 | 
|ip | 否 | ip | 119.119.119.119 | ip | 

* 返回参数

```
{
    "code": 200,
    "data": {
        "prepayId": "1d94e9f885328bbcccf05a490a388d8c"
    }
}
```

|请求参数 | 是否必须 | 说明 | 示例值 | 描述|
|------|---|---|---|---|
|code | 是 | 返回码 | 100 | 200表示正常，其它的都是失败 | 
|data | 是 | 结果 |  | 返回结果 | 
|prepayId | 是 | 预支付id | 1d94e9f885328bbcccf05a490a388d8c | 预支付id, 支付时需要 | 


### 支付
* 使用上一步返回的 prepayId 支付
* `GET http://${domain}/pay/pdd?prepayId=${prepayId}`

### 签名方式
1. 设所有发送或者接收到的数据为集合M，将集合M内非空参数值的参数按照参数名ASCII码从小到大排序（字典序），使用URL键值对的格式（即key1=value1&key2=value2…）拼接成字符串stringA。
2. 在stringA最后拼接上key得到stringSignTemp字符串，并对stringSignTemp进行MD5运算，再将得到的字符串所有字符转换为小写，得到sign值signValue。
3. 看这个 https://pay.weixin.qq.com/wiki/doc/api/app/app.php?chapter=4_3#


### 支付回调
* 服务器使用POST方式回调预下单时，传入的notifyUrl接口
* 回调参数

|请求参数 | 是否必须 | 说明 | 示例值 | 描述 |
|------|---|---|---|---|
|result | 是 | 是否成功 | SUCCESS/FAIL | 是否成功 | 
|appId | 是 | 应用ID | zw200313430203613184 | 商户后台可以查看 | 
|payNo | 是 | 支付单号 | 200313430203613184 | 支付单号 | 
|payTime | 是 | 支付时间 | 2019-09-09 00:00:00 | 支付时间 | 
|amount | 是 | 金额（分） | 300 | 金额单位为分 | 
|payType | 是 | 支付方式 | pdd_weixin | pdd_weixin： 微信 pdd_alipay: 支付宝 | 
|nonceStr | 是 | 随机字符 | 123456 | 最大长度为32 | 
|sign | 是 | 签名 | 123456 | 签名算法看后面 | 
|orderNo | 是 | 订单号 | 123456 | 必须唯一 | 
|signType | 是 | 签名方式 | md5 | 直接填写md5 | 

### 查询
* 请求接口 `POST http://${domain}/pay/order/query`
* 请求参数

|请求参数 | 是否必须 | 说明 | 示例值 | 描述 |
|------|---|---|---|---|
|appId | 是 | 应用ID | zw200313430203613184 | 商户后台可以查看 | 
|nonceStr | 是 | 随机字符 | 123456 | 最大长度为32 | 
|sign | 是 | 签名 | 123456 | 签名算法看后面 | 
|orderNo | 是 | 订单号 | 123456 | 必须唯一 |  
|signType | 是 | 签名方式 | md5 | 直接填写md5 | 

* 返回参数

|请求参数 | 是否必须 | 说明 | 示例值 | 描述 |
|------|---|---|---|---|
|result | 是 | 是否成功 | SUCCESS/FAIL | 是否成功 | 
|appId | 是 | 应用ID | zw200313430203613184 | 商户后台可以查看 | 
|payNo | 是 | 支付单号 | 200313430203613184 | 支付单号 | 
|payTime | 是 | 支付时间 | 2019-09-09 00:00:00 | 支付时间 | 
|name | 是 | 订单名称 | 测试订单名称 | 最大长度为64 | 
|amount | 是 | 金额（分） | 300 | 金额单位为分 | 
|payType | 是 | 支付方式 | pdd_weixin | pdd_weixin： 微信 pdd_alipay: 支付宝 | 
|nonceStr | 是 | 随机字符 | 123456 | 最大长度为32 | 
|sign | 是 | 签名 | 123456 | 签名算法看后面 | 
|orderNo | 是 | 订单号 | 123456 | 必须唯一 | 
|signType | 是 | 签名方式 | md5 | 直接填写md5 | 
