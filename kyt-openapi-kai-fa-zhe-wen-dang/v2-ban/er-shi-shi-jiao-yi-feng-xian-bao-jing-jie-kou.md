# 二、实时交易风险报警接口

说明：支持最新实时交易（最近48小时内），对交易hash进行风险检测（参与交易的地址是否包含黑名单、交易地址是否直接或间接和黑名单进行过交易、交易中接收地址交易金额是否超过AML阈值等等）

## 1、接口URL <a href="#id-1-jie-kou-url" id="id-1-jie-kou-url"></a>

GET /openapi/v2/risk/tx/check

## 2、header参数 <a href="#id-2header-can-shu" id="id-2header-can-shu"></a>

<table data-header-hidden><thead><tr><th width="187"></th><th width="127"></th><th width="130"></th><th></th></tr></thead><tbody><tr><td><strong>参数名</strong></td><td><strong>数据类型</strong></td><td><strong>是否必传</strong></td><td><strong>描述</strong></td></tr><tr><td>timestamp</td><td>int</td><td>true</td><td>时间戳（单位s）</td></tr><tr><td>sign</td><td>string</td><td>true</td><td>sha256("timestamp=timestamp的值&#x26;secret=secretkey的值")</td></tr></tbody></table>

## 3、请求参数 <a href="#id-3-qing-qiu-can-shu" id="id-3-qing-qiu-can-shu"></a>

<table data-header-hidden><thead><tr><th width="187"></th><th width="124"></th><th width="125"></th><th></th></tr></thead><tbody><tr><td><strong>参数名</strong></td><td><strong>数据类型</strong></td><td><strong>是否必传</strong></td><td><strong>描述</strong></td></tr><tr><td>api_key</td><td>string</td><td>true</td><td>apikey</td></tr><tr><td>tx</td><td>string</td><td>true</td><td>交易hash(支持查询最近72小时的交易hash)</td></tr><tr><td>network</td><td>string</td><td>true</td><td>主网名称(Bitcoin、Ethereum...... 详见《<strong>主网代币枚举值》</strong>)</td></tr><tr><td>to_address</td><td>string</td><td>true</td><td>接收地址</td></tr><tr><td>coin</td><td>string</td><td>true</td><td>代币名称(btc、eth、trx、bnb、usdt、usdc......详见<strong>主网代币枚举值接口</strong>)</td></tr><tr><td>app_id</td><td>string</td><td>true</td><td>应用id(在WEB端KYT配置页面获取)</td></tr><tr><td>query_indirect_risk</td><td>bool</td><td>false</td><td>是否查询间接风险（默认值true）</td></tr><tr><td>business_tag</td><td>string</td><td>false</td><td><p>业务类型（</p><p>钱包：wallet</p><p>交易所：exchange</p><p>NFT：nft...</p><p>等等</p><p>）</p></td></tr><tr><td>kyt_status</td><td>int</td><td>false</td><td><p>to_address的KYC状态（</p><p>1：已KYC认证</p><p>2：未KYC认证</p><p>）</p></td></tr><tr><td>kyc_level</td><td>int</td><td>false</td><td><p>to_address的KYC等级（</p><p>1：KYC 1级</p><p>2：KYC 2级</p><p>3：KYC 3级</p><p>4：KYC 4级</p><p>）</p></td></tr></tbody></table>

## 4、返回参数 <a href="#id-4-fan-hui-can-shu" id="id-4-fan-hui-can-shu"></a>

```json
{
    "code": 200,
    "msg": "success",
    "data": { 
        "unique_id": "0140......8be5", //唯一标识id(用于查询历史数据)
        "risk_level": "severe", //风险等级（严重、高、中、低、未知）
        "risk_code": 4444 //风险code
        "risk_source": {
            "is_private_whitelist": false, //是否命中私有白名单  
            "is_private_blacklist": false, //是否命中私有黑名单  
            "risk_from_address_list":[ //风险转出地址
                { 
                    "black_address": "3E5L......44Bc",//交易的from地址
                    "black_address_type": "Blackmail Scam", //黑名单地址类型
                    "black_address_label": [ //黑名单地址标签
                        "attacker",
                        "hacker"
                    ],
                },
                ......
            ],
            "risk_to_address_list":[ //风险转入地址
                { 
                    "black_address": "35AT......yzew",//交易的to地址       
                    "black_address_type": "Blackmail Scam", //黑名单地址类型
                    "black_address_label": [ //黑名单地址标签
                        "attacker",
                        "hacker"
                    ],
                },
                ......
            ],
            "direct_tx_from_risk_list":[ //交易发送方地址 的直接风险交易列表
                {
                    "black_address": "1KHw......aGbX", //黑名单
                    "tx_hash": "2bc3......b693",
                    "black_address_type": "Blackmail Scam", //风险类型
                    "black_address_label": [ //黑名单地址标签
                        "attacker",
                        "hacker"
                    ],
                }, 
                ......
            ],
            "direct_tx_to_risk_list":[ //交易接收方地址 的直接风险交易列表
                {
                    "black_address": "1KHw......aGbX", //黑名单
                    "tx_hash": "2bc3......b693",
                    "black_address_type": "Blackmail Scam", //风险类型
                    "black_address_label": [ //黑名单标签
                        "attacker",
                        "hacker"
                    ],
                }, 
                ......
            ],
            "from_indirect_risk_list":[ //交易发送发间接风险交易列表
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
            ],
            "to_indirect_risk_list":[ //交易接收方间接风险交易列表
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

<table data-header-hidden><thead><tr><th width="314"></th><th width="115"></th><th></th></tr></thead><tbody><tr><td><strong>参数名</strong></td><td><strong>数据类型</strong></td><td><strong>描述</strong></td></tr><tr><td>code</td><td>Int</td><td><p>200：请求成功</p><p>-2：不支持该主网</p></td></tr><tr><td>message</td><td>string</td><td>接口请求状态描述</td></tr><tr><td>unique_id</td><td>string</td><td>唯一id（标识当前请求，用于查询历史记录）</td></tr><tr><td>risk_level</td><td>string</td><td><p>风险等级（</p><p>severe：严重</p><p>high：高风险</p><p>medium：中风险</p><p>low：低风险</p><p>none：未知</p><p>）</p></td></tr><tr><td>risk_code</td><td>int</td><td><p>风险code（</p><p>0：未知</p><p>-1：未查询到</p><p>4444：命中黑名单</p><p><strong>其他code说明详见：《risk_code说明书》</strong></p><p>）</p></td></tr><tr><td>risk_source</td><td>jsonArray</td><td>风险来源</td></tr><tr><td>risk_source.risk_from_address_list</td><td>jsonArray</td><td>交易发送方地址中的黑名单列表</td></tr><tr><td>risk_source.risk_to_address_list</td><td>jsonArray</td><td>交易接收方地址中的黑名单列表</td></tr><tr><td>risk_source.direct_tx_from_risk_list</td><td>jsonArray</td><td>交易发送方地址的直接风险交易列表</td></tr><tr><td>risk_source.direct_tx_to_risk_list</td><td>jsonArray</td><td>交易接收方地址的直接风险交易列表</td></tr><tr><td>risk_source.from_indirect_risk_list</td><td>jsonArray</td><td>交易发送发地址的间接风险交易列表</td></tr><tr><td>risk_source.to_indirect_risk_list</td><td>jsonArray</td><td>交易接收发地址的间接风险交易列表</td></tr></tbody></table>

\
