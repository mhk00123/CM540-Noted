# Lesson 7 - 物件、Module(time、os)、輸入流輸出流、pip

**tags: `python`** **`CM-540`** **`Lesson7`**

物件、Module(time、os)、輸入流輸出流、pip

## Slide
課件：[https://docs.google.com/presentation/d/15Yld0Ppk5lrHQV_FyxswlJePxbhe7zyFZ9xkh1E_gmE/edit?usp=sharing](https://docs.google.com/presentation/d/15Yld0Ppk5lrHQV_FyxswlJePxbhe7zyFZ9xkh1E_gmE/edit?usp=sharing)

## 作業 - 21 點遊戲(final)
1. 嘗試重構程式
2. 2人玩家 Dealer 、Player
3. 每一步取牌後輸出當時時間
4. 把整個遊戲過程輸出到txt中作記錄 *(嘗試)

繳交期限：2024-10-04 23:59:59
繳交：[https://hamster.cpttm.org.mo/spaces/E_xEKq9Ywg6IK4Du4BlV3g/upload](https://hamster.cpttm.org.mo/spaces/E_xEKq9Ywg6IK4Du4BlV3g/upload)

# 物件導向程式設計(Object-oriented programming、OOP)
在學習程式語言時，或多或少都有聽過物件導向程式設計(Object-oriented programming，簡稱OOP)，它是一個具有物件(Object)概念的開發方式，能夠提高軟體的重用性、擴充性及維護性，在開發大型的應用程式時更是被廣為使用，所以在現今多數的程式語言都有此種開發方式，Python當然也不例外。而要使用物件導向程式設計就必須對類別(Class)及物件(Object)等有一些基本的了解，包含了：
- 物件(Object)
- 類別(Class)
- 屬性(Attribute)
- 方法(Method)
- 建構式(Constructor)

# 類別(Class)、物件(Object)
簡單來說，類別(Class)就是物件(Object)的藍圖。

就像要生產一部汽車時，都會有設計圖，藉此可以知道此類汽車會有哪些特性及功能，類別(Class)就類似設計圖，會定義未來產生物件時所擁有的屬性(Attribute)及方法(Method)。

而最終透過藍圖產生的實體，則叫 物件(Object)

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202405281442328.png)


### 汽車Class及實體化汽車物件的例子
```python
# 汽車類別 Class
class Cars:
    # 建構式 Constructor
    def __init__(self, color, seat):
        self.color = color  # 顏色 屬性Attribute
        self.seat = seat  # 座位 屬性Attribute

    # 方法(Method)
    def drive(self):
        print(f"My car is {self.color} and {self.seat} seats.")

# 實體化物件 (Object)
car_1 = Cars(“Yellow”, 5)
car_2 = Cars(“White”, 7)
```

## 屬性(Attribute)
```python
# 汽車類別 Class
class Cars:
    # 建構式 Constructor
    def __init__(self, color, seat):
        self.color = color  # 顏色 屬性Attribute
        self.seat = seat  # 座位 屬性Attribute


# 實體化物件 (Object)
car_1 = Cars(“Yellow”, 5)

# 存取屬性
print(car_1.color) # Yellow 
```
## 方法(Method)
```python
# 汽車類別 Class
class Cars:
    # 建構式 Constructor
    def __init__(self, color, seat):
        self.color = color  # 顏色 屬性Attribute
        self.seat = seat  # 座位 屬性Attribute

    # 方法(Method)
    def drive(self):
        print(f"My car is {self.color} and {self.seat} seats.")

# 實體化物件 (Object)
car_1 = Cars(“Yellow”, 5)

# 呼叫方法
car_1.drive()
```

## 練習 : 構建學生Student的Object和Class
每個學生中的資料包含:
- 中文姓名
- 英文姓名
- 性別
- 學號
- 年級
- 並且每個學生中都可以透過 intro() 做一個自我介紹

```python
class Student:
    def __init__(self, ch_name, en_name, sex, class_num, grade):
        self.ch_name = ch_name
        self.en_name = en_name
        self.sex = sex
        self.class_num = class_num
        self.grade = grade
    
    def intro(self):
        print(f"你好，我名字是{self.ch_name}, 英文名是{self.en_name}")
        print(f"我是{self.sex}性, 目前就讀{self.grade}年級")
    
stu_Leo = Student("尼奧","Leo","男",12345,6)

stu_Leo.intro()
        
```


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

## 常用Module - datetime
datetime module 該模塊提供了各種與時間相關的函數。

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