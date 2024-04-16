# Lesson 9 - API、爬蟲

**tags: `python`** **`CM-540`** **`Lesson9`**

## Slide
課件：[https://tinyurl.com/atnuxps7](https://tinyurl.com/atnuxps7)

## 作業5
1. 完成 21 點遊戲 Final
2. 取得簡單天氣，給定天氣API，取得目前天氣，並輸出。

天氣API : [https://xml.smg.gov.mo/c_actual_brief.xml](https://xml.smg.gov.mo/c_actual_brief.xml)

繳交：[https://tinyurl.com/5du9az6t](https://tinyurl.com/5du9az6t)


## 作業6 - Final Project
自己思考一個題目，任何類型
- 小算盤?
- 待辦行事記錄?
- 資料分析? 停車場車位一些應用?
- 自動檢查退休基金價格?
- 檢查政府工什麼時候開考?

## (補充)Pass by value and pass by reference
傳值(Value)、還是傳址(Address)的問題。

## 傳址(by reference)
在Python中，任何儲存容器的資料類型，在進行參數傳遞時為傳址(Address)即 function 中的修改，會直接改變原資料。

## 傳值(by value)
而其他int、float等為傳值(Value)，只是把值放到參數中，function 不能改變原資料。

## 示意圖

![Img](https://www.mathwarehouse.com/programming/images/pass-by-reference-vs-pass-by-value-animation.gif)

```python
def test_value_ref(a, b):
    a = a.append(4)
    b = b + 1

a_list = [1,2,3]
b_int = 1

print("執行function前")
print(a_list)
print(b_int)
print("--------")

test_value_ref(a_list, b_int)

print("執行function後")
print(a_list)
print(b_int)
print("--------")
```

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202404161653002.png)


# 爬取資料的思路
1. 取得資料(**下載、API**)
2. 判斷回傳資料的格式(**json、xml、xlsx、csv**)
3. 用對應的Module、Package把資料格式通通轉為**dict / list**
4. 透過 for 迴圈讀取所有相關數據
5. 透過不同判斷、拿出需要的資料


# html、xml、json
- HTML: 主要用於「創建和呈現」網頁。
- xml、json：是傳輸和儲存數據，以及在不同的系統或網站之間共享數據。 它提供了一種通用的標記語言，可用於創建「自定義」的標籤和結構，用於描述各種類型的數據資料。

## HTML
超文本標記語言、HTML 使用「標記」（markup）來詮釋文字、圖像、或是其他能在瀏覽器裡面顯示的內容。
html以一對「標記」的方式去分不同的元素。
例如：
```html
<body> 內容 </body>
```

而在一對標記中，又可以再包含另外幾組不同的標記
```html
<body>
   <p>你好</p>
   <p>這里是CM540</p>
</body>
```

## HTML架構
```html
<html>
	<header>頭部內容</header>

    <body>
        <p>你好</p>
        <p>這里是CM540</p>
    </body>

    <footer>尾部內容</footer>
</html>
```
![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202404161656929.png)

## 取得HTML元素的重點
Python中無法直接讀取 html 結構資料，因此需進行轉換。

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202404161658745.png)

如我想取得` <p></p>`中的`你好`

剛我們把html結構轉為`dict`結構、以`data`作變數名儲存
```python
data["html"]["body"]["p"]
```

假如是一個另一種套件(可能)
```python
data.html.body.p
```

## XML
與HTML相同，XML也採用標記方式記錄資料格式，而不同的是XML主要用於存放數據。

```xml
<data>
	<Weather>
	<Temperature>
		Value：25
		Unit：°C
	</Temperature>
	</Weather>
</data>
```

## Json / XML  Parser
實際上，Json檔案一般為程式查看，所以資料呈現上是不友好的。但我們可以透過一些簡單的工具為我們美化這些 json / XML 資料。
- json Parser : http://json.parser.online.fr/
- Python Dictionary：https://codebeautify.org/python-formatter-beautifier

# 取得XML元素
在Python中無法直接讀取XML結構，我們透過xmltodict把xml轉換為dict格式。

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202404161701378.png)

如我想取得目前的溫度
把資料轉換至一個`dict`、以`data`作變數名儲存
```Python
data["Weather"]["Temperature"]["value"]
```

## 練習
### 由 smg.gov 公開數據平台取得當前天氣
1. 使用 requests 向 smg.gov API 取得資料
2. 判斷回傳資料的格式：xml
3. 用對應的Module（xmltodict）把資料格式通通轉為dict
4. 透過 for 迴圈讀取所有相關數據
5. 透過不同判斷、拿出需要的資料

```python
import requests
import xmltodict
import time 

# 1. 目標 url
url = "https://xml.smg.gov.mo/c_actual_brief.xml"

# 2. 向目標發送請求(request)
response = requests.get(url)

# 3. 接收回覆(Response)
xml_data = response.content.decode("utf-8")

# 4. 回覆的格式為.xml
#    我們使用 xmltodict 套件處理
data_dict = xmltodict.parse(xml_data)

# 5. 取得Response中的"溫度"欄位
g_temperature = data_dict["ActualWeatherBrief"]["Custom"]["Temperature"][0]["Value"]

# 6. 取得目前時間
timestamp = time.time()
struct_time_local = time.localtime(timestamp)
format_time = time.strftime("%Y-%m-%d %I:%M", struct_time_local)

print(f"現在是 {format_time}，溫度是：{g_temperature}度")
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

## Python中讀取json
Python 自帶讀取json格式的module：`json`
```python
import json

file = open('test.json', encoding='utf-8')

data = json.load(file)
```

# 堂上練習
香港城巴站點資訊API:

https://rt.data.gov.hk/v2/transport/citybus/route/ctb

找出所有終點站為 ”堅尼地城” 的巴士路線

## laod json 功能
```python
import os
import json

def load_json(json_data_list, file_path):
    file = open(file_path, encoding='utf-8')
    json_data = json.load(file)
    json_data_list.append(json_data)
    
folder_path = '此處請換成您的path'
file_list = os.listdir(folder_path)

json_files = []
json_files_list = []

print(file_list)

for file_name in file_list:
    file_path = os.path.join(folder_path, file_name)
    
    # 檢查副檔名為 .json
    if os.path.isfile(file_path) and file_name.endswith('.json'):
        json_files.append(file_path)

for file_address in json_files:
    load_json(json_files_list, file_address)
    
print(json_files_list)
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
