# Lesson 2
變數、資料型態、輸入輸出、邏輯判斷

**tags: `python`** **`CM-540`** **`Lesson2`**

# Slide
課件：[https://docs.google.com/presentation/d/1V65yCaEIEPAe7G4l96b3gdxwrjxu6e9AdiGx25um2YY/edit?usp=sharing](https://docs.google.com/presentation/d/1V65yCaEIEPAe7G4l96b3gdxwrjxu6e9AdiGx25um2YY/edit?usp=sharing)


# Python 基本組成
- 資料型態: int、float、str、bool
- 儲存容器: list、tuple、set、dict
- 輸出與輸入: print()、input()
- 運算子、運算式：加減乘除、大小等於
- 流程控制(選擇性敘述): if、elif、else
- 重複執行的迴圈: for、while、switch
- 例外狀況處理: try except

## 變數類型、資料型態
在Python中，基資料型態有以下4類：
- int 整數：1、100、-50
- float 浮點數：3.14、2.0、-6.7
- string (str) 字串：必須用單引號或雙引號括住，"Hello World"、 '1234'
- bool 布林型態：用來表示真或假，只有兩個值 True 和 False

資料型態在程式中很重要，它們決定了資料的處理方式和運算規則，因此在撰寫程式時需要確保資料型態的一致性和適當使用。

## 字串分割
如果要將字串分割，在Python中使用 `[ start_index : end_index+1 ]` 作分割 
> 注意一般來說 `[ ]` 中的 index 都是取頭不取尾 
```python
name = "LeoTam"   
my_phone_num = 28781313

# 如果我想要取得前 3 碼
result = name[0:3] 
print(result) # Leo

# 想取得數字類型的前 3 碼
result2 = my_phone_num[0:3]
print(result2) # Error
```

## 字串相加
如果要將兩個字串連接起來，在Python中使用 `+`
```python
first_name = "Leo"
last_name ="Tam"
my_phone_num = 28781313

mix_str = first_name + last_name + str(my_phone_num) 

print("Hi, My name is " + first_name + " " + last_name + ", my phone number is " + str(my_phone_num))
# Hi, My name is Leo Tam, my phone numer is 28781313

print(mix_str)
# Hi, My name is Leo Tam, my phone numer is 28781313
```

## 強制轉型
{% hint style="info" %}
補充資料：函數/方法(Function)，Python自定了很多不同的已經寫好的Function，我們先在這邊開一個頭，在後續的章節中我們會再詳講。所謂函數就是『敘述的集合』，並且以一個函數名稱來代表此敘述集合。通常一個函數可以完成某項功能，所以可以把函數想像成是一種對資料的操作方法。一般來說，函數以這樣的返式表示`函數名()`，例如我們接觸到的`print()` `type()`便是Python內建的函數。
{% endhint %}

從剛才的例子中，我們發現不同型態的變數是無法進行相互運算的，那麼若現在有需要把變數指定類型，可以使用Python中內置的函數對變量類型進行強制轉換

* `int()`：將一個數值或字符串轉換成整數，可以指定進制。
* `float()`：將一個字符串轉換成浮點數。
* `str()`：將指定的對像轉換成字符串形式，可以指定編碼。
* `chr()`：將整數轉換成該編碼對應的字符串（一個字符）。
* `ord()`：將字符串（一個字符）轉換成對應的編碼（整數）。

```python
a = 100
b = 12.345

print(type(a)) # <class 'int'>
print(type(b)) # <class 'float'>

c = str(a)
print(c) # 100
print(type(c)) # <class 'str'>

d = int(b)
print(d) # ???
```

## 輸入及輸出

到目前為止我們都只有在程式中輸出特定的變數，那麼若今天我們需要由使用者輸入變數，那麼就需要使用Python的輸入`input()`功能。`input()` 是 Python 的內置函數，用於從控制台讀取用戶輸入的內容。`input()` 函數總是以**字符串**的形式來處理用戶輸入的內容，所以用戶輸入的內容可以包含任何字符。

```python
a = input("請輸入內容") # 輸入 123

print(a) # 123
print(type(a)) # <class 'str'>
```

若我們需要對變數進行運算，則需要對其進行強制轉型

```python
a = input("請輸入數字1： ") # 輸入 123
b = input("請輸入數字2： ") # 輸入 456

# 強制轉型並重新賦值
a = int(a)
b = int(b)

# 兩個變數相加
rs = a + b

print(rs) # 579

print(type(a))  # <class 'int'>
print(type(b))  # <class 'int'>
print(type(rs)) # <class 'int'>
```

**簡寫**

在Python中，函數可以嵌套，執行順序以括號優先。套用以上例子，我們可以把`input()`的程式碼簡化為：

```python
# 在輸入後，強制轉型並賦值
a = int(input("請輸入數字1： ")) # 輸入 123
b = int(input("請輸入數字2： ")) # 輸入 456

print(type(a))  # <class 'int'>
print(type(b))  # <class 'int'>
```

## 格式化輸出

在Python3中，提供了簡潔的字串格式化語法，使用方式就是在字串的前方加上`f` 或 `F` 前綴字，接著在 `{}` 符號中，傳入**變數或運算式**，Python會將 `{}` 中的變數資料或運算結果帶出來。

```python
first_name = "Leo"
last_name ="Tam"
my_phone_num = 28781313

print("Hi, My name is " + first_name + " " + last_name + ", my phone number is " + str(my_phone_num))
# Hi, My name is Leo Tam, my phone numer is 28781313

# f-string
print(f"Hi, My name is {first_name} {last_name}, my phone number is {my_phone_num}")
# Hi, My name is Leo Tam, my phone numer is 28781313
```

### 格式化輸出變數的用法

```python
num1 = 12.345 
num2 = 456.789
print(f'{num1}')
print(f'{num2}')
```

#### 對齊
- `<` 靠左對齊 
- `>` 靠右對齊 (默認)
- `^` 置中對齊


```python
# 觀察
# 12.345  => 6個位元
# 456.789 => 7個位元

print(f'{num1:7}')
print(f'{num2:7}')
```

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202402280216877.png)

**補0**

```python
print(f'{num1:07}')
print(f'{num2:07}')
```

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202402280216982.png)

**精度(取小數點後 n 位)**

```python
print(f'{num1:.2}')
print(f'{num2:.1}')
```

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202402280219610.png)


# 邏輯判斷
迄今為止，我們寫的Python代碼都是一條一條語句順序執行，這種代碼結構通常稱之為順序結構。

然而僅有順序結構並不能解決所有的問題，比如我們設計一個游戲，游戲第一關的通關條件是玩家獲得1000分，那麼在完成本局游戲後，我們要根據玩家得到分數來決定究竟是進入第二關，還是告訴玩家“Game Over”，這裡就會產生兩個分支，而且這兩個分支只有一個會被執行。

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202402262114223.png)


## 流程控制
流程控制是學習python的重點之一，所謂流程控制是代表當有多行的程式碼時，我們可以有效的控制程式應該執行的順序和方向，先前章節的程式是由上而下一行一行執行，當學會流程控制後，程式執行將更有變化性。

### 單向選擇 (if)
使用方法
```python
if(條件): 
    若成立則執行語句
```

``` python
a = 15
b = 1

if(a > b): 
    print("a 大於 b")
```

### 雙向選擇 (if、else)
使用方法
```python
if(條件): 
    若成立則執行語句
else:
    若條件不成立則執行語句
```

``` python
a = 15
b = 1

if(a < b): 
    print("a 小於 b")
else: 
    print("a 大於 b")
```

### 多重選擇 (if、elif、else)
#### 情況1 : 若條件成立時則跳出 if 

使用方法：
```python
if(條件1): 
    若成立則執行語句
elif(條件2):
    若成立則執行語句
elif(條件3):
    若成立則執行語句
.
.
.
else:
    全部條件都不成立時執行
```

``` python
a = 15
b = 1

if(a < b): 
    print("a 小於 b")
elif(a > b): 
    print("a 大於 b")
else: 
    print("a 等於 b")
```

#### 情況2 : 就算條件成立也不會跳出 if，繼續判斷 
```python
if(條件1): 
    若成立則執行語句
if(條件2):
    若成立則執行語句
if(條件3):
    若成立則執行語句
.
.
.
else:
    全部條件都不成立時執行
```

``` python
a = 100

if(a > 0): 
    print("a 大於 0")
if(a > 10): 
    print("a 大於 10")
if(a > 99):  
    print("a 大於 99")
if(a > 100):   
    print("a 大於 100")
```
### 嵌套分支
當然根據實際開發的需要，分支結構是可以嵌套作多重。
```python
if(條件1): 
    if(條件2):
    若成立則執行語句
    else:
    若條件2不成立則執行語句

else:
    全部條件都不成立時執行
```

Python支持多種運算符，下表大致按照優先級從高到低的順序列出了所有的運算符，運算符的優先級指的是多個運算符同時出現時，先做什麼運算然後再做什麼運算。除了我們之前已經用過的賦值運算符和算術運算符，我們稍後會陸續講到其他運算符的使用。
    
## 練習1
用戶驗證：請用戶輸入Username、Password，判斷是否管理員帳戶登入若成功輸出"成功登入"，若不是則輸出"登錄失敗"

- 管理員：
    - Username : `admin`
    - Password : `123456`

## 練習2
百分制成績轉換為等級制成績
- 大於等於 90 分 -> Grade A
- 大於等於 80 分 -> Grade B
- 大於等於 70 分 -> Grade C
- 大於等於 60 分 -> Grade D
- 小於 60 分 -> Grade F

## 練習3
計算狗狗的年齡相對人類年齡是多少歲
公式：
- 如果狗狗 1 歲，相當於 14 的人類
- 如果狗狗 2 歲，相當於 22 的人類
- 2歲以後，則為 (狗狗歲數 - 2) * 5 + 22

# 功課 1
作業1 : 共 2 題
由於系統限制只能上傳 1 個檔案，您可以
1. 壓縮成 `.zip` `.rar` 繳交 
2. 把 2 個作業的程式碼寫在同1個py檔案中

[https://hamster.cpttm.org.mo/spaces/iG7O6rYBK4mfmZkG5Y-2FA/upload](https://hamster.cpttm.org.mo/spaces/iG7O6rYBK4mfmZkG5Y-2FA/upload)
## 題目 1： 計算BMI指數
請寫一個程式，提示使用者輸入他們的身高（ cm ）和體重（kg）然後計算並輸出他們的BMI指數。
$$BMI = \frac{體重(kg)}{身高^2(m)}$$

根據計算結果使用以下標準判斷BMI指數的範圍：
| BMI值 | 描述 |
| :--: | :--: | 
| 小於 18.5 | 體重過輕 | 
| 18.5 到 24.9 | 正常範圍 | 
| 25 到 29.9 | 超重 | 
| 大於等於 30 | 肥胖 |

> 提示：在計算BMI指數時，需要將身高從 cm 轉換為 m

## 題目２： 學生成績評級
請寫一個程式，提示使用者輸入 3 個科目的成績，然後根據以下標準進行評級和總評：

科目分數判斷：
- 每個科目的成績範圍為 0 到 100 分。
- 如果任一科目的成績低於 60 分，則該科目評級為「不及格」。

總評：
___
- 如果三個科目的平均成績低於 60 分，則總評為「不及格」。
- 如果三個科目的平均成績在 60 分（含）以上且小於 70 分，則總評為「及格」。
- 如果三個科目的平均成績在 70 分（含）以上且小於 80 分，則總評為「中等」。
- 如果三個科目的平均成績在 80 分（含）以上且小於 90 分，則總評為「優良」。
- 如果三個科目的平均成績在 90 分（含）以上，則總評為「優秀」。
