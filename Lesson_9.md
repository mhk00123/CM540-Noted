# Lesson 9 - API、爬蟲

**tags: `python`** **`CM-540`** **`Lesson9`**

## Slide
課件：[https://docs.google.com/presentation/d/1KNGlC-_waAO3HGziN4mOu7OJjdbq8Bt8_ZQ6kA37GTA/edit?usp=sharing](https://docs.google.com/presentation/d/1KNGlC-_waAO3HGziN4mOu7OJjdbq8Bt8_ZQ6kA37GTA/edit?usp=sharing)

## 作業 - Final Project
自己思考一個題目，任何類型
- 小算盤?
- 待辦行事記錄?
- 資料分析? 停車場車位一些應用?
- 自動檢查退休基金價格?
- 檢查政府工什麼時候開考?

# 爬取資料的思路
1. 取得資料(**下載、API**)
2. 判斷回傳資料的格式(**json、xml、xlsx、csv**)
3. 用對應的Module、Package把資料格式通通轉為**dict / list**
4. 透過 for 迴圈讀取所有相關數據
5. 透過不同判斷、拿出需要的資料


# html、xml、json
- HTML: 主要用於「創建和呈現」網頁。
- xml、json：是傳輸和儲存數據，以及在不同的系統或網站之間共享數據。 它提供了一種通用的標記語言，可用於創建「自定義」的標籤和結構，用於描述各種類型的數據資料。


## Json / XML  Parser
實際上，Json檔案一般為程式查看，所以資料呈現上是不友好的。但我們可以透過一些簡單的工具為我們美化這些 json / XML 資料。
- Python Dictionary : http://json.parser.online.fr/
- json Parser：https://codebeautify.org/python-formatter-beautifier

## 需要認證的 API
目前我們所遇到的API，一般都是可以直接發送 request 得到 response。因為這些 API 都沒有經過加密，因此我們才可以輕易取得資料。

而實際上，有更多的API是需要透過認證才可以取得資料的。這組 key : value 正是驗證所需要的資料，我們需要在發送 requests 時附帶這組參數在 header(表頭) 中


### 交通事務局 API 
APP Link : [https://data.gov.mo/Detail?id=ea50a770-cc35-47cc-a3ba-7f60092d4bc4](https://data.gov.mo/Detail?id=ea50a770-cc35-47cc-a3ba-7f60092d4bc4)

API Link : `https://dsat.apigateway.data.gov.mo/car_park_maintance`

調用 API 參數，這組 key : value 正是驗證所需要的資料，我們需要在發送 requests 時附帶這組參數在 header(表頭) 中
```
'Authorization'：'APPCODE 09d43a591fba407fb862412970667de4'
```

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202406032218011.png)

## Postman - 用作測試 API 的工具
Postman 為一個測試 API request、response的工具，可以網站、API、伺服器等發送 requests 並附帶各種參數。

[https://www.postman.com/](https://www.postman.com/)

使用 Google 即可登入使用 web 版，或可以下載使用。

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202406032226936.png)

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202406032226661.png)

## Requests 中加入 header

透過 payload 變數加入所需的認證參數，以 dict 型式記錄
在 requests 的參數中加入 headers

```python
import requests

url = "https://dsat.apigateway.data.gov.mo/car_park_maintance"

payload = {
    "Authorization": "APPCODE 09d43a591fba407fb862412970667de4"
}

response = requests.get(url, headers = payload)
```

## 取得交通事務局中的資料
```python
import requests
import xmltodict
import json
 
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
print(target_data)

# 7. 輸出到 txt 方便放到 pareser中
with open("data.txt", "w", encoding="utf-8") as myfile:
    write_data = json.dumps(data_dict, ensure_ascii=False)
    myfile.write(write_data)
```

## 練習：尋找目前澳門沒有電單車車位的停車場
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

## json
json 檔案一開始於用 javascript 中，是一種輕量級的資料交換格式。它的使用範圍很廣，並成為ECMA 標準，可以使用在多種程式語言中，用於前後端之間的資料傳輸、儲存和交換資料。可以說是“用更少的編碼，有更快的處理速度”，所以深受廣大程式設計師的喜愛。

json 格式以 `{ }` 作為開始，如有新一層也是以`{ }`分開並加上 `,`，結束和python的dict相似。

```json
{
    "person information" : {
        "name": "Leo Tam",
        "age": 27,
        "city": "Macau"
    },
    
    "company information" : {
        "name": "CPTTM",
        "title": "Teacher"
    }
}
```

## Python中讀取json、輸出json

Python 自帶讀取json格式的module：`json`

- 讀取 (loads)、轉換成 `json` 格式
- 輸出 (dumps)、由 `json` 轉換為 `string`
```python
import json

file = open('test.json', encoding='utf-8')

data = json.loads(file)

dump_data = json.dumps(data)

with open("data.txt", "w",encoding="utf-8") as my_file:
    # json中含有utf-8的操作
    write_data = json.dumps(dump_data, ensure_ascii=False)
    my_file.write(write_data)
```

## 民航局-澳門國際機場航班時間表 API 
[https://data.gov.mo/Detail?id=ea50a770-cc35-47cc-a3ba-7f60092d4bc4](https://data.gov.mo/Detail?id=ea50a770-cc35-47cc-a3ba-7f60092d4bc4)

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202406032302183.png)


# 練習 - 尋找所有目的地為北京的航班
```python
import requests
import xmltodict
import json

# 1. 目標 url
url = "https://aacm.apigateway.data.gov.mo/api/open/listFlightTimetable"

# 2. Header
headers = {
    "Authorization": "APPCODE 09d43a591fba407fb862412970667de4"
}

# 3. 向目標發送請求(request)
response = requests.get(url, headers=headers)

print(response)

# 4. 讀取 response 並進行 utf-8 decode
# 使用 loads
json_data = json.loads(response.content)

# 5. 尋找目的地為北京的 Beijing 的所有航空
for i in json_data:
    if("Beijin" in i['destination']):
        print(f"{i['airline']} - {i['weekDay']}，航行周期：{i['periodStartDate']} 至 {i['periodEndDate']}")
```


## (補充)如何透過 Python 程式向手機發送通知
首先，要向自己的手機發送信息是十分困難的!

由於手機系統中有著非常多的認證機制，以現階段我們的知識未具備以撰寫可通過驗證的程式。

因此我們需要透過第三方工具協助，目前適用於Telegram、微信。
- Telegram：開放API，可直接透過Telegram官方API向指定的群組發送推送。
```python
import requests

def telegram_bot_sendtext(bot_message):

    bot_token = 'your_token'
    bot_chatID = 'your_chatID'
    send_text = 'https://api.telegram.org/bot' + bot_token + '/sendMessage?chat_id=' + bot_chatID + '&parse_mode=Markdown&text=' + bot_message

    response = requests.get(send_text)

    return response.json()
```

- 微信：透過第三應用 pushplus 向特定微信帳戶 (pushplus) 發送`post`推送。
```python
def wechat_bot_sendtext(bot_message):

    payload = {
            'token' : 'your_token',
            'content': bot_message
        }
    rs = requests.post('http://www.pushplus.plus/send', data=payload)
    
    return rs
```
