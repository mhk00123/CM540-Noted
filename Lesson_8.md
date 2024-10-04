# Lesson 8 - pip、API、爬蟲入門

**tags: `python`** **`CM-540`** **`Lesson8`**

Datetime Module、pip、API、爬蟲入門

## Slide
課件：[https://docs.google.com/presentation/d/1Cq-7TjksWri1E_UvoaNF1Vaz4W_xtlI1VOs3oVbB8Qg/edit?usp=sharing](https://docs.google.com/presentation/d/1Cq-7TjksWri1E_UvoaNF1Vaz4W_xtlI1VOs3oVbB8Qg/edit?usp=sharing)

## 功課：21 點遊戲增強(final)
繳交日期：2024-10-15 23:59
繳交地址：[https://hamster.cpttm.org.mo/spaces/E_xEKq9Ywg6IK4Du4BlV3g/upload](https://hamster.cpttm.org.mo/spaces/E_xEKq9Ywg6IK4Du4BlV3g/upload)
- 嘗試重構程式
- 2人玩家 Dealer、Player (生成1個Class - 創建2實體p1,p2, 參數 )
- 每一步取牌後輸出當時時間 (*)
- 把整個遊戲過程輸出到txt中作記錄 (*)

## 功課：取得API資料
給定天氣API，取得目前天氣，並輸出。
嘗試尋找其他 API / 網站，看看使用相同方法能否成功取得你想要的資料
繳交日期：2024-10-15 23:59
繳交地址：[https://hamster.cpttm.org.mo/spaces/E_xEKq9Ywg6IK4Du4BlV3g/upload](https://hamster.cpttm.org.mo/spaces/E_xEKq9Ywg6IK4Du4BlV3g/upload)

## 常用Module - datetime

```python
# 引入 datetime
from datetime import datetime

# 取得目前日期時間
t_now = datetime.now()
t_now_s = datetime.now().timestamp()
print(t_now)
print(t_now_s)

# 定義要解析的日期字符串
date_string = "2025-09-27 14:30"
parsed_date = datetime.strptime(date_string, "%Y-%m-%d %H:%M")

# 計算時間差
diff_time = parsed_date - now


# 兩個 datetime 對象相減時，得到的是一個 timedelta 對象，這個對象不能直接使用 strftime() 方法
# 獲取天數和秒數
days = diff_time.days
seconds = diff_time.seconds

# 拆開小時、分鐘、秒
ans_hour = int(diff_time / 3600)
ans_min = int(diff_time % 3600 / 60)
ans_sec = int(diff_time % 3600 % 60)

# 格式化為字符串
result_string = f"時間差: {days}天{ans_hour}小時{ans_min}分鐘{ans_sec}秒"
print(result_string)

```
    
## 格式化日期

### 有關日期
| 格式 | 含義 |
| :-: | :-: |
| %y | （00 - 99）兩個數字表示的年份 |
| %Y | 完整的年份（4個數字表示年份） |
| %m | 月份（01 - 12） |
| %d | 日期（0-31） |
| %b | 本地月份名稱的簡寫（如八月份為agu） |
| %B | 本地月份名稱的全稱（如八月份為august） |
| %a | 本地星期名稱的簡寫（如星期四為Thu） |
| %A | 本地星期名稱的全稱（如星期四為Thursday） |


### 有關時間
| 格式 | 含義 |
| :-: | :-: |
| %H | 一天中的第幾個小時（24小時制，00 - 23） |
| %I | 第幾個小時（12小時制，0 - 11） |
| %M | 分鐘數（00 - 59） |
| %S | 秒（00 - 61） |
| %p | 本地am或者pm的識別字 |
| %j | 一年中的第幾天（001 - 366） |

## 練習
請計算現在距離 2024年10月4日21:45 還有多少小時、分、秒。

```python
# 請計算現在距離 2024年10月4日21:45 還有多少小時、分、秒。

from datetime import datetime

# 取得目前時間 
now_time = datetime.now() # datetime格式

# 目標時間
target_string = "2024-10-15 21:45"
target_time = datetime.strptime(target_string, "%Y-%m-%d %H:%M") # datetime格式

# 兩日期相減
time_diff = target_time - now_time
print(time_diff)

days = time_diff.days
diff_seconds = time_diff.seconds

print(f"{days} {diff_seconds}")

ans_hour = int(diff_seconds / 3600)
ans_min = int(diff_seconds % 3600 / 60)
ans_sec = int(diff_seconds % 3600 % 60)

print(f"現在距離{target_string}, 還有{days}天{ans_hour}小時{ans_min}分鐘{ans_sec}秒")
```

## 補充常用時間函數 time.sleep()
若我們要程式等待一定時間後再執行下一步，可以使用`sleep(秒)`這個function

```python
import time
from datetime import datetime

now = datetime.now()
print(now)

time.sleep(2)

now = datetime.now()
print(now)
```


# 常用Module - os
- 得到當前的工作目錄的路徑：os.getcwd( )
- 取得當前工作路徑的文件列表：os.listdir(os.getcwd())
- 將一個文件名與擴展名分開。 os.path.splitext()

## 資料補充 - 路徑 path
在系統中，對於路徑(Path)我們有兩種標識方法
1. 絕對路徑
2. 相對路徑

## 絕對路徑
絕對路徑是從文件系統的根目錄（例如，在 Windows 上是盤符如 C:，在 Unix/Linux 上是/）開始的完整路徑。它指定了文件或目錄的完整位置，不依賴於當前工作目錄。絕對路徑通常包含完整的目錄結構，以及文件或目錄的名稱。例如：

在 Windows 上的絕對路徑：`C:\Users\Username\Documents\file.txt`

在 Unix/Linux 上的絕對路徑：`/home/username/documents/file.txt`

## 絕對路徑
相對路徑是相對於當前工作目錄的路徑。它指定了文件或目錄相對於當前位置的位置。根據當前工作目錄的不同，相對路徑可能會有所變化。

如果當前工作目錄是 C:\Users\Username

相對路徑 Documents\file.txt 將指向 C:\Users\Username\Documents\file.txt

需要注意的是，相對路徑也可以使用特殊符號來表示路徑關系：

## 絕對路徑、相對路徑表示

請注意，在 python 中，路徑一律用單引號裝 `'path'`

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202410041550961.png)

### `/` ：根目錄
### `./`：當前同級目錄
### `../` ：上級目錄

```python
open('檔名1.txt')

open('/data/檔名2.txt')

open('./data/檔名3.txt')

open('../data/檔名4.txt')

open('C:\\user\\檔名5.txt')
```


## 資料補充 - 文件輸入/輸出流
在Python中，我們可以透過文件輸入/輸出流open() 處理文件的新增/修改
基礎用法
```python
f = open("文件名", "打開方式")

f = open("demofile.txt", "w")
```
有四種打開文件的不同方法（模式）：
"r" - 讀取 - 默認值。打開文件進行讀取，如果文件不存在則報錯。
"a" - 追加 - 打開供追加的文件，如果不存在則創建該文件。
"w" - 寫入 - 打開文件進行寫入，如果文件不存在則創建該文件。
"x" - 創建 - 創建指定的文件，如果文件存在則返回錯誤。

### 寫入文件
```python
try:
    my_file = open("demo.txt", "w")

    my_file.write("你好，我叫Leo\n")
    my_file.write("現在是 CM540 課程 \n")

    my_file.close()

except Exception as E:
    print(E)
```

### 讀取文件
使用 read() 和 readline()
```python
try:
    my_file = open("demo.txt", "r")
   
    rs = my_file.read()
    print(rs)
   
    rs2 = my_file.readline()
    print(rs2)
   
except Exception as E:
    print(E)
```

使用 for 迴圈
```python
try:
    my_file = open("demo.txt", "r")

    for i in my_file:
        print(i)
   
except Exception as E:
    print(E)
```

## 練習
嘗試每2秒輸出現在的時間(共5次)，記錄在 time_record.txt 中

Ex : 
2024年10月4日 20:00:02
2024年10月4日 20:00:04
2024年10月4日 20:00:06
2024年10月4日 20:00:08
2024年10月4日 20:00:10

```python
import time
from datetime import datetime

for i in range(5):
    now = datetime.now()
    now = now.strftime("%Y%m%d %H:%M:%S") #格式化日期
    try:
        myfile = open("date_record2.txt","a")
        myfile.write(f"{str(now)}\n")
    except Exception as E:
        print(E)
        
    time.sleep(2)
```


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
