# 六、Risk\_Code说明书

单一code分为：命中黑名单、间接风险交易、未知、未查询到等等；

**其他复杂code是由“分类+交易方向+交易曝光类型+风险等级”按顺序拼接而成**

#### 1、单一code <a href="#id-1-ming-zhong-hei-ming-dan-he-wei-zhi-code" id="id-1-ming-zhong-hei-ming-dan-he-wei-zhi-code"></a>

| **code** | **名称**     | **name**                       |
| -------- | ---------- | ------------------------------ |
| 4444     | 命中黑名单      | Black Address                  |
| 0        | 未知         | none                           |
| -1       | 未查询到       | not found                      |
| -2       | 不支持该主网或该代币 | network or coin is not support |
| 1        | 命中私有白名单    | Private White Address          |
| 444      | 命中私有黑名单    | Private Blacklist Address      |
| 4400     | 直接风险       | Direct Risk                    |
| 4401     | 间接1层风险     | Indirect Risk Level 1          |
| 4402     | 间接2层风险     | Indirect Risk Level 2          |
| 4403     | 间接3层风险     | Indirect Risk Level 3          |
| 4404     | 间接4层风险     | Indirect Risk Level 4          |
| 4405     | 间接5层风险     | Indirect Risk Level 5          |
| 4406     | 间接6层风险     | Indirect Risk Level 6          |

#### 2、交易方向code <a href="#id-2-jiao-yi-fang-xiang-code" id="id-2-jiao-yi-fang-xiang-code"></a>

| **code** | **名称** | **name**  |
| -------- | ------ | --------- |
| 21       | 转出     | sending   |
| 22       | 转入     | receiving |

#### 3、交易曝光类型code <a href="#id-3-jiao-yi-pu-guang-lei-xing-code" id="id-3-jiao-yi-pu-guang-lei-xing-code"></a>

| **code** | **名称** | **name** |
| -------- | ------ | -------- |
| 11       | 直接     | direct   |
| 12       | 间接     | indirect |

#### 4、风险等级code <a href="#id-4-feng-xian-deng-ji-code" id="id-4-feng-xian-deng-ji-code"></a>

| **code** | **名称** | **name** |
| -------- | ------ | -------- |
| 45       | 极高风险   | severe   |
| 44       | 高风险    | high     |
| 43       | 中风险    | medium   |
| 42       | 低风险    | low      |
| 41       | 未知     | none     |

#### 5、黑名单分类code <a href="#id-5-hei-ming-dan-fen-lei-code" id="id-5-hei-ming-dan-fen-lei-code"></a>

<table data-header-hidden><thead><tr><th width="141"></th><th width="206"></th><th></th></tr></thead><tbody><tr><td><strong>code</strong></td><td>名称</td><td><strong>Name</strong></td></tr><tr><td>3000</td><td>所有类别</td><td>All Categories</td></tr><tr><td>3001</td><td>去中心化交易所</td><td>Decentralized Exchange</td></tr><tr><td>3002</td><td>中心化交易所</td><td>Centralized Exchange</td></tr><tr><td>3003</td><td>托管钱包</td><td>Custody Wallet</td></tr><tr><td>3004</td><td>商业和支付服务</td><td>Merchant Service</td></tr><tr><td>3005</td><td>ATM取款或转账</td><td>ATM</td></tr><tr><td>3006</td><td>挖矿</td><td>Mining</td></tr><tr><td>3007</td><td>其他智能合约</td><td>Other Smart Contract</td></tr><tr><td>3008</td><td>基础设施服务</td><td>Infrastructure as a Service</td></tr><tr><td>3009</td><td>Token智能合约</td><td>Token Smart Contract</td></tr><tr><td>3010</td><td>高风险交易所</td><td>High Risk Exchange</td></tr><tr><td>3011</td><td>高风险辖区</td><td>High Risk Jurisdiction</td></tr><tr><td>3012</td><td>贷款合约</td><td>Lending Contract</td></tr><tr><td>3013</td><td>矿池</td><td>Mining Pool</td></tr><tr><td>3014</td><td>ICO</td><td>ICO</td></tr><tr><td>3015</td><td>欺诈骗局</td><td>Blackmail Scam</td></tr><tr><td>3016</td><td>混币服务</td><td>Tumbler Mixer</td></tr><tr><td>3017</td><td>性勒索</td><td>Sextortion</td></tr><tr><td>3018</td><td>暗网</td><td>Darknet Market</td></tr><tr><td>3019</td><td>虐待儿童</td><td>Child Exploitation</td></tr><tr><td>3020</td><td>虚假慈善</td><td>Fake Charity</td></tr><tr><td>3021</td><td>虚假交易所</td><td>Fake Exchange</td></tr><tr><td>3022</td><td>虚假有奖参与</td><td>Fake Giveaway</td></tr><tr><td>3023</td><td>虚假代币</td><td>Fake Token</td></tr><tr><td>3024</td><td>虚假矿工</td><td>Fake Miner</td></tr><tr><td>3025</td><td>虚假投资</td><td>Fake Investment</td></tr><tr><td>3026</td><td>仿造钱包地址</td><td>Fake Wallet Address</td></tr><tr><td>3027</td><td>庞氏骗局</td><td>Ponzi Scheme</td></tr><tr><td>3028</td><td>贩卖人口和器官</td><td>Trafficking in Human Beings and Organs</td></tr><tr><td>3029</td><td>虚假购物</td><td>Fake Shop</td></tr><tr><td>3030</td><td>博彩或赌博</td><td>Betting or Gambling</td></tr><tr><td>3031</td><td>非法交易和分销</td><td>Illegal Sale and Distribution</td></tr><tr><td>3032</td><td>非法组织</td><td>Illegal Org</td></tr><tr><td>3033</td><td>协议隐私</td><td>Protocol Privacy</td></tr><tr><td>3034</td><td>勒索敲诈</td><td>Ransomware/Virus</td></tr><tr><td>3035</td><td>制裁</td><td>Sanctions</td></tr><tr><td>3036</td><td>盗窃</td><td>Stolen Crypto</td></tr><tr><td>3037</td><td>恐怖主义</td><td>Terrorist Financing</td></tr><tr><td>3038</td><td>美国政治黑名单</td><td>USA Political Blacklist</td></tr><tr><td>3039</td><td>以太坊合约添加黑名单</td><td>Etherscan_AddedBlackList</td></tr><tr><td>3040</td><td>公链合约黑名单</td><td>Mainnet_AddedBlackList</td></tr><tr><td>3041</td><td>数字货币关联卡</td><td>Cryptoassets-related Cards</td></tr><tr><td>3042</td><td>DeFi智能合约</td><td>DeFi Smart Contract</td></tr><tr><td>3043</td><td>NFT智能合约</td><td>NFT Smart Contract</td></tr></tbody></table>
