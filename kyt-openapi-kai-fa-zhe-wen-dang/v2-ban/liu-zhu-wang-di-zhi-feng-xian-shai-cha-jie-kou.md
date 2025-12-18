# 六、主网地址风险筛查接口

说明：预先检测地址风险(例如：是否是黑名单、是否直接或间接黑名单交易过等等)。

注意：此接口不执行规则引擎逻辑。

## 1、接口URL

GET /openapi/v2/risk/address/screening

## 2、header参数

<table data-header-hidden><thead><tr><th width="187"></th><th width="118"></th><th width="141"></th><th></th></tr></thead><tbody><tr><td><strong>参数名</strong></td><td><strong>数据类型</strong></td><td><strong>是否必传</strong></td><td><strong>描述</strong></td></tr><tr><td>timestamp</td><td>int</td><td>true</td><td>时间戳（单位s）</td></tr><tr><td>sign<br></td><td>string<br></td><td>true<br></td><td>签名sha256("timestamp=timestamp的值&#x26;secret=secretkey的值")</td></tr></tbody></table>

## 3、请求参数

<table data-header-hidden><thead><tr><th width="187"></th><th width="117"></th><th width="141"></th><th></th></tr></thead><tbody><tr><td><strong>参数名</strong></td><td><strong>数据类型</strong></td><td><strong>是否必传</strong></td><td><strong>描述</strong></td></tr><tr><td>api_key</td><td>string</td><td>true</td><td>apikey</td></tr><tr><td>network</td><td>string</td><td>true</td><td>主网</td></tr><tr><td>address</td><td>string</td><td>true</td><td>钱包地址</td></tr><tr><td>query_indirect_risk</td><td>bool</td><td>false</td><td>是否查询间接风险（默认值false）</td></tr></tbody></table>

## 4、返回参数

```json
{
    "code": 200, //200:代表成功
    "msg": "success",
    "data": {
        "unique_id": "0140......8be5", //唯一标识id(用于查询历史记录) 
        "risk_level": "severe", //风险等级（严重、高、中、低、未知）
        "risk_code": 4444, //风险code
        "risk_source": { //风险来源
            "is_private_whitelist": false, //是否命中私有白名单  
            "is_private_balcklist": false, //是否命中私有黑名单
            "private_balcklist_name":"私有黑名单名称",
            "black_address_type": "Blackmail Scam", //黑名单类型
            "black_address_label": [ //黑名单标签
                "attacker",
                "hacker"
            ],
            "direct_risk_list":[ //直接风险交易列表
                {
                    "black_address": "1KHw......aGbX", //直接交易的黑名单地址
                    "black_address_type": "Blackmail Scam", //风险类型
                    "tx_hash": "2bc34......b693", //交易hash
                    "black_address_label": [ //黑名单标签
                        "attacker",
                        "hacker"
                    ],
                }, 
                ......
            ],
            "indirect_risk_list":[ //间接风险交易列表
                {
                    "indirect_level": 2, //间接层级
                    "black_address":"0x99......4bE1", //间接交易的黑名单
                    "black_address_type": "Blackmail Scam", //风险类型
                    "indirect_tx_list":[ //间接交易hash
                        "0x74......2a90",
                        "0x56......9d4b"
                    ],
                    "black_address_label": [ //黑名单标签
                        "attacker",
                        "hacker"
                    ],
                },
                ......
            ]
        }
    }
}
```

<table data-header-hidden><thead><tr><th width="297"></th><th width="132"></th><th></th></tr></thead><tbody><tr><td><strong>参数名</strong></td><td><strong>数据类型</strong></td><td><strong>描述</strong></td></tr><tr><td>code</td><td>Int<br></td><td>200：请求成功-2：不支持该主网</td></tr><tr><td>message</td><td>string</td><td>接口请求状态描述</td></tr><tr><td>unique_id</td><td>string</td><td>唯一id（标识当前请求，用于查询历史记录）</td></tr><tr><td>risk_level<br></td><td>string<br></td><td>风险等级（severe：严重high：高风险medium：中风险low：低风险none：未知）</td></tr><tr><td>risk_code<br></td><td>int<br></td><td>风险code（0：未知-1：未查询到4444：命中黑名单<strong>其他code说明详见：《risk_code说明书》</strong>）</td></tr><tr><td>risk_source</td><td>json</td><td>风险来源</td></tr><tr><td>risk_source.is_private_whitelist</td><td>boolean</td><td>是否命中私有白名单</td></tr><tr><td>risk_source.is_private_blacklist</td><td>boolean</td><td>是否命中私有黑名单</td></tr><tr><td>risk_source.black_address_type</td><td>string</td><td>地址的黑名单类型</td></tr><tr><td>risk_source.black_address_label</td><td>stringArray</td><td>地址的黑名单标签</td></tr><tr><td>risk_source.direct_risk_list</td><td>jsonArray</td><td>地址参与的直接风险交易列表</td></tr><tr><td>risk_source.indirect_risk_list</td><td>jsonArray</td><td>地址参与的间接风险交易列表</td></tr></tbody></table>
