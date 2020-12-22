# 异步通知



用户支付成功后，平台会发送异步通知到订单携带的notify\_url（如果有该参数的话），请求方式为 POST

请求参数：

| 字段名称 | 字段类型 | 必填参数 | 说明 |
| :--- | :--- | :--- | :--- |
| pay\_status | int\(1\) | Y | 1：支付成功 |
| total\_fee | int\(16\) | Y | 金额。单位：分 |
| out\_trade\_no | string\(32\) | Y | 用户端自主生成的订单号 |
| trade\_no | string\(32\) | Y | PAYJS 订单号 |
| transaction\_id | string\(32\) | Y | 微信用户手机显示订单号 |
| time\_end | string\(32\) | Y | 支付成功时间 |
| openid | string\(32\) | Y | 用户OPENID标示，本参数没有实际意义，旨在方便用户端区分不同用户 |
| attach | string\(127\) | N | 用户自定义数据 |
| mchid | string\(16\) | Y | AIPAY 商户号 |
| type | string\(16\) | N | 支付类型。微信订单不返回该字段；支付宝订单返回：alipay |
| sign | string\(32\) | Y | 数据签名 详见[签名算法]() |

接收回调流程示例：

```text
$data = $_POST;

if($data['pay_status'] == 1){
    // 1.验签逻辑

    // 2.验重逻辑

    // 3.自身业务逻辑

    // 4.返回 success 字符串（http状态码为200）
    echo 'success';
}
```

