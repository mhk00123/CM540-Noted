# Lesson 10 - 停車場API、Pandas

**tags: `python`** **`CM-540`** **`Lesson10`**

## Slide
課件：[https://tinyurl.com/bdd9s85t](https://tinyurl.com/bdd9s85t)

# 需驗證的 API
目前我們所遇到的API，一般都是可以直接發送 request 得到 response。因為這些 API 都沒有經過加密，因此我們才可以輕易取得資料。

而實際上，有更多的API是需要透過認證才可以取得資料的。

### 交通事務局 API 

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202404191649488.png)


API Link : [https://dsat.apigateway.data.gov.mo/car_park_maintance](https://dsat.apigateway.data.gov.mo/car_park_maintance)

調用 API 參數：
```
Authorization：APPCODE 09d43a591fba407fb862412970667de4
```
這組 `key` : `value` 正是驗證所需要的資料，我們需要在發送 requests 時附帶這組參數在 header (表頭)中。

## Postman - 測試 API 工具
Postman 為一個測試 API request、response的工具，可以網站、API、伺服器等發送 requests 並附帶各種參數。

Postman : [https://www.postman.com/](https://www.postman.com/)

Postman可以在發送的 requests 中加入需要 header:

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202404191651300.png)

加入 header 後，API通過驗證後便會回傳 response：

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202404191651237.png)

## 在 Requests 中加入 Header
在 Python 的 Requests 套件中，我們可以透過以下方式插入 header: 

透過 payload 變數加入所需的認證參數，以 dict 型式記錄

```python
import requests

url = "https://dsat.apigateway.data.gov.mo/car_park_maintance"

payload = {
    "Authorization": "APPCODE 09d43a591fba407fb862412970667de4"
}

response = requests.get(url, headers = payload)
```

## 交通局 API Response
讀取交通局 Response，注意交通事務局API中resopone回覆為`XML`格式

```python
import requests
import xmltodict

# 1. 目標 url
url = "https://dsat.apigateway.data.gov.mo/car_park_maintance"

# 2. Header
headers = {
    "Authorization": "APPCODE 09d43a591fba407fb862412970667de4"
}

# 3. 向目標發送請求(request)
response = requests.get(url, headers=headers)

# 4. 讀取 response 並進行 utf-8 decode
xml_data = response.content.decode("utf-8")

# 5. 透過 xmltodict 把 xml 轉換為 dict
data_dict = xmltodict.parse(xml_data)

# 6. 尋找 target 標籤
target_data = data_dict['CarPark']['Car_park_info']

for i in target_data:
    print(i)

# 7. 輸出到txt
with open("data.txt", "w", encoding="utf-8") as myfile:
    for key, value in data_dict.items():
        line = f'{key}: {value}\n'
        myfile.write(line)
```

## 練習 - 尋找目前澳門沒有電單車車位的停車場
```python
import requests
import xmltodict

# 1. 目標 url
url = "https://dsat.apigateway.data.gov.mo/car_park_maintance"

# 2. Header
headers = {
    "Authorization": "APPCODE 09d43a591fba407fb862412970667de4"
}

# 3. 向目標發送請求(request)
response = requests.get(url, headers=headers)

# 4. 讀取 response 並進行 utf-8 decode
xml_data = response.content.decode("utf-8")

# 5. 透過 xmltodict 把 xml 轉換為 dict
data_dict = xmltodict.parse(xml_data)

# 6. 尋找 target 標籤
target_data = data_dict['CarPark']['Car_park_info']

for i in target_data:
    if(i["@MB_CNT"] == "" or i["@MB_CNT"] == "0"):
        print(f'{i["@name"]} - 沒有電單車停車場')
```
