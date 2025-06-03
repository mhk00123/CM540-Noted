# Lesson 7 - 物件、Module(time、os)、輸入流輸出流、pip

**tags: `python`** **`CM-540`** **`Lesson7`**

OOP、Module(time)、pip

## 功課：21 點遊戲單人版(Final)

繳交連結：[https://hamster.cpttm.org.mo/spaces/RMe_Iu_nn3Tv7ufj1-CXEQ/upload](https://hamster.cpttm.org.mo/spaces/RMe_Iu_nn3Tv7ufj1-CXEQ/upload)

截止日期：2025-06-08

- 把玩家模組化(Class)
- 新增玩家Dealer、Player
- 把整個遊戲過程輸出到txt中作記錄 *(嘗試)

## Slide
課件：[https://docs.google.com/presentation/d/15Yld0Ppk5lrHQV_FyxswlJePxbhe7zyFZ9xkh1E_gmE/edit?usp=sharing](https://docs.google.com/presentation/d/15Yld0Ppk5lrHQV_FyxswlJePxbhe7zyFZ9xkh1E_gmE/edit?usp=sharing)

# 例外狀況處理: try except
執行 Python 程式的時候，往往會遇到「錯誤」的狀況。如果沒有好好處理錯誤狀況，就會造成整個程式壞掉而停止不動。因此，透過「例外處理」try except 機制。能夠在發生錯誤時進行對應的動作，不僅能保護整個程式的流程，也能夠掌握問題出現的位置，馬上進行修正。

## 錯誤例子
觀察以下程式碼:
```python
a = "Hello"
b = a + 1
print(b)
```

String 和 int 不能作相加的動作
此處會出現 `TypeError` 的錯誤，程式終結

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202506031421324.png)


## 錯誤類型

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202403261728234.png)

# 使用 Try 和 Except
我們可以透過 `try`、`except`組合捕捉對應執式執行錯誤。
## 基本用法
```python
try:
    # 需要執行的程式碼`

except:
    # 如果有錯誤，則執行
```

### 例子
```python
try:
    a = "Hello"
    b = a + 1
except:
    print("程式出現錯誤，請檢查！")
```

## 可以為每一個Error作特定的判斷

```python
try:
    # 需執行的程式碼

except TypeError:
	print('型別發生錯誤')
    
except NameError:
    print('使用沒有被定義的對象！')

except IndexError:
    print('沒有特定的index，請重新確認!')

except Exception as E:
    print('不知道怎麼了，反正發生錯誤！')
```

## Try Except 所有用法
```python
try:
    # 需執行的程式碼

except Exception as E:
    # 若有錯誤，捕捉錯誤訊息，以變數 E 作儲存

else:
    # 若沒有錯誤則執行

finally:
    # 不論有沒有錯誤都執行
```

## Try Except 意義
- 處理預期的錯誤：
例如處理使用者輸入、檔案操作、網路請求等可能失敗的操作

- 提供替代方案：
當主要方法失敗時，可以使用備用方法繼續執行

- 盡獲特定的異常，而不是捕獲所有異常 (except Exception)
- **將 try 區塊保持盡可能減小**，只包含可能引發異常的程式碼


# 練習1:

請使用 Try Except 令以下這段程式碼可以順利執行
若執行錯誤則由系統補上 key 為 3 的內容 或是其他修正方法

```python
temp = {
    1: "我是Pie", 
    2: "我是Pie2"
}

print(temp[3])
```

### 解答
```python
temp = {
    1: "我是Pie", 
    2: "我是Pie2"
}

# 有問的題的應是這段程式碼

try:
    print(temp[3])

except:
    print("沒有這個key，系統為你新增一個")
    temp[3] = "我是Pie3"
    print(temp[3])
```

## 練習2
優化我們早前的手動抽牌流程
- 由使用者輸入數字(1-13)，並轉為int類型
- 若使用者輸入bye，則結束
- 輸入其他英文字母，則提示輸入錯誤，請重新輸入

```python
while(True):
    user_input = input("請輸入一個數字，若輸入bye則結束：")
   
    if(user_input == "bye"):
        print("bye bye!")
        break
   
    else:
        user_input = int(user_input
```

### 解答
```python
while(True):
    user_input = input("請輸入一個數字，若輸入bye則結束：")
    
    if(user_input == "bye"):
        print("結束程式")
        break
    
    else:
        try:
            user_input = int(user_input)
            print(f"你輸入的數字是：{user_input}, Type: {type(user_input)}")
        except:
            print("輸入錯誤，請輸入數字或bye")
            continue
```

# 物件導向程式設計(Object-oriented programming、OOP)
過去我們一條一條的寫程式，加上一些整合式的 function，並以排序的方式讓編譯器知道程式執行的先後順序，這就目前我們寫程式一般常見的架構:

**程序導向設計 (Procedure-Oriented Programming, POP)**

現代軟體開發中，物件導向程式設計(Object-oriented programming、OOP) 是主流設計範式，幾乎所有主流語言（如 Java、Python、C++、C#）都支援它。以下是它的核心優勢：
- OOP 是一種「用物件（對象）來組織程式碼」的設計方式。
- 就像現實世界中的每一「物體」都有自己的「屬性」和「行為」一樣
- OOP 把程式中的「**數據**」和「**操作數據的函數**」打包成一個個獨立的「物件」，讓程式更容易管理和擴充。

想像你在玩樂高積木，樂高有許多相同形狀的模組（例如輪胎、門窗），你可以用這些模組快速拼出不同的東西（車子、房子等）。

**OOP 就像在寫程式時，把程式碼拆成可重複使用的『模組』**

**再用這些模組組合出完整的程式**

## 為什麼要教大家?
以入門學習來說，根本不需要學OOP。

以POP的架構，甚至連 function 都不用寫就可以一步一步完成目標了。

但是每樣功能存在一定都有它的道理，OOP就是軟體不停開發、演進下的一個產物，當程式能力到一定的程度後，一旦開始做比較大的專案或是計畫，則就會需要用到OOP的技巧。


## OOP 的五大核心
在學習程式語言時，或多或少都有聽過物件導向程式設計(Object-oriented programming，簡稱OOP)，它是一個具有物件(Object)概念的開發方式，能夠提高軟體的重用性、擴充性及維護性，在開發大型的應用程式時更是被廣為使用，所以在現今多數的程式語言都有此種開發方式，Python當然也不例外。而要使用物件導向程式設計就必須對類別(Class)及物件(Object)等有一些基本的了解，包含了：
- 物件(Object)
- 類別(Class)
- 建構式(Constructor)
- 屬性(Attribute)
- 方法(Method)

# 類別(Class)、物件(Object)
- 類別／類（Class）：像是「**設計藍圖**」，定義一個物件的「**結構**」。
例如：設計一張「**汽車藍圖**」，寫明汽車應該有顏色、品牌、速度等屬性，以及加速、煞車等功能。

- 物件（Object）：根據「**類別**」的藍圖實際創造出來的「**實例**」。
例如：根據「汽車藍圖」製造出「一台紅色 Toyota 汽車」，這台車就是一個具體的「物件」。


![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202405281442328.png)

## Class 架構
```python
class 類別名稱:
    # 建構子（初始化物件）
    def __init__(self, 參數1, 參數2, ...): 
        self.屬性1 = 參數1  # 定義屬性
        self.屬性2 = 參數2

	# 定義方法（行為）
    def 方法名稱(self, 參數):  
        # 方法要做的事情
        return 結果

# 實體化物件 (Object)
my_OOP_item = 類別名稱(參數1, 參數2, ...)

```

## 汽車Class及實體化汽車物件的例子
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

## 存取屬性(Attribute)
```python
# 汽車類別 Class
class Cars:
    # 建構式 Constructor
    def __init__(self, color, seat):
        self.color = color  # 顏色 屬性Attribute
        self.seat = seat  # 座位 屬性Attribute


# 實體化物件 (Object)
car_1 = Cars("Yellow", 5)

# 存取屬性
print(car_1.color) # Yellow 
```
## 使用方法(Method)
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
car_1 = Cars("Yellow", 5)

# 呼叫方法
car_1.drive()
```

## 練習 : 銀行帳戶
以OOP的概念創建一個銀行帳戶(BankAccount)
每個帳戶包含屬性:
- 帳號
- 餘額

並且每個帳戶都可以對自己的戶口進行以下行為:
- 存款
- 提款
- 查詢餘額

**生成 2 個帳戶作測試**


```python
# 定義 BankAccount 類別
# 定義 BankAccount 類別
class BankAccount:
    # 初始化方法
    def __init__(self, account_number, balance):
        self.account_number = account_number        
        self.balance = balance
        print(f"帳戶創建成功！{self.account_number}，餘額：{self.balance}")  # 提示帳戶創建成功      

    # 提款方法
    def deposit(self, amount):
        self.balance += amount
        print(f"存款成功！餘額：{self.balance}")

    # 存款方法
    def withdraw(self, amount):
        if(amount <= self.balance):
            self.balance =  self.balance - amount
            print(f"提款成功！餘額：{self.balance}")
            
        else:
            print("提款失敗：餘額不足！")   # 提示餘額不足

    # 查詢餘額方法
    def get_balance(self):
        return self.balance

# 建立兩個帳戶物件
account_Leo = BankAccount("1234", 10)     # 創建物件1 - Leo：帳號 1234，初始餘額1000
account_May = BankAccount("5678", 1000)   # 創建物件2 - May：帳號 5678，初始餘額0

# 使用帳戶功能
account_May.deposit(500)                  # May 存入500
account_Leo.withdraw(200)                 # Leo 取款200、提示：提示餘額不足
account_Leo.get_balance()                 # Leo 查詢自己餘額
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
diff_time = parsed_date - t_now

# 兩個 datetime 對象相減時，得到的是一個 timedelta 對象，這個對象不能直接使用 strftime() 方法
# 獲取天數和秒數
days = diff_time.days
seconds = diff_time.seconds

# 拆開小時、分鐘、秒
ans_hour = int(seconds / 3600)
ans_min = int(seconds % 3600 / 60)
ans_sec = int(seconds % 3600 % 60)

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
請由用戶輸入目標日期時間，計算距離現在還有多少天、小時、分、秒。
```python
from datetime import datetime

def cal_time(target_time):
    # 取得目前日期時間
    t_now = datetime.now()

    try:
        parsed_date = datetime.strptime(target_time, "%Y-%m-%d %H:%M:%S")
    except:
        parsed_date = datetime.strptime(target_time, "%Y-%m-%d")

    # 計算時間差
    diff_time = parsed_date - t_now

    # 兩個 datetime 對象相減時，得到的是一個 timedelta 對象，這個對象不能直接使用 strftime() 方法
    # 獲取天數和秒數
    days = diff_time.days        # 天數
    seconds = diff_time.seconds  # 秒數

    # 拆開小時、分鐘、秒
    ans_hour = int(seconds / 3600)
    ans_min = int(seconds % 3600 / 60)
    ans_sec = int(seconds % 3600 % 60)

    # 格式化為字符串
    result_string = f"時間差: {days}天{ans_hour}小時{ans_min}分鐘{ans_sec}秒"
    print(result_string)


#### Main function ####
while(True):
    target_time = input("請輸入目標時間：")
    cal_time(target_time)
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

### 練習 
每隔一秒輸出當前時間
```python
from datetime import datetime
import time

count = 0

while(True):
    time.sleep(1)
    
    t_now = datetime.now()
    str_time = t_now.strftime("%Y年%m月%d日 %H:%M:%S")
    
    print(f"當前時間{str_time} : {count}")
    
    count = count + 1
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
```
2024年10月4日 20:00:02

2024年10月4日 20:00:04

2024年10月4日 20:00:06

2024年10月4日 20:00:08

2024年10月4日 20:00:10
```


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

