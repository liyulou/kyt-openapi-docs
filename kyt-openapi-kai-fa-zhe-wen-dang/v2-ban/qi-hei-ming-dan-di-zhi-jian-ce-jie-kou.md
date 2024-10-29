# 七、黑名单地址检测接口

说明：检测地址是否是黑名单。支持全部EVM主链。

## 1、接口URL

GET /openapi/v2/risk/address/blacklist

## 2、header参数

<table data-header-hidden><thead><tr><th width="143"></th><th width="125"></th><th width="122"></th><th></th></tr></thead><tbody><tr><td><strong>参数名</strong></td><td><strong>数据类型</strong></td><td><strong>是否必传</strong></td><td><strong>描述</strong></td></tr><tr><td>timestamp</td><td>int</td><td>true</td><td>时间戳（单位s）</td></tr><tr><td>sign<br></td><td>string<br></td><td>true<br></td><td>签名sha256("timestamp=timestamp的值&#x26;secret=secretkey的值")</td></tr></tbody></table>

## 3、请求参数

<table data-header-hidden><thead><tr><th width="141"></th><th width="126"></th><th width="128"></th><th></th></tr></thead><tbody><tr><td><strong>参数名</strong></td><td><strong>数据类型</strong></td><td><strong>是否必传</strong></td><td><strong>描述</strong></td></tr><tr><td>api_key</td><td>string</td><td>true</td><td>apikey</td></tr><tr><td>address</td><td>string</td><td>true</td><td>钱包地址</td></tr></tbody></table>

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
            ]
        }
    }
}
```

<table data-header-hidden><thead><tr><th width="285"></th><th width="152"></th><th></th></tr></thead><tbody><tr><td><strong>参数名</strong></td><td><strong>数据类型</strong></td><td><strong>描述</strong></td></tr><tr><td>code</td><td>Int<br></td><td>200：请求成功-2：不支持该主网</td></tr><tr><td>message</td><td>string</td><td>接口请求状态描述</td></tr><tr><td>unique_id</td><td>string</td><td>唯一id（标识当前请求，用于查询历史记录）</td></tr><tr><td>risk_level<br></td><td>string<br></td><td>风险等级（severe：严重high：高风险medium：中风险low：低风险none：未知）</td></tr><tr><td>risk_code<br></td><td>int<br></td><td>风险code（0：未知-1：未查询到4444：命中黑名单<strong>其他code说明详见：《risk_code说明书》</strong>）</td></tr><tr><td>risk_source</td><td>json</td><td>风险来源</td></tr><tr><td>risk_source.is_private_whitelist</td><td>boolean</td><td>是否命中私有白名单</td></tr><tr><td>risk_source.is_private_blacklist</td><td>boolean</td><td>是否命中私有黑名单</td></tr><tr><td>risk_source.black_address_type</td><td>string</td><td>地址的黑名单类型</td></tr><tr><td>risk_source.black_address_label</td><td>stringArray</td><td>地址的黑名单标签</td></tr></tbody></table>

