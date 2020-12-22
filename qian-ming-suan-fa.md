# 签名算法

## 签名算法 <a id="&#x626B;&#x7801;&#x652F;&#x4ED8;-api"></a>

签名生成的通用步骤如下：

1. 设所有发送或者接收到的数据为集合M，将集合M内非空参数值的参数按照参数名ASCII码从小到大排序（字典序），使用URL键值对的格式（即key1=value1&key2=value2…）拼接成字符串stringA。
2. 在stringA最后拼接上`&key=密钥`得到stringSignTemp字符串，并对stringSignTemp进行MD5运算，再将得到的字符串所有字符转换为大写，得到sign值

特别注意以下重要规则：

* 参数名ASCII码从小到大排序（字典序）；
* 如果参数的值为空不参与签名；
* 参数名区分大小写；
* 验证调用返回或微信主动通知签名时，传送的sign参数不参与签名，将生成的签名与该sign值作校验。



## 举例 <a id="&#x4E3E;&#x4F8B;"></a>

例如传递的参数如下：

```text
mchid: 12345
total_fee: 1
out_trade_no: 123123123123
```

第一步：对参数按照key=value的格式，并按照参数名ASCII字典序排序如下

```text
mchid=12345&out_trade_no=123123123123&total_fee=1
```

第二步：对上一步中的字符串拼接`&key=密钥`

```text
mchid=12345&out_trade_no=123123123123&total_fee=1&key=xxxxxxxxx
```

第三步：对上一步中字符串取MD5值

```text
$sign = md5('mchid=12345&out_trade_no=123123123123&total_fee=1&key=xxxxxxxxx');
```

第四步：对上面md5值转化为大写

```text
$sign = strtoupper($sign);
```

## PHP代码示例 <a id="php&#x4EE3;&#x7801;&#x793A;&#x4F8B;"></a>

```text

function sign(array $data, $key) {
    ksort($data);
    $sign = strtoupper(md5(urldecode(http_build_query($data)).'&key='.$key));
    return $sign;
}


$data = [
    'mchid' => '12345',
    'total_fee' => 1,
    'out_trade_no' => '123123123123',
];


$key = 'xxxxxxxxxxx';

$sign = sign($data, $key);
```



