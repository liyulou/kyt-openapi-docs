# 一、地址充值｜提现风险预警接口

说明：支持地址充值或提现交易场景，预先检测地址风险(例如：是否是黑名单、是否直接或间接黑名单交易过等等)。

## 1、接口URL <a href="#id-1-jie-kou-url" id="id-1-jie-kou-url"></a>

GET /openapi/v2/risk/address/check

## 2、header参数 <a href="#id-2header-can-shu" id="id-2header-can-shu"></a>

<table data-header-hidden><thead><tr><th width="196"></th><th width="117"></th><th width="107"></th><th></th></tr></thead><tbody><tr><td><strong>参数名</strong></td><td><strong>数据类型</strong></td><td><strong>是否必传</strong></td><td><strong>描述</strong></td></tr><tr><td>timestamp</td><td>int</td><td>true</td><td>时间戳（单位s）</td></tr><tr><td>sign</td><td>string</td><td>true</td><td>签名sha256("timestamp=timestamp的值&#x26;secret=secretkey的值")</td></tr></tbody></table>

## 3、请求参数 <a href="#id-3-qing-qiu-can-shu" id="id-3-qing-qiu-can-shu"></a>

<table data-header-hidden><thead><tr><th width="193"></th><th width="119"></th><th width="110"></th><th></th></tr></thead><tbody><tr><td><strong>参数名</strong></td><td><strong>数据类型</strong></td><td><strong>是否必传</strong></td><td><strong>描述</strong></td></tr><tr><td>api_key</td><td>string</td><td>true</td><td>apikey</td></tr><tr><td>network</td><td>string</td><td>true</td><td>主网名称(Bitcoin、Ethereum、...... 详见《<strong>主网代币枚举值》</strong>)</td></tr><tr><td>address</td><td>string</td><td>true</td><td>钱包地址</td></tr><tr><td>address_role</td><td>string</td><td>true</td><td><p>地址角色（</p><p>from：转出地址；</p><p>to：转入地址</p><p>）</p></td></tr><tr><td>coin</td><td>string</td><td>true</td><td>代币名称(btc、eth、trx、bnb、usdt、usdc......详见<strong>主网代币枚举值</strong>)</td></tr><tr><td>app_id</td><td>string</td><td>true</td><td>应用id（在WEB端KYT配置页面获取）</td></tr><tr><td>value</td><td>float64</td><td>false</td><td>代币数量</td></tr><tr><td>query_indirect_risk</td><td>bool</td><td>false</td><td>是否查询间接风险（默认值true）</td></tr><tr><td>business_tag</td><td>string</td><td>false</td><td><p>业务类型（</p><p>钱包：wallet</p><p>交易所：exchange</p><p>NFT：nft...</p><p>等等</p><p>）</p></td></tr><tr><td>kyc_status</td><td>int</td><td>false</td><td><p>KYC状态（</p><p>1：已KYC认证</p><p>2：未KYC认证</p><p>）</p></td></tr><tr><td>kyc_level</td><td>int</td><td>false</td><td><p>KYC等级（</p><p>1：KYC 1级</p><p>2：KYC 2级</p><p>3：KYC 3级</p><p>4：KYC 4级</p><p>）</p></td></tr></tbody></table>

## 4、返回参数 <a href="#id-4-fan-hui-can-shu" id="id-4-fan-hui-can-shu"></a>

apikey过期或错误，返回：

```
{
    "code": -1,
    "data": {},
    "message": "api_key is invalid"
}
```

apikey和secrectkey验证通过，正常返回：

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

<table data-header-hidden><thead><tr><th width="314"></th><th width="115"></th><th></th></tr></thead><tbody><tr><td><strong>参数名</strong></td><td><strong>数据类型</strong></td><td><strong>描述</strong></td></tr><tr><td>code</td><td>Int</td><td><p>200：请求成功</p><p>-2：不支持该主网</p></td></tr><tr><td>message</td><td>string</td><td>接口请求状态描述</td></tr><tr><td>unique_id</td><td>string</td><td>唯一id（标识当前请求，用于查询历史记录）</td></tr><tr><td>risk_level</td><td>string</td><td><p>风险等级（</p><p>severe：严重</p><p>high：高风险</p><p>medium：中风险</p><p>low：低风险</p><p>none：未知</p><p>）</p></td></tr><tr><td>risk_code</td><td>int</td><td><p>风险code（</p><p>0：未知</p><p>-1：未查询到</p><p>4444：命中黑名单</p><p><strong>其他code说明详见：《risk_code说明书》</strong></p><p>）</p></td></tr><tr><td>risk_source</td><td>jsonArray</td><td>风险来源</td></tr><tr><td>risk_source.black_address_type</td><td>string</td><td>黑名单类型</td></tr><tr><td>risk_source.black_address_label</td><td>array</td><td>黑名单标签</td></tr><tr><td>risk_source.is_private_whitelist</td><td>bool</td><td>是否是私有白名单</td></tr><tr><td>risk_source.is_private_balcklist</td><td>bool</td><td>是否是私有黑名单</td></tr><tr><td>risk_source.direct_risk_list</td><td>jsonArray</td><td>地址的直接风险交易列表</td></tr><tr><td>risk_source.indirect_risk_list</td><td>jsonArray</td><td>地址的直接风险交易列表</td></tr></tbody></table>
