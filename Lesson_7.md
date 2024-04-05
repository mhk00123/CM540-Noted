# Lesson 7 - Module(time、os)、輸入流輸出流、pip

**tags: `python`** **`CM-540`** **`Lesson7`**

Module(time、os)、輸入流輸出流、pip

## Slide
課件：[https://tinyurl.com/35kuy3cn](https://tinyurl.com/35kuy3cn)

# Python - Module
Module(模塊)，是一個Python文件，以`.py`結尾。

在Module中，我們可以把定義好Function、變量、代碼等封裝。使其可以在其他Python文件中使用。

我們可以認為一個模塊就是一個工具包、每一個工具包中有著各種各樣的工具令我們實現各種不同的功能。

使用Module前，需要導入(import)

### 基本語法
```python
import module_name [as 別名]

import random 

import random as rd
```

### 基本語法 from
```python

from module_name import module_name|function_name [as 別名]

from random import *

from random import randint as rINT
```

# Python - 常用Module(系統內建)
- math：用來進行數學計算，它提供了很多數學方面的專業函式
- os：提供了與作業系統互動的功能，比如檔案和目錄操作
- datetime：用於處理日期和時間
- json：專門用來處理 JSON 格式資料

# 常用Module - time
time module 該模塊提供了各種與時間相關的函數。

時間表示方法：時間戳( TimeStamp )

在 time module 中的 function 很常會以時間戳作return statment

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


## 常用Module - time
- 取得目前時間戳：time( )
- 把時間戳轉換為 str : ctime( )
- 把時間戳轉換為 Time Structure : gmtime( )
- 把 Time Structure 轉換為指定時間：strftime( 時間標記格式 )
- 把 str 轉為 Time Structure：strptime(string, 時間標記格式 )

```python
import time as T

# 取得 TimeStamp
timestamp = T.time()
print(timestamp)

# 把時間戳轉換為 string
time_str = T.ctime(timestamp)
print(time_str)
print(type(time_str))

# 取得gmt+0時間的 time struct 格式時間戳
struct_time = T.gmtime(timestamp)
print(struct_time)

# 取得本地時間的 time struct 格式時間戳
struct_time_local = T.localtime(timestamp)

# 格式化時間
# Time Structure -> String
format_time = T.strftime("%Y-%m-%d %I:%M:%S", struct_time_local)
print(format_time)

# String -> Time Structure
str_time = "2024-01-01"
tr_time = T.strptime(str_time, "%Y-%m-%d")
print(tr_time)
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
`.` 表示當前目錄
`..` 表示上一級目錄

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