# Lesson 8 - pip、API、爬蟲入門

**tags: `python`** **`CM-540`** **`Lesson8`**

os Module、pip、API、爬蟲入門

# 功課 : 21 點遊戲增強(final)
- 嘗試重構程式
- 2人玩家 Dealer 、Player
- 每一步取牌後輸出當時時間
- 把整個遊戲過程輸出到txt中作記錄 *(嘗試)

截止日期：2025-04-01 23:59
繳交地址：[https://hamster.cpttm.org.mo/spaces/iaMUdcYZAHaWIl9bpm3-jw/upload](https://hamster.cpttm.org.mo/spaces/iaMUdcYZAHaWIl9bpm3-jw/upload)


# 功課2 : 
思考工作中可自動化動作為Final Project題目

# Slide
課件：[https://docs.google.com/presentation/d/1Cq-7TjksWri1E_UvoaNF1Vaz4W_xtlI1VOs3oVbB8Qg/edit?usp=sharing](https://docs.google.com/presentation/d/1Cq-7TjksWri1E_UvoaNF1Vaz4W_xtlI1VOs3oVbB8Qg/edit?usp=sharing)


# 常用Module - os
在 Python 中，`os` 模塊是操作系統的接口，提供了與操作系統交互的多種功能，例如管理文件、目錄、執行系統命令等。

## os 模塊功能

```python
import os
```

- 管理文件和目錄（創建、刪除、重命名）。
- 獲取系統信息（當前工作目錄、環境變量）。
- 執行系統命令（如打開文件、運行程序）。
- 處理路徑（跨平台兼容的路徑操作）。
    - 得到當前的工作目錄的路徑：`os.getcwd()`
    - 取得當前工作路徑的文件列表：`os.listdir(os.getcwd())`
    - 把2個路徑組合：`os.path.join(path1, path2)`
    - 將一個文件名與擴展名分開： `os.path.splitext()`

## 資料補充 - 路徑 path
路徑（Path）：計算機中用來定位文件或目錄位置的字符串。
在系統中，對於路徑(Path)我們有兩種標識方法
1. 絕對路徑
2. 相對路徑

### 絕對路徑
絕對路徑是從文件系統的根目錄（例如，在 Windows 上是盤符如 C:，在 Unix/Linux 上是/）開始的完整路徑。它指定了文件或目錄的完整位置，不依賴於當前工作目錄。絕對路徑通常包含完整的目錄結構，以及文件或目錄的名稱。例如：

- 在 Windows 上的絕對路徑：
```
C:\Users\Username\Documents\file.txt
```

- 在 Unix/Linux 上的絕對路徑：
```
/home/username/documents/file.txt
```

### 相對路徑
相對路徑是相對於當前工作目錄的路徑。它指定了文件或目錄相對於當前位置的位置。根據當前工作目錄的不同，相對路徑可能會有所變化。

如果當前工作目錄(`即python程式碼存放的位置`)：`C:\Users\Username`

相對路徑為
```
Documents\file.txt
``` 
將指向 `C:\Users\Username\Documents\file.txt`

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
在Python中，我們可以透過文件輸入/輸出流with open() 處理文件的新增/修改

基礎用法
```python
with open("文件名", "打開方式", encoding="utf-8") as 臨時變數:
    臨時變數.操作()
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

## 組合練習
向 `.\tempTxT\`生成50個.txt文件，並在每一個txt中寫入該文件名。
```python
import os

# 確保目錄存在
directory = './tempTxT'
if not (os.path.exists(directory)):
    os.makedirs(directory)

# 生成 50 個 .txt 文件
for i in range(1, 51):
    # 文件名
    filename = f'txt文件_{i}.txt'

    # 文件路徑
    filepath = os.path.join(directory, filename)

    # 寫入文件名到文件中
    with open(filepath, 'w', encoding='utf-8') as file:
        file.write(f'這是文件: {filename}')

print(f'已生成 50 個 .txt 文件到目錄: {directory}')
```

# 常用Module - datetime
```python
from datetime import datetime
```

## datetime 出現的變數類型
用於處理日期、時間相關的問題，在 datetime 下，日期時間會有3種格式。
- datetime時間格式 : class `datetime`
- 格式輸出用 : class `String`
- 兩日期相減/加 : class `datetime.timedelta`

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

## 常用time function - time.sleep()
若只計算時間(不考慮日期)，可以直接使用 `time` module
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
