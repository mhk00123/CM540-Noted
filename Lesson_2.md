戈大尸# Lesson 2
變數、資料型態、輸入輸出、邏輯判斷

**tags: `python`** **`CM-540`** **`Lesson2`**

# Slide
課件：[https://docs.google.com/presentation/d/1V65yCaEIEPAe7G4l96b3gdxwrjxu6e9AdiGx25um2YY/edit?usp=sharing](https://docs.google.com/presentation/d/1V65yCaEIEPAe7G4l96b3gdxwrjxu6e9AdiGx25um2YY/edit?usp=sharing)

# 作業：
## 題目 1： 計算BMI指數
[https://hamster.cpttm.org.mo/spaces/jiXtQg8wgwwUDCVPdKz4GA/upload](https://hamster.cpttm.org.mo/spaces/jiXtQg8wgwwUDCVPdKz4GA/upload)
請寫一個程式，提示使用者輸入他們的身高（ cm ）和體重（kg）然後計算並輸出他們的BMI指數。
* 提示：在計算BMI指數時，需要將身高從 cm 轉換為 m

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202502271842351.png)


根據計算結果使用以下標準判斷BMI指數的範圍：

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202502271841302.png)


## 題目 2： 學生成績評級

[https://hamster.cpttm.org.mo/spaces/rHPXTT_ONoMF5Z4iT5dDoQ/upload](https://hamster.cpttm.org.mo/spaces/rHPXTT_ONoMF5Z4iT5dDoQ/upload)

請寫一個程式，提示使用者輸入 3 個科目的成績，然後根據以下標準進行評級和總評：

### (1)科目分數判斷：
- 每個科目的成績範圍為 0 到 100 分。
- 如果任一科目的成績低於 60 分，則該科目評級為「不及格」。

### (2)總評：
- 如果三個科目的平均成績低於 60 分，則總評為「不及格」。
- 如果三個科目的平均成績在 60 分（含）以上且小於 70 分，則總評為「及格」。
- 如果三個科目的平均成績在 70 分（含）以上且小於 80 分，則總評為「中等」。
- 如果三個科目的平均成績在 80 分（含）以上且小於 90 分，則總評為「優良」。
- 如果三個科目的平均成績在 90 分（含）以上，則總評為「優秀」。

# 變量／變數
你可以把變數想像成一個 **容器**，用來存放資料，這些資料可以是`數字`、`文字`、或是其他類型的資訊。
變數就像是一個標籤，幫助我們記住和操作這些資料。

``` python
my_name = "Leo" 
```

- 等號右側稱作值(Value)、值可以是任何東西，例如：數字、文字、甚至是另一個變數、運算式......等。
- 等號左側稱作變數名稱，即標籤/標記，讓值(Value)在程式中變得有意義。
- 等號(=)，意思是賦予。

而這個過程，我們稱作宣告變數，**所有變數在使用前必須要先宣告才可以使用**。

# 註解
在 Python 中，我們都可以在程式碼任意位置加上註解，以 `# `號作記號，在註解後方的所有內容，均不會執行。
```python
# 我是註解
```

# Python 基本組成
- 基本資料型態: int、float、str、bool
- 儲存容器: list、tuple、set、dict
- 輸出與輸入: print()、input()
- 運算子、運算式：加減乘除、大小等於
- 流程控制(選擇性敘述): if、elif、else
- 重複執行的迴圈: for、while、switch
- 例外狀況處理: try except

# 變數類型、資料型態

Python 的內建型態主要分為以下幾種：

1. 整數(`int`)：1、100、-50
2. 浮點數(`float`)：3.14、2.0、-6.7
3. 字串(`string`)：用來表示文字，必須用單引號或雙引號括住，"Hello World"、 'Hello World'
4. 布林型態(`bool`) ：用來表示真或假，只有兩個值`True` 和 `False`

資料型態在程式中很重要，它們決定了資料的處理方式和運算規則，因此在撰寫程式時需要確保資料型態的一致性和適當使用。

## 整數(integer)

一般來說，所有沒有小數點的數字，我們都歸類為整數。在 Python2 裡，分`整數 int`跟`長整數 long`，而在 Python3 裡，不管多大的數字，都只會顯示`整數 int`，已經沒有`長整數 long`的概念了，但其他語言仍然還是有`長整數 long`的概念，所以我們還是需要了解一下。

長整數: 即大於等於2^64，一般要在定義變數時加上`L`作標記

正常情況下，整數是有取值範圍的：

* 在32位元的機器上，整數的位數為32位，取值的範圍為 -2^31 \~ 2^31-1 即 -2147483648 \~ 2147483648
* 在64位元的機器上，整數的位數為64位，取值的範圍為 -2^63 \~ 2^63-1 即 -9223372036854775808L \~ 9223372036854775807L

但由於Python3後統一使用長整數類型，不會存在溢出問題，即可以存放任意大小的數值不會出錯。

如果是其他語言的話，存超過限制的話，會發生錯誤的，而在Python裡，則會自動幫你做轉換。

```python
# 定義一個整數

# 隠式定義
a = 1

# 顯式定義
b = int(1)

c = 2**101
```

## 浮點數(float)

廣義上浮點數就是有小數點的數字，其實不完全正確，還有部份不常用的情況涉及計算機概論知識，礙於篇幅，我們這裡不展開討論，本課程中僅會出現含小數點的情況。

浮點數有兩種表示方式

1. 直接包含小數：`314.159`、 `314159.0`(含有.0也算是浮點數)
2. 小數 + E次冪(E標記是表示 10的冪數)：`52.3E4`即`523000.0`

```python
# 宣告一個浮點數

# 隠式宣告
a = 314.159
b = 314159.0
c = 52.3E4

# 顯式宣告
d = float(314.159)
```

## 數字計算 (加減乘除)
整數(int)和浮點數(float)之間可以進行運算
``` python
a = 10
b = 3

add = a + b       # 加法
minus = a - b     # 減法
multiply = a * b  # 乘法
divide = a / b    # 除法

print("加法結果：" + add)       # 輸出 13
print("減法結果：" + minus)     # 輸出 7
print("乘法結果：" + multiply)  # 輸出 30
print("除法結果：" + divide)    # 輸出 3.333...
# 除法結果必為浮點數 float
```

## Boolean 布林

布林（英語：Boolean）是電腦科學中的**邏輯資料**類型，它是只有兩種值的原始類型，Boolean型類一般是運算後的一個結果

* 真 `True`
* 假 `False`

``` python
a = 1
b = 10

result = (a > b)
print(result) # False

result = (b > a)
print(result) # True
```


**字元**
像是`字母`、`數字`、`符號`、`空格`或是`換行`都是字元，一個 a 是一個字元，一個空格也是一個字元，它是文書系統裡頭最小的單位。

## 字串(String)
字串由一串有順序的字元所組成，也屬於Python 序列(Sequence)的一種，稱為字元序列。字串**成對的引號**來呈現，`單引號`、`雙引號` 、`三個單引號`、`三個雙引號`都可以拿來表示字串。如果想表達文字，卻忘了使用引號，Python 會將你輸入的文字視為變數、數字或是保留字。

```python
# 正常字串宣告
str_1 = 'this'
str_2 = "is"
str_3 = '''a'''
str_4 = """string"""

# 如果想表達文字，卻忘了使用引號，Python 會將你輸入的文字視為變數、數字或是保留字。
temp_str = str_1
# temp_str = 'this'
```

### 字串有長度

既然Python的字串是字元序，那麼，在這個序列中各個字元的位置、以及整個字串的長度，我們應如何計算呢?

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img/2024/202402062340466.png)

1. 在Python中，任何**序列**開端編號(Index)一定為 `0`
2. 每一字元皆佔 1 個長度

以`"Hello World!"`作例子，這個字串的長度為：**12**

### 取得字元

可以透過中括號`[ ]`取得任意字串中的字元

```python
str_1 = "Hello World!"

print(str_1[4]) # o

print(str_1[6]) # W
```

另外，在Python中，也可以**反向**取得字元 

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img/2024/202402062348197.png)

```python
str_1 = "Hello World!"

print(str_1[-2]) # d

print(str_1[-6]) # W
```

### 改變字串

Python 字串是`不可變的 （inmmutable）`，你無法使用方法（Method）對字串進行修改，但可以透過指派一個新的值給變數，來達到修改的效果。也就是說，字串屬於`不可變的資料型態`。

```python
name = "Leo"

# 嘗試把 name[0] 改變為 N
# 系統顯示報錯
name[0] = "N"
```

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202402232325812.png)

因此若我們想改變字串中的內容，目前我們只能重新賦值

```python
name = "Leo"

# 把 L 改變為 N
# 重新賦值
name = "Neo"
print(name) # Neo
```

### 字串相加
如果要將兩個字串連接起來，在Python中使用 `+`
* 字串只可以和字串相加，不可以和數字相加，如有遇到非同類型相加只可以強制轉型

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

### 字串分割
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

## 檢查變量型態

可以使用 `type()` 函數去檢查該變量屬於甚麼型態

```python
var_a = 100
var_b = 12.345
var_c = "Hello, World"
var_d = True

print(type(var_a))    # <class 'int'>
print(type(var_b))    # <class 'float'>
print(type(var_c))    # <class 'str'>
print(type(var_d))    # <class 'bool'>
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
print(d) #12
```

### 字串相加轉型
剛才我們提及 `字串只可以和字串相加，不可以和數字相加，如有遇到非同類型相加只可以強制轉型`

```python
a = "今年是"
b = 2025
c = "年"

print(a + b + c) # Error
```

正確做法

```python
a = "今年是"
b = 2025
c = "年"

print(a + str(b) + c)
```

## 課堂練習
建立變數 ：name、sex、born_in(int)、age(int)，由屏幕輸出
> Hello 我是 Leo Tam，我是一個出生於 19xx 年出生的男性，今年 N 歲。

```python
name = "Leo Tam"
sex = "男性"
born_in = 1996
age = (2025 - born_in)

print("Hello 我是" + name + "，我是一個出生於" + str(born_in) + "年的" + sex + "性，今年" + str(age) + "歲")
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

## 課堂練習
修改剛才例子，把所有固定的變數，都變成由你輸入
建立變數 ：name、sex、born_in(int)、age(計出來)
可由用戶輸入：name、sex、bron_in

```python
name = input("請問你的名字是： ")
sex = input("請問你的性別是： ")
born_in = input("請問你的出生年份是： ")
age = (2025 - int(born_in))

print("Hello 我是" + name + "，我是一個出生於" + str(born_in) + "年的" + sex + "，今年" + str(age) + "歲")
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

print(f'{num1:15}') # 輸出字串共15個位元，不足自動填空格
print(f'{num2:15}')
```

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202502262200878.png)


#### 靠左對齊
```python
num1 = 12.345 
num2 = 456.789
print(f'{num1:<15}')
print(f'{num2:15}')
```

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202409101647014.png)


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

## 課堂練習
再修改剛才例子，把輸出的 print() 改以格式化輸出顯示
```python
name = input("請問你的名字是： ")
sex = input("請問你的性別是(男/女)： ")
born_in = input("請問你的出生年份是： ")
age = (2025 - int(born_in))

print("Hello 我是" + name + "，我是一個出生於" + str(born_in) + "年的" + sex + "，今年" + str(age) + "歲")

print(f"Hello 我是{name}，我是一個出生於{born_in}年的{sex}性 ，今年{age}歲。")
```



# 邏輯判斷
迄今為止，我們寫的Python代碼都是一條一條語句順序執行，這種代碼結構通常稱之為順序結構。

言而我們的實際流程中，必定有著非常多情況，需要按照不同的情況，輸出不同的結果。

## 流程控制
流程控制是學習python的重點之一，所謂流程控制是代表當有多行的程式碼時，我們可以有效的控制程式應該執行的順序和方向，先前章節的程式是由上而下一行一行執行，當學會流程控制後，程式執行將更有變化性。

流程控制就像做決定，根據不同的條件選擇不同的行動。例如：

## 例子
- 如果今天下雨，就帶傘；否則，就不帶傘。
- 如果成績大於 60 分，就及格；否則，就不及格。

在程式中，我們用 `if` 和 `else` 來實現這種決策邏輯。

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202402262114223.png)


## 單向選擇 (if)
使用方法
```python
if(條件): 
    若成立則執行語句
```

``` python
age = 18

if(age >= 18):
    print("你已經成年了！")
```

## 雙向選擇 (if、else)
`else` 用來處理 if 條件不成立（False）的情況：

使用方法
```python
if(條件): 
    若成立則執行語句
else:
    若條件不成立則執行語句
```

``` python
age = 16

if(age >= 18):
    print("你已經成年了！")
else:
    print("你還未成年！")
```

## 多重選擇 (if、elif、else)
如果有多個條件需要檢查，可以用 `elif` (else if 的縮寫)：

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

## 嵌套分支

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

``` python
age = 20
has_license = True

if(age >= 18):
    if(has_license == True):
        print("你可以開車！")
    else:
        print("你還不能開車，因為沒有駕照！")
else:
    print("你還不能開車！")
```
- 如果 age 大於或等於 18 且 has_license 為 True，輸出：你可以開車！。
- 如果 age 大於或等於 18 但 has_license 為 False，輸出：你還不能開車，因為沒有駕照！。
- 如果 age 小於 18，輸出：你還不能開車！。

## and(與)、or(或)、xor(非)
當出現多個條件需要`同時`判斷時，我們可以使用`and`、`or`、`xor`
- and : 所有結果需要同時為True，才是True
- or：只需有 1 個結果為True，就是True
- xor：當兩個參數相同時為False、兩個參數不同時為True (不常用)

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202405132331072.png)
    
## 練習1
用戶驗證：請用戶輸入Username、Password，判斷是否管理員帳戶登入若成功輸出"成功登入"，若不是則輸出"登錄失敗"

- 管理員：
    - Username : `admin`
    - Password : `123456`

## 練習2
計算狗狗的年齡相對人類年齡是多少歲
公式：
- 如果狗狗 1 歲，相當於 人類的 14 歲
- 如果狗狗 2 歲，相當於 人類的 22 歲
- 狗狗 2 歲以後，相當於人類歲數則為 `(狗狗歲數 - 2) * 5 + 22`