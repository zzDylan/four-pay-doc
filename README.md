# 生成订单

请求地址：[网关地址?mchid=商户号&total\_fee=金额&out\_trade\_no=订单号&notify\_url=异步通知url&sign=XXX](/网关地址?mchid=商户号&total_fee=金额&out_trade_no=订单号&notify_url=异步通知url&sign=XXX)

同步请求

请求方式:get

| 字段名称 | 字段类型 | 必填参数 | 说明 |
| :--- | :--- | :--- | :--- |
| mchid | string | Y | 商户号 |
| total\_fee | int | Y | 金额。单位：分 |
| out\_trade\_no | string | Y | 用户端自主生成的订单号 |
| notify\_url | string | Y | 异步通知url |
| return\_url | string | N | 支付完毕之后跳转到的商家网址 |
| sign | string | Y | 加密参数 |



