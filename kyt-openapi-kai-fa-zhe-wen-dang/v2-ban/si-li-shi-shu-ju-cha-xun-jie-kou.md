# 四、历史数据查询接口

说明：根据报警接口返回的unique\_id，查询历史数据记录。

## 1、接口URL <a href="#id-1-jie-kou-url" id="id-1-jie-kou-url"></a>

GET /openapi/v2/risk/data/push

## 2、header参数 <a href="#id-2header-can-shu" id="id-2header-can-shu"></a>

<table data-header-hidden><thead><tr><th width="163"></th><th width="108"></th><th width="109"></th><th></th></tr></thead><tbody><tr><td><strong>参数名</strong></td><td><strong>数据类型</strong></td><td><strong>是否必传</strong></td><td><strong>描述</strong></td></tr><tr><td>timestamp</td><td>int</td><td>true</td><td>时间戳（单位s）</td></tr><tr><td>sign</td><td>string</td><td>true</td><td>签名sha256("timestamp=timestamp的值&#x26;secret=secretkey的值")</td></tr></tbody></table>

## 3、请求参数 <a href="#id-3-qing-qiu-can-shu" id="id-3-qing-qiu-can-shu"></a>

<table data-header-hidden><thead><tr><th width="163"></th><th width="109"></th><th width="110"></th><th></th></tr></thead><tbody><tr><td><strong>参数名</strong></td><td><strong>数据类型</strong></td><td><strong>是否必传</strong></td><td><strong>描述</strong></td></tr><tr><td>api_key</td><td>string</td><td>true</td><td>apikey</td></tr><tr><td>unique_id</td><td>string</td><td>true</td><td>唯一id</td></tr></tbody></table>

## 4、返回参数 <a href="#id-4-fan-hui-can-shu" id="id-4-fan-hui-can-shu"></a>

```json
{
    "code": 200,
    "msg": "success",
    "data": { 
        "risk_data": {
            "unique_id": "0140......8be5", //唯一标识id
            "risk_level": "severe", //风险等级（严重、高、中、低、未知）
            "risk_code": 4444 //风险code
            "risk_source": {
                "is_private_whitelist": false, //是否命中私有白名单  
                "risk_from_address_list":[ //风险转出地址
                    { 
                        "black_address":"3E5L......44Bc",//交易的from地址
                        "black_address_type": "Blackmail Scam", //黑名单地址类型
                        "black_address_label": [ //黑名单地址标签
                            "attacker",
                            "hacker"
                        ],
                    },
                    ......
                ],
                .......
            }
        }
    }
}
```

<table data-header-hidden><thead><tr><th width="149"></th><th width="117"></th><th></th></tr></thead><tbody><tr><td><strong>参数名</strong></td><td><strong>数据类型</strong></td><td><strong>描述</strong></td></tr><tr><td>risk_data</td><td>json</td><td>历史检测记录详情</td></tr></tbody></table>
