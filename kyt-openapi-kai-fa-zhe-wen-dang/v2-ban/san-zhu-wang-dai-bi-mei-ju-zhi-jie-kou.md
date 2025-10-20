# 三、主网代币枚举值接口

说明：获取openapi接口支持的主网和代币名称。

## 1、接口URL <a href="#id-1-jie-kou-url" id="id-1-jie-kou-url"></a>

GET /openapi/v2/data/enum

## 2、header参数 <a href="#id-2header-can-shu" id="id-2header-can-shu"></a>

<table data-header-hidden><thead><tr><th width="182"></th><th width="99"></th><th width="106"></th><th></th></tr></thead><tbody><tr><td><strong>参数名</strong></td><td><strong>数据类型</strong></td><td><strong>是否必传</strong></td><td><strong>描述</strong></td></tr><tr><td>timestamp</td><td>int</td><td>true</td><td>时间戳（单位s）</td></tr><tr><td>sign</td><td>string</td><td>true</td><td>签名sha256("timestamp=timestamp的值&#x26;secret=secretkey的值")</td></tr></tbody></table>

## 3、请求参数 <a href="#id-3-qing-qiu-can-shu" id="id-3-qing-qiu-can-shu"></a>

<table data-header-hidden><thead><tr><th width="181"></th><th width="101"></th><th width="105"></th><th></th></tr></thead><tbody><tr><td><strong>参数名</strong></td><td><strong>数据类型</strong></td><td><strong>是否必传</strong></td><td><strong>描述</strong></td></tr><tr><td>api_key</td><td>string</td><td>true</td><td>apikey</td></tr></tbody></table>

## 4、返回参数 <a href="#id-4-fan-hui-can-shu" id="id-4-fan-hui-can-shu"></a>

```json
{
    "code": 200,
    "msg": "success",
    "data": { 
        "network_coin_list": [
            {
                "coin_list": [ //支持的代币列表
                    "BTC"
                ],
                "network": "Bitcoin" //主网名称
            },
            {
                "coin_list": [
                    "ETH",
                    "USDT",
                    "USDC"
                ],
                "network": "Ethereum"
            },
            {
                "coin_list": [
                    "TRX",
                    "USDT"
                ],
                "network": "TRON"
            },
            {
                "coin_list": [
                    "BNB",
                    "USDT",
                    "USDC"
                ],
                "network": "BNB"
            },
            {
                "coin_list": [
                    "POL",
                    "USDT",
                    "USDC"
                ],
                "network": "POLYGON"
            },
            {
                "coin_list": [
                    "LTC"
                ],
                "network": "Litecoin"
            },
            {
                "coin_list": [
                    "DOGE"
                ],
                "network": "Dogecoin"
            }
        ]
    }
}
```
