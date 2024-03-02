# Lesson 2 - 變數、變數類型

**tags: `python`** **`CM-540`** **`Lesson2`**

### 程式語言中的變量/變數是什麼?

```python
print("Hello World!")
```

觀察到程式碼的 Hello World 用了一對引號`" "`包起來，引號包起來的東西我們叫`字串 String`，是Python中的一種數據類型，目前這個字串是固定狀態的，俗稱hard-coding(寫死的)，即若我們如果需要輸出另外的文字，我們需要直接改變程式中的引號的內容，這顯然是不合理的，因此在這章我們引入變數的概念，令這個固定的內容可以隨著不同的需求，而動態作更改。

### 定義變數

**變數就是存放資料值的容器**，我們可以使用英文字母 + 數字，去表示去定義變數。

```python
a = 1
```

這里的意思是：

1. 把數字 `1` **放進** 物件容器當中
2. 指定該容器的名稱為 `a` (等於符號的作用)

* 這里的等於符號並不是指相等的意思，在大部份程式語言中，這個等於符號的意思是**給予/賦予**的意思 ![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img/2024/202402042342728.png)

#### 變數命名

按照Python官方的限制，變數的命名有以下限制：

* 英文字母：**a-z**、**A-Z** (變數區分大小寫)
* 數字：**0-9**
* 符號：只能使用**底線/下劃線** `_`
* **變數名稱不得以數字開頭**

```python
# 合法變數命名
a = 1
cpttm = 2
Cpttm = 3
LeOtam = 4
Leo_tam = 5
_LEotam = 6

# 不合法變數
1Leo = 7 # 以數字開頭
CM-540 = 8 # 包含非法符號破折號 - 
%m53$ = 9 # 包含非法符號
```

改寫 `HelloWorld.py`

```python
a = "Hello World"
print(a)
# Hello World

b = "CM-540"
print(b)
# CM-540

# 如果 a + b 呢?
print( a + b )
```

#### 變數命名規則

事實上對於電腦來說，變數名稱的好壞並不重要。 真正重要的好壞，是變數命名習慣將影響整個程式的可讀性及可維護性。

{% hint style="info" %}
因為變數是給人看的。
{% endhint %}

命名習慣的好壞可由以下2點判斷:

* 可讀性
* 一致性

**可讀性**

我們剛才的例子中，都是使用a、b、c....等作為變數名稱，實際上，隔了一段時間後再看回程式碼的話，我們很大概率會忘記這些變數的意思，若是面對更複雜的 function 或是整個大結構的程式，我們會很難讀懂程式的運作。

實務上，對於大型程式的變數，我們一般會把該變數的作用以英文方式作命名。

**一致性**

一致性是指必須要用相同的規則命名整個程式的變數，可以是合作的工程師口頭約定也可以是一份 Code Style 文字文件。

如果採用了駝峰式就必須一直使用駝峰式，如果將使用者名稱命名成userName 就不要在中途改成 accountName 或只剩下 user，維持整個工程代碼的命名一致性。

### 主流命名方式

#### Camel Case (駝峰式命名法)

第一個字母為小寫，之後每一個單字的開頭為大寫，不包含空格。例如:

* userName
* fileName

#### Snake Case 命名法

單字皆為小寫，單字以底線\_分離。例如:

* user\_name
* file\_name

#### Screaming Case 命名法

跟Snake Case類似，單字皆為全大寫，一般用於**常量**(後續會介紹)。例如:

* USER\_NAME
* FILE\_NAME

### Exercise

### 變數類型

Python 的內建型態主要分為以下幾種：

1. 整數(`int`)：1、100、-50
2. 浮點數(`float`)：3.14、2.0、-6.7
3. 字串(`string`)：用來表示文字，必須用單引號或雙引號括住，"Hello World"、 'Hello World'
4. 布林型態(`bool`) ：用來表示真或假，只有兩個值`True` 和 `False`

資料型態在程式中很重要，它們決定了資料的處理方式和運算規則，因此在撰寫程式時需要確保資料型態的一致性和適當使用。

#### 整數(integer)

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

#### 浮點數(float)

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

#### Boolean 布林

布林（英語：Boolean）是電腦科學中的**邏輯資料**類型，它是只有兩種值的原始類型，通常是

* 真 `True`
* 假 `False`

#### 字串(String)

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

**字元**

剛才我們說字串是**字元序列**，字元又是什麼？像是`字母`、`數字`、`符號`、`空格`或是`換行`都是字元，一個 a 是一個字元，一個空格也是一個字元，它是文書系統裡頭最小的單位。

**字串長度**

既然Python的字串是字元序，那麼，在這個序列中各個字元的位置、以及整個字串的長度，我們應如何計算呢?

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img/2024/202402062340466.png)

1. 在Python中，任何**序列**開端編號(Index)一定為 `0`
2. 每一字元皆佔 1 個長度

以`"Hello World!"`作例子，這個字串的長度為：**12**

**取得字元**

可以透過中括號`[ ]`取得任意字串中的字元

```python
str_1 = "Hello World!"

print(str_1[4]) # l

print(str_1[6]) # W
```

另外，在Python中，也可以**反向**取得字元 ![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img/2024/202402062348197.png)

```python
str_1 = "Hello World!"

print(str_1[-2]) # !

print(str_1[-6]) # W
```

**改變字串**

Python 字串是`不可變的 （inmmutable）`，你無法使用方法（Method）對字串進行修改，但可以透過指派一個新的值給變數，來達到修改的效果。也就是說，字串屬於`不可變的資料型態`。

```python
name = "Leo"

# 嘗試把 name[0] 改變為 N
# 系統顯示報錯
name[0] = "N"
```

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202402232325812.png)

因此若我們想改變字串中的內容，可以採用 `replace()` 函數

```python
name = "Leo"

# 把 L 改變為 N
name = name.replace("L","N")
print(name) # Neo
```

**字串相加**

如果要將兩個字串連接起來，在Python中使用 `+`

```python
first_name = "Leo"
last_name ="Tam"
my_phone_num = 28781313

print("Hi, My name is " + first_name + " " + last_name + ", my phone number is " + str(my_phone_num))
# Hi, My name is Leo Tam, my phone numer is 28781313
```

#### 檢查變量型態

可以使用 `type()` 函數去檢查該變量屬於甚麼型態

```python
a = 100
b = 12.345
c = "Hello, World"
d = True

print(type(a))    # <class 'int'>
print(type(b))    # <class 'float'>
print(type(c))    # <class 'str'>
print(type(d))    # <class 'bool'>
```

#### 強制轉型

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

#### 輸入及輸出

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

#### 格式化輸出

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

<<<<<<< Updated upstream
**對齊**
=======
#### 對齊
- `<` 靠左對齊 (默認)
- `>` 靠右對齊
- `^` 置中對齊
>>>>>>> Stashed changes

```python
# 觀察
# 12.345  => 6個位元
# 456.789 => 7個位元

print(f'{num1:7}')
print(f'{num2:7}')
```

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202402280216877.png)

**補0**

```python
print(f'{num1:07}')
print(f'{num2:07}')
```

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202402280216982.png)

**精度(取小數點後 n 位)**

```python
print(f'{num1:.2}')
print(f'{num2:.1}')
```

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202402280219610.png)

## 作業：CV模版

程式描述：只需輸入你的名字、出生年月日、性別、年齡，便可以生成一段固定格式的個人介紹。

* input :
  * 姓名：string
  * 出生年月日：string `XXXX-XX-XX (年-月-日)`
  * 姓別：string
  * 年齡：int
