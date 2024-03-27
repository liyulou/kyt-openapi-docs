# KYT OPEN-API开发者文档

## **API 域名** <a href="#api-yu-ming" id="api-yu-ming"></a>

​https://openapi.trustformer.info

## 接口鉴权 <a href="#jie-kou-jian-quan" id="jie-kou-jian-quan"></a>

KYT运营会提供给客户apikey和secret。在请求接口时，为了保障安全性，除了传递apikey，还需要按规定的算法进行加密签名。并在header中传递时间戳timestamp和签名sign参数。

### header参数

<table data-header-hidden><thead><tr><th width="143"></th><th width="111"></th><th width="114"></th><th></th></tr></thead><tbody><tr><td><strong>参数名</strong></td><td><strong>数据类型</strong></td><td><strong>是否必传</strong></td><td><strong>描述</strong></td></tr><tr><td>timestamp</td><td>int</td><td>true</td><td>时间戳（单位s）</td></tr><tr><td>sign</td><td>string</td><td>true</td><td><p><strong>签名计算方式：</strong>sha256("timestamp=timestamp的值&#x26;secret=secret的值")</p><p><strong>在线加密工具：</strong>https://crypot.51strive.com/sha256.html</p><p></p><p><strong>示例：</strong></p><p>加密前： timestamp=1677148682&#x26;secret=9e3df800bbcbb1b8fc97bf78ed95a95a92aa3a155d270f1e48eb330c2d435321</p><p>加密后： 110a20dcbe1fef5456051a8887c8d1aeba637bbc624e606697fb82a7e7ded604</p></td></tr></tbody></table>

