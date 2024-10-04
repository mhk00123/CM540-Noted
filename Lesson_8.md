# Lesson 8 - pip、API、爬蟲入門

**tags: `python`** **`CM-540`** **`Lesson8`**

Module、pip、API、爬蟲入門

## Slide
課件：[https://docs.google.com/presentation/d/1Cq-7TjksWri1E_UvoaNF1Vaz4W_xtlI1VOs3oVbB8Qg/edit?usp=sharing](https://docs.google.com/presentation/d/1Cq-7TjksWri1E_UvoaNF1Vaz4W_xtlI1VOs3oVbB8Qg/edit?usp=sharing)

# 功課
## 21 點遊戲增強(final)
- 嘗試重構程式
- 2人玩家 Dealer、Player (生成1個Class - 創建2實體p1,p2, 參數 )
- 每一步取牌後輸出當時時間 (*)
- 把整個遊戲過程輸出到txt中作記錄 (*)

## 取得簡單新聞
給定天氣API，取得目前天氣，並輸出。
嘗試尋找其他 API / 網站，看看使用相同方法能否成功取得你想要的資料

# 第三方Module下載 - pip
pip 是 Python 的包管理器，用於安裝和管理第三方庫（也稱為包）的工具。它使你能夠輕松地下載、安裝、升級和卸載 Python 包。

pip 是 Python 2.7.9 版本及其後續版本的標准組件，也是 Python 3.4 及其後續版本的標准組件。它在安裝 Python 解釋器時一同安裝。

## Python pip 基本命令
安裝包：
`pip install package_name`

升級包：
`pip install --upgrade package_name`

卸載包：
`pip uninstall package_name`

顯示已安裝的包：
`pip list`

搜索包：
`pip search package_name`

## pypi.org
[https://pypi.org/](https://pypi.org/)

在Python中，有一個官方儲存第三方 module / package 的網站基本上若我們使用 pip安裝的第三方 module 都會優先搜索此網站。
![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202404051611421.png)

## 取得網絡資料所用到的第三方 package
- requests
- BeautifulSoup
- pandas
- numpy
- Matplotlib
- xmltodict

### 請使用cmd命令全部安裝
```bash
pip install requests

pip install BeautifulSoup4

pip install pandas

pip install numpy

pip install Matplotlib

pip install xmltodict
```

# 進入爬蟲世界 - 認識網頁
在現階段我們在使用電腦的時候，我們經常會瀏覽網頁。
今天我們將向大家介紹由我們發出請求開始，網頁最後是如何呈現在我們面前的。

## 網頁如何呈現到你的電腦
當我們在瀏覽器中輸入一個網址後回車，後台會發生什麼？
比如說你輸入 http://google.com/ 你就會看到Google的首頁。
簡單來說這段過程發生了以下四個步驟：
1. 查找域名對應的IP地址(DNS)
2. 向IP對應的服務器(Server)發送請求(Request)
3. 服務器響應請求，發回網頁內容(Response)
4. 瀏覽器解析網頁內容

## HTTP協定
「HyperText Transfer Protocol(HTTP) 是⼀種⽤戶端瀏覽器和伺服端伺服器之間溝通的標準協定，規範了「客⼾端」與「伺服器端」兩者間如何傳輸資料。」
簡單來說就是：使⽤者端發送一個「Request 請求」，伺服器端根據請求回傳⼀個「Response 回覆」

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202404051613930.png)

## Response 回覆
Response 由目標伺服器在接收到Request後發出。
一般回覆會夾帶著Response代碼。其中狀態呈現綠色 200，我們就可以知道這個請求是「成功」的，可以從 response body 找到我們要請求的資料，另外一般常見的狀態碼有：

1. 200 成功回應
2. 4xx 用戶端錯誤回應 (Ex : 404)
3. 5xx 伺服器端錯誤

## 認識HTML
HTML（HyperText Markup Language，超文本標記語言）是打造網頁的基石。它表述並定義網頁的內容。伴隨 HTML 而來的技術還有描述網頁外觀（CSS）及功能性的程式語言（JavaScript）。
HTML 使用「標記」（markup）來詮釋文字、圖像、或是其他能在瀏覽器裡面顯示的內容。HTML 標記還包括一些特殊「元素」（element），例如：`<head>`、`<title>`、`<body>`、`<header>`、`<footer>`、`<article>`、`<section>`、`<p>`、`<div>`、`<span>`、`<img>`……等等。

### 一個基礎的HTML
一個基礎的HTML網頁需要包含以下幾個tag
- html
- head
- body

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <title>Document_name</title>
</head>
<body>
   
</body>
</html>
```

## HTTP headers
在HTTP協議中，headers對於每個request，response提供了一些額外的資訊，基本上他們就是只是一對(key, value) pair，由冒號(:)隔開。用作給伺服器和用戶認證的資訊。

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202404051618119.png)

## API
API 的全名叫應⽤程式介面（Application Programming Interface），表⽰程式與程式間的溝通⽅式或介面。換句句話說，就是資料⽅寫好⼀組程式，提供你可以用程式的⽅式與其串接資料。直接由伺服器回覆的資料已經經是整理好的json格式、或是其他不包含HTML、JavaScript代碼的資料。
常用收到格式：
- json
- xml
- csv
- xlsx

## 如何尋找API
並非所有網站都希望提供資料給別人下載，因此不是所有網站都會提供API給大家。而在本澳則有 1 開放資料平台，供大家使用：澳門特別行政區政府數據開放平台：

[https://data.gov.mo/](https://data.gov.mo/)

如何使用 Python 取得這些東西
- 透過 requests 向目標 API 發送請求
- 透過不同module處理response資料
- 整理
- 輸出有效數據

## 由 smg.gov 公開數據平台取得當前天氣

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

print(data_dict)

# 5. 取得Response中的"溫度"欄位
g_temperature = data_dict["ActualWeatherBrief"]["Custom"]["Temperature"]["Value"]

# 6. 取得目前時間
timestamp = time.time()
struct_time_local = time.localtime(timestamp)
format_time = time.strftime("%Y-%m-%d %I:%M", struct_time_local)

print(f"現在是 {format_time}，溫度是：{g_temperature}度")
```
