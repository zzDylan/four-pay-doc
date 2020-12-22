# 订单查询

用户发起支付后，可通过本接口发起订单查询来确认订单状态

请求地址：[https://xxx.com/api/check](https://payjs.cn/api/check)

请求参数：

| 字段名称 | 字段类型 | 必填参数 | 说明 |
| :--- | :--- | :--- | :--- |
| trade\_no | string\(32\) | Y | AIPAY平台订单号 |
| sign | string\(32\) | Y | 数据签名 详见签名算法章节 |

请求返回：

| 字段名称 | 字段类型 | 必填参数 | 说明 |
| :--- | :--- | :--- | :--- |
| code | int | Y | 1:请求成功 0:请求失败 |
| mchid | string\(32\) | Y | PAYJS 平台商户号 |
| out\_trade\_no | string\(32\) | Y | 用户端订单号 |
| trade\_no | string\(32\) | Y | PAYJS 订单号 |
| transaction\_id | string\(32\) | N | 微信显示订单号 |
| status | int\(1\) | Y | 0：未支付，1：支付成功 |
| openid | string\(32\) | N | 用户 OPENID |
| total\_fee | int\(16\) | N | 订单金额 |
| paid\_at | string\(32\) | N | 订单支付时间 |
| attach | string\(127\) | N | 用户自定义数据 |
| sign | string\(32\) | Y | 数据签名 详见签名算法章节 |

提示：请做好用户端订单号的唯一性处理。

此接口用户订单状态的**辅助查询**，请勿直接使用此接口做订单状态的高频轮询，调用频率过高可能会导致IP进入黑名单

正确的业务逻辑：商户侧服务器通过接收异步通知后更新自己订单状态，用户前端轮询应放在商户侧订单状态



