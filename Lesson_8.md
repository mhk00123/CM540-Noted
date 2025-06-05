# Lesson 8 - pip、API、爬蟲入門

**tags: `python`** **`CM-540`** **`Lesson8`**

文件輸入流、輸出流、Module、pip、API、爬蟲入門

# 作業1：
截止時間：2025年6月8日 23:59

{% hint style="info" %}

# 21 點遊戲單人版 Final

繳交網址：[https://hamster.cpttm.org.mo/spaces/RMe_Iu_nn3Tv7ufj1-CXEQ/upload](https://hamster.cpttm.org.mo/spaces/RMe_Iu_nn3Tv7ufj1-CXEQ/upload)

---
- 把玩家模組化(Class)
- 新增玩家Dealer、Player
- 把整個遊戲過程輸出到txt中作記錄 *(嘗試)

{% endhint %}

# 作業2：

{% hint style="info" %}

# 功課 :
**思考**工作中可自動化動作為Final Project題目

{% endhint %}


# Slide
課件：[https://docs.google.com/presentation/d/1Cq-7TjksWri1E_UvoaNF1Vaz4W_xtlI1VOs3oVbB8Qg/edit?usp=sharing](https://docs.google.com/presentation/d/1Cq-7TjksWri1E_UvoaNF1Vaz4W_xtlI1VOs3oVbB8Qg/edit?usp=sharing)

# 創建/讀取文件 - 文件輸入/輸出流
在Python中，我們可以透過文件輸入/輸出流with open() 處理文件的新增/修改

## 語法
```python
with open("路徑及文件名", "打開方式", encoding="utf-8") as 臨時變數:
    臨時變數.操作()
```

## 基礎用法
創建一個 demo
```python
with open("demo.txt", "w") as my_file:
    my_file.write("你好，我叫Leo\n")
```



### 有四種打開文件的不同方法（模式）：
`r` - 讀取 - 默認值。打開文件進行讀取，如果文件不存在則報錯。

`a` - 追加 - 打開並供追加文件的最後，如果不存在則創建該文件。

`w` - 寫入 - 打開文件進行寫入，如果文件不存在則創建該文件。

`x` - 創建 - 創建指定的文件，如果文件存在則返回錯誤。

### 操作
- `write`
    - 將指定的字符串寫入文件。一次只能寫入一個字符串
    - 不會自動添加換行符，需要手動添加 `\n`
- `read`
    - 讀取文件的**全部**內容。
- `writelines`
    - 將一個字符串列表（或其他可迭代對象）寫入文件。
    - 不會自動添加換行符，需要手動在每個字符串末尾添加 `\n`。比 write 更適合一次性寫入多行內容。
- `readline`
    - 讀取文件的一行內容。
    - 每次調用只讀取一行。返回的字符串包含行尾的換行符 \n。
    - 適合逐行處理大文件，避免內存不足。
    
## 寫入、讀取
```python
# 使用 'w' 模式來寫入文件，如果文件不存在則會創建它
# write()
with open('example.txt', 'w', encoding='utf-8') as file:
    file.write('這是第一行文字。\n')
    file.write('這是第二行文字。\n')


# writelines()
lines_content = ['這是第一段長文字\n', '這是第二段長文字\n', '這是第三段長文字\n']
with open('example.txt', 'a', encoding='utf-8') as file:
    file.writelines(lines_content)


# 使用 'r' 模式來讀取整份文件
# read()
print("##### 使用 read() #####")
with open('example.txt', 'r', encoding='utf-8') as file:
    content = file.read()
    print(content)


# readline()
print("##### 使用 readline() #####")
with open('example.txt', 'r', encoding='utf-8') as file:
    while True:
        line = file.readline()
        if not line:  # 如果讀取到文件末尾，line 為空字符串
            break
        print(line.strip())  # 使用 strip() 去除換行符
```

# 文件路徑 - 絕對路徑
在電腦世界中，「路徑」就是表示當前文件的地址。

例如：我們要透過程式訪問 `C:\Code\Lesson_1\abc.txt`

我們解讀作 ： 在 `C:\Code\Lesson_1` 資料夾中的 `abc.txt` 檔案

而像這種把確實位置全部寫出來的寫法`C:\Code\Lesson_1\abc.txt`，稱作「**絕對路徑**」

# 文件路徑 - 相對路徑
所謂「相對路徑」基於當前目錄，透過A文件與B文件的位置關係去描述路徑。

因此「相對路徑」一定會出現 2 個文件的關係：

**稱作B文件相對於A文件的xx位置。**

## 文件路徑 - 相對路徑(同層)
同樣地，如我們要透過程式訪問 `C:\Code\Lesson_1\abc.txt ` 
(假設，這個程式也位於 Lesson_1資料夾中)

這裡我們便有2個文件的關係：
- A文件(程式)     `C:\Code\Lesson_1\main.py`
- B文件(abc.txt)  `C:\Code\Lesson_1\abc.txt`

我們便可以以相對路徑描述 B 文件的位置:
*B文件相對於A文件的同一層的位置*

同一層表示方法，路徑直接以文件名標識 `abc.txt` 或使用 1 個 `.\`
即 `.\abc.txt`

## 文件路徑 - 相對路徑(下一層)
A文件(程式)      `C:\Code\main.py`
B文件(abc.txt)  `C:\Code\Lesson_1\abc.txt`

路徑表示：`.\Lesson_1\abc.txt`

## 文件路徑 - 相對路徑(上一層)
上一層文件，以`..`表示表上層

A文件(程式)     `C:\Code\Lesson_1\Code\main.py`
B文件(abc.txt)  `C:\Code\Lesson_1\abc.txt`

路徑表示：`..\abc.txt`


## 練習 - 心情記錄
```python
# 獲取用戶輸入
date_input = input("請輸入今天的日期（YYYY-MM-DD）：")
mood = input("請輸入今天的心情：")
journal_entry = input("請輸入一句話描述今天的事情：")

# 構造文件名
filename = f"{date_input}_{mood}.txt"

# 構造完整路徑（相對路徑）
file_path = f"Daily/{filename}"

# 寫入日記內容
with open(file_path, "w", encoding="utf-8") as file:
    file.write(f"日期：{date_input}\n")
    file.write(f"心情：{mood}\n")
    file.write(f"記錄：{journal_entry}\n")

# 提示保存成功
print(f"日記已保存至：{file_path}")
```

# Python - Module
Module(模塊)，是一個Python文件，一般以`.py`結尾。

在Module中，我們可以把定義好的Class、Function、變量、代碼等封裝。

使其可以在其他Python文件中使用。

我們可以認為一個模塊就是一個工具包、每一個工具包中有著各種各樣的工具令我們實現各種不同的功能。

使用Module前，需要進行導入`import`

### 基本語法
```python
import module_name [as 別名]
```

```python
import random          # 導入 random 

import random as rd    # 導入 random 以別名 rd 記錄
```


### 基本語法 from
```python
from module_name import module_name|function_name [as 別名]
```
```python
from random import randint as rINT
```


# Python - 常用Module(系統內建)
- math：用來進行數學計算，它提供了很多數學方面的專業函式
- os：提供了與作業系統互動的功能，比如檔案和目錄操作
- datetime：用於處理日期和時間
- json：專門用來處理 JSON 格式資料


# 常用Module - datetime
```python
from datetime import datetime
```

## 時間戳( TimeStamp )
**時間戳**：是一串十分長的數字

他所表示的是(格林威治時間) 1970年1月1日 00:00到現所經歷的秒數

1970年1月1日計算機時間元年，UNIX設計者把這一天作為所有計算機時間的起點

## 知識補充：二進制
二進制（binary）指以2為底數的記數系統，以2為基數代表系統是二進位制的。這一系統中，通常用兩個不同的數字0和1來表示。

電腦中的最小儲存單位 bits : 8bits = 1 byte

所以我們在二進制中一般以8個為1組 即

- 0(10) 記作 00000000
- 255(10) 記作 11111111
- 256(10) 記作 00000001 00000000

### 知識補充：2038年問題
過去曾發生千年蟲問題( 1999年過渡到 2000 年)

主因是因為舊有的電腦都是以 32 位元 (2^32) 作儲存大小

因此 time module 最大只可以記錄 2^(32-1) = 2,147,483,647 秒的時間戳

即由 1970年1月1日00:00起計

所有32位元的電腦，**在2038年1月19日3時14分07秒**之後便會出現記錄錯誤
> https://zh.wikipedia.org/zh-hant/2038%E5%B9%B4%E9%97%AE%E9%A2%98


## datetime 出現的變數類型
用於處理日期、時間相關的問題，在 datetime 下，日期時間會有3種格式。
- datetime時間格式 : **class** : `datetime`
- 格式輸出用 : **class** : `String`
- 兩日期相減/加 : **class** : `datetime.timedelta`

## 格式化日期時間
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

## 使用方法
```python
from datetime import datetime

# 1. 取得目前日期時間
t_now = datetime.now()
print(t_now)

# 2. 自定義一個時間
# 參數(可留空) : datetime(年, 月, 日, 時, 分, 秒)
d_time = datetime(2025, 3, 20, 18, 45, 00)
d_time2 = datetime(2025, 3, 20)
print(d_time)
print(d_time2)

# 3. 格式化輸出(datetime -> string)
# strftime()
formatted_date = t_now.strftime("%Y年%m月%d日 %H時%M分%S秒")
print(formatted_date)

# 4. 格式化輸入(string -> datetime)
# strptime()
date_string = "2026-10-05 15:45:30"
format_string = "%Y-%m-%d %H-%M-%S"

format_datetime = datetime.strptime(date_string, format_string)
print(format_datetime)

# 5. 日期時間計算
# 計算後的結果為 timedelta *
date1 = datetime.now()
date2 = datetime(2025,3,20,21,45,00)

time_diff = date2 - date1
print(time_diff)
print(type(time_diff))

# 5.1 提取結果
# timedelta 中可提取2個結果
diff_days = time_difference.days
diff_seconds = time_difference.total_seconds()

# 5.2 若需要得到確實時間，需要進行轉換
# 計算小時、分鐘和秒
hours = diff_seconds // 3600
minutes = (diff_seconds % 3600) // 60
seconds = diff_seconds % 60

print(f"相差 {hours:.0f} 小時 {minutes:.0f} 分鐘 {seconds:.2f} 秒")

```

# time module
若只計算時間(不考慮日期)，可以直接使用 `time` module

主要用於處理時間戳（timestamp），即從 Unix 紀元（1970-01-01 00:00:00 UTC）開始經過的秒數（浮點數）。
適合簡單的計時、延遲或低精度的時間操作。

- 獲取當前時間戳 `time.time()`
- 程序延遲 `time.sleep()`

```python
import time
```
其中，最常用的功能，為 time.sleep()

若我們需要程式進行特定時間的等待，此時可以使用 time.sleep(秒)等待

```python
import time
from datetime import datetime

while(True):
    now = datetime.now()
    current_time = now.strftime("%H:%M:%S")
    print(f"現在的時間是：{current_time}")
    time.sleep(1)
```

## 練習 - 倒數計時
請用戶輸入計時秒數，顯示完成日期時間開始計時，計時記錄在 time_record.txt 中 


```python
import time
from datetime import datetime, timedelta

target_second = input("請輸入要計時幾秒：")
target_second = int(target_second)

# 因計算時需要引入 timedelta 類別
# 所以需要從 datetime 模組中引入 datetime 和 timedelta 類別
completion_time = datetime.now() + timedelta(seconds=target_second)

# 記錄計時開
with open("timer_log.txt", "a", encoding="utf-8") as file:
    print("##### 計時開始！#####")
    print(f"計時將在 {completion_time.strftime('%Y-%m-%d %H:%M:%S')} 完成。")
    file.write("##### 計時開始！#####\n")
    file.write(f"計時將在 {completion_time.strftime('%Y-%m-%d %H:%M:%S')} 完成。\n")
    
    # 進入計時迴圈
    while(datetime.now() < completion_time):
        
        diff_time = completion_time - datetime.now()
        diff_seconds = diff_time.total_seconds()
        rs = f"{datetime.now().strftime('%Y-%m-%d %H:%M:%S')} - 剩餘時間：{diff_seconds:.0f} 秒"
        print(rs)
        file.write(rs + "\n")
        
        time.sleep(1)

    print(f"{datetime.now().strftime('%Y-%m-%d %H:%M:%S')} - 計時完成！")
    file.write(f"{datetime.now().strftime('%Y-%m-%d %H:%M:%S')} - 計時完成！\n")
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
