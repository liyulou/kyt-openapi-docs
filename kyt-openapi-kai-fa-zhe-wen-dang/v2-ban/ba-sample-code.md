# 八、Sample Code

接口调用示例代码

#### 1、调用V2版地址风险检测接口 <a href="#id-1-tiao-yong-v2-ban-di-zhi-feng-xian-jian-ce-jie-kou" id="id-1-tiao-yong-v2-ban-di-zhi-feng-xian-jian-ce-jie-kou"></a>

**Python版**

{% code overflow="wrap" %}
```python
import requests

url = "https://openapi.chaineyes.com/openapi/v2/risk/address/check?api_key=a0876......bb6f&network=Ethereum&address=0x53......a920b&coin=eth&app_id=6491......21qa&address_role=to"

payload = {}
headers = {
  'sign': '8a96......1911',
  'timestamp': '1697788140'
}

response = requests.request("GET", url, headers=headers, data=payload)

print(response.text)
```
{% endcode %}

**Golang版**

{% code overflow="wrap" %}
```go
package main

import (
  "fmt"
  "net/http"
  "io/ioutil"
)

func main() {

  url := "https://openapi.chaineyes.com/openapi/v2/risk/address/check?api_key=a0876......bb6f&network=Ethereum&address=0x53......a920b&coin=eth&app_id=6491......21qa&address_role=to"
  method := "GET"

  client := &http.Client {
  }
  req, err := http.NewRequest(method, url, nil)

  if err != nil {
    fmt.Println(err)
    return
  }
  req.Header.Add("sign", "8a96......1911")
  req.Header.Add("timestamp", "1697788140")

  res, err := client.Do(req)
  if err != nil {
    fmt.Println(err)
    return
  }
  defer res.Body.Close()

  body, err := ioutil.ReadAll(res.Body)
  if err != nil {
    fmt.Println(err)
    return
  }
  fmt.Println(string(body))
}
```
{% endcode %}

#### 2、调用V2版交易风险检测接口 <a href="#id-2-tiao-yong-v2-ban-jiao-yi-feng-xian-jian-ce-jie-kou" id="id-2-tiao-yong-v2-ban-jiao-yi-feng-xian-jian-ce-jie-kou"></a>

**Python版**

{% code overflow="wrap" %}
```python
import requests

url = "https://openapi.chaineyes.com/openapi/v2/risk/tx/check?api_key=a087......bb6f&tx=0x04......548df&network=ethereum&to_address=0x17......a10d&coin=usdt&app_id=1425......2w8d"

payload = {}
headers = {
  'sign': '8a96......1911',
  'timestamp': '1697788140'
}

response = requests.request("GET", url, headers=headers, data=payload)

print(response.text)
```
{% endcode %}

**Golang版**

{% code overflow="wrap" %}
```go
package main

import (
  "fmt"
  "net/http"
  "io/ioutil"
)

func main() {

  url := "https://openapi.chaineyes.com/openapi/v2/risk/tx/check?api_key=a087......bb6f&tx=0x04......548df&network=ethereum&to_address=0x17......a10d&coin=usdt&app_id=1425......2w8d"
  method := "GET"

  client := &http.Client {
  }
  req, err := http.NewRequest(method, url, nil)

  if err != nil {
    fmt.Println(err)
    return
  }
  req.Header.Add("sign", "8a96......1911")
  req.Header.Add("timestamp", "1697788140")

  res, err := client.Do(req)
  if err != nil {
    fmt.Println(err)
    return
  }
  defer res.Body.Close()

  body, err := ioutil.ReadAll(res.Body)
  if err != nil {
    fmt.Println(err)
    return
  }
  fmt.Println(string(body))
}
```
{% endcode %}
