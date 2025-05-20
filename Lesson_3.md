# Lesson 3 - 邏輯判斷、循環結構

邏輯判斷、循環結構

**tags: `python`** **`CM-540`** **`Lesson3`**

# Slide

課件：[https://docs.google.com/presentation/d/1qh0-se2MSjAxyeE6rOPOm6hnW7SK_aeh6He7Su8Vb04/edit?usp=sharing](https://docs.google.com/presentation/d/1qh0-se2MSjAxyeE6rOPOm6hnW7SK_aeh6He7Su8Vb04/edit?usp=sharing)

# 作業：
截止時間：2025年5月25日 23:59

{% hint style="info" %}
# 題目 1： 學生成績評級
[https://hamster.cpttm.org.mo/spaces/zJSnedsakiRQAL6E3Iq1YA/upload](https://hamster.cpttm.org.mo/spaces/zJSnedsakiRQAL6E3Iq1YA/upload)

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

{% endhint %}

{% hint style="info" %}
# 題目 2： 超級無敵開口中

繳交網址：[https://hamster.cpttm.org.mo/spaces/hH39vKqdQFC09C3ha3D-LQ/upload](https://hamster.cpttm.org.mo/spaces/hH39vKqdQFC09C3ha3D-LQ/upload)

奬門人節目內的超級無敵開口中， 玩法是電腦隨機抽出一個 1 - 100 之間的號碼作為幸運號碼，參加者輪流說出一個數字，電腦會根據答案和參加者的數字，將可選範圍縮窄，直到最後幸運號碼被估中為止。

要求：
* 系統提示：需要告知目標數字比目前估的數字大或細
* 若使用者輸入`bye`，則輸出答案和結束遊戲

> 由於目前還沒有教到導入模塊的部份，因此先提供隨機數生成方法

```python
# 生成隨機數的函數如下(隨機生成 1-100 的整數)
import random

lucky_num = random.randint(1, 100) # 變數 lucky_num 為一個1-100的int隨機數 

print(lucky_num)
```
{% endhint %}

{% hint style="info" %}
# 題目 3： 三角型的9x9乘法表(選做)

繳交網址：[https://hamster.cpttm.org.mo/spaces/ZSDkaA1BgsBJzo364fC8qw/upload](https://hamster.cpttm.org.mo/spaces/ZSDkaA1BgsBJzo364fC8qw/upload)

請嘗試以迴圈輸出：

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202403110049230.png)

{% endhint %}


# 邏輯判斷
迄今為止，我們寫的Python代碼都是一條一條語句順序執行，這種代碼結構通常稱之為順序結構。

言而我們的實際流程中，必定有著非常多情況，需要按照不同的情況，輸出不同的結果。

## 數字比較
```python
1 > 2      # False

100 > 99   # True

100 <= 99  # False

100 == 99  # False

100 == 100 # True

100 > 100  # False

100 >= 100 # True
```

## 文字比較
字串比較是根據字元的順序進行的。通常情況下，字串的比較是以字典順序進行的，也就是根據字元的Unicode碼值進行比較。
另外，字串比較是區分大小寫的。這意味著大寫字母在比較時會被認為是小於相同字元的小寫字母。例如，字串"apple"會被認為是大於字串"Apple"。
```python
a = "Leo"
b = "Leo"
c = "leo"

a == b # True

a == c # False

c > b  # True
```

# 流程控制
流程控制是學習python的重點之一，所謂流程控制是代表當有多行的程式碼時，我們可以有效的控制程式應該執行的順序和方向，先前章節的程式是由上而下一行一行執行，當學會流程控制後，程式執行將更有變化性。

流程控制就像做決定，根據不同的條件選擇不同的行動。例如：

## 例子
- 如果今天下雨，就帶傘；否則，就不帶傘。
- 如果成績大於 60 分，就及格；否則，就不及格。

在程式中，我們用 `if` 和 `else`、`elif` 來實現這種決策邏輯。


## 單向選擇 (if)
使用方法
```python
if(條件): 
    若成立則執行語句
```

``` python
if( weather == "raining" ):
    print("記得帶雨傘")
```

### Python 特性
實際操作上，條件最終只要不為 `0`(int) 或 `False`，語句都會被執行。
由於文字不是 0 ，因此直接把文字放進條件判斷，結果是 `True`。

```python
if("I am a good boy"): # True
    print("Leo Tam")
```

### 單向選的獨立性
單向選擇的每次判斷(每一次if)均獨立
```python
 a = 100

if(a > 0): 
    print("a 大於 0") # true 輸出
if(a > 10): 
    print("a 大於 10") # true 輸出
if(a > 99):  
    print("a 大於 99") # true 輸出
if(a > 100):   
    print("a 大於 100") # False 不輸出

# 以上全部滿足條件的 if 都會有輸出
```

## 雙向選擇 (if、else)
`else` 用來處理 if 條件不成立（False）的情況(只會有一個結果)：

使用方法
```python
if(條件): 
    若成立則執行語句
else:
    若條件不成立則執行語句
```

``` python
# 如果今天下雨，就帶傘；否則，就不帶傘。
 
if(weather == "raining"): 
    print("記得帶雨傘")

else: 
    print("不用帶雨傘")
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

```python
# 如果今天下雨，就帶傘；
# 如果今天出太陽，就都帶傘；

# 使用 if、elif、else 來判斷該帶什麼
if (weather == "raining"):
    print("今天下雨，帶傘。")

elif (weather == "sunny"):
    print("今天出太陽，帶傘。")

else:
    print("今天天氣普通，不用帶傘。")
```

# 嵌套分支
當然根據實際開發的需要，分支結構是可以嵌套作多重。
我們使用巢狀的 if 語句來進一步細分條件，若 if  的情況大於 2 個時，可以繼續細分。

```python
if(條件1): 
    if(條件2):
    若成立則執行語句 # 此處的意思是若條件1成立 且 條件2也成立
    else:
    若條件2不成立則執行語句

else:
    全部條件都不成立時執行
```

```python
weather = "下雨"  # 可以改為 "出太陽" 或其他
temperature = 20  # 可以改為其他溫度值

# 使用嵌套分支來判斷
if(weather == "下雨"):
    if(temperature < 15):
        print("今天下雨且溫度低於 15°C，帶傘和外套。")
    else:
        print("今天下雨，帶傘。")

elif(weather == "出太陽") :
    if(temperature < 15):
        print("今天出太陽且溫度低於 15°C，帶傘、防曬霜以及外套。")
    else:
        print("今天出太陽，帶傘。")
else:
    print("今天天氣普通，什麼都不用帶。")

```


# and(與)、or(或)、xor(非)
and 和 or 是 邏輯運算符，用於組合多個條件，在條件判斷中實現更複雜的邏輯。

當出現多個條件需要`同時`判斷時，我們可以使用`and`、`or`、`xor`
- and : 需要同時為True，結果才是True
- or：只需有 1 個為True，結果就是True
- xor：當兩個參數相同時為False、兩個參數不同時為True (不常用)

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202405132331072.png)

## and(與)
用於檢查 **所有條件是否同時成立**。
結果：只有當所有條件都為 True 時，and 的結果才是 True；否則結果為 False

```python
x = 5

if((x > 0) and (x < 10)):
    print("x 是一個介於 0 和 10 之間的正數。")
```

## or(或)
用於檢查 **至少有一個條件是否成立**。

結果：
只要有一個條件為 True，or 的結果就是 True；
只有當所有條件都為 False 時，結果才是 False

```python
y = -3
if((y < 0) or (y > 100)):
    print("y 是小於 0 或大於 100 的數。")

```

### 練習2
用戶驗證：請用戶輸入管理員的Username、Password，判斷是否管理員帳戶登入
- 若成功顯示"成功登入"
- 若用戶名錯誤、則顯示”用戶名錯誤”
- 若用戶名正確，密碼錯，則顯示”密碼錯誤”
- 若不是則輸出"登入失敗"

管理員帳戶密碼：
Username : admin

Password : admin12345

### 思路
1. 定義正確的登入帳號、密碼
2. 由用戶輸入帳號、密碼
3. 確定輸入為 String 
4. 判斷
- (帳號是否與預設帳號相同) 且 (密碼是否與預設帳號密碼) 
-- 條件1 : 帳號密碼正確：登入成功
-- 條件2 : 帳號錯誤 : "用戶名錯誤"
-- 條件2 : 帳號正確、密碼錯誤 : "密碼錯誤"
- 否：
-- "登入失敗"

```python
# 1. 定義正確的登入帳號、密碼
admin_username = "Admin"
admin_password = "Admin12345"

# 2、3. 由用戶輸入帳號、密碼
# 由於使用 input() 得到的值類型一定是 String，因此不需要進行強轉
input_username = input("請輸入用戶名：")
input_password = input("請輸入密碼：")

# 4. 判斷

# 4.1 若成功顯示"成功登入"
if((input_username == admin_username) and (input_password == admin_password)):
    print("登入成功")
    
# 4.2 若用戶名錯誤、則顯示”用戶名錯誤”
elif((input_username != admin_username)):
    print("用戶名錯誤")

# 4.3 若用戶名正確，密碼錯，則顯示”密碼錯誤”
elif((input_username == admin_username) and (input_password != admin_password)):
    print("密碼錯誤")

# 4.4 若不是則輸出"登入失敗"
else:
    print("登入失敗")
```


# 循環結構
### 應用場景

我們在寫程序的時候，一定會遇到需要重復執行某條或某些指令的場景。例如要實現每隔1秒中在屏幕上打印一次“hello, world”並持續打印一個小時，我們肯定不能夠直接把print('hello, world')這句代碼寫3600遍，這裡同樣需要循環結構。

```python
print("Hello World")
print("Hello World")
print("Hello World")
print("Hello World")
.
.
.
```

這顯然是不合理的，因此我們在這裡引入循環結構`迴圈`的概念，循環結構就是程序中控制某條或某些指令重復執行的結構。

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202403110014295.png)

#### 在Python中構造循環結構有兩種做法：

1. 一種是 while 循環
2. 一種是 for 循環

```python
for i in range(1,101): 
    print(f"{i:3d}", end=" ")
    if(i%25==0):
        print("")
```

## While 循環/迴圈

While 循環用於在某條件下，循環執行某段程序

### While 結構

```python
外變數

while(條件):
    條件滿足時，做的事1
    條件滿足時，做的事2
    條件滿足時，做的事3
    ………
    外變數 +-*/
```

#### While循環中的`條件`

在While迴圈中，條件是優先判斷的，先判斷條件再執行語句。 因此條件中，沒有加入終止條件的變數，迴圈會一直執行下去，變成無限迴圈。

## 無限迴圈

相較於 for 迴圈，While 迴圈中含有讓程式判斷的條件，因此有機會出現**無限迴圈**，即迴圈條件永遠都成立，不會跳出。在正式開發程序中，我們必須避免出現無限迴圈，這會使服務端死機。

```python
count = 1

while(count < 11): # 條件為 count < 10時"執行"
    print(f"Now, count = {count}")
    count = count - 1 # count 這個變數會永遠 < 1，因此迴圈永遠不會終結
```

{% hint style="info" %}
當我們遇到無限迴圈時，可以按鍵盤中的 `Ctrl` + `c`強制終止程式。
{% endhint %}

#### 練習1：輸出 1、3、5、7、...、93、95、97、99。。

```python
# 一般在 While 迴圈中需要有一個變數去讓程式判斷是否條件立
# 一般這個變數需要先在迴圈外先宣告好
num = 1

while(num < 100): # 條件為 count < 100 時"執行"
    print(f"{num}", end=" ")
    num = num + 2
```

#### 練習2：求1 - 100的和

```python
count = 1 
sum = 0 # 設置變數 count 記錄累加

while(count < 101):
    sum = sum + count 
    count = count + 1 

print(sum)
```

## 巢狀迴圈

巢狀迴圈並非新的程式結構，只是迴圈範圍內又有迴圈，巢狀迴圈可以有好幾層，巢狀迴圈與單層迴圈運作原理相同，從外層迴圈來看，內層迴圈指示外層迴圈內的動作，因此外層迴圈作用一次，內迴圈需要執行完畢。

```python
外變數 1
外變數 2

while(條件1):
    while(條件2):

```

#### 練習

輸出如下

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202403110026778.png)

```python
# 習慣上 外變數我們用 i, j
i = 1
j = 1

while(i<3):
    print(f"第{i}行：", end = " ")

    j = 1 # 每次內循環完成後，需要把 j 的值重置
    while(j<10):
        print(f"{i}.{j}", end =" ")
        j = j + 1

    print("換行")
    i = i + 1
```

#### 練習 - 9x9乘法表

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202403110029464.png)

```python
i = 1
while (i <= 9):
    j = 1
    while (j <= 9):
        result = i * j
        print(f"{i}x{j}={result:<3}",end=" ")
        j = j + 1
    print()
    i = i + 1
```

### 格式化輸出(f-string)變數的用法

```python
num_A = 12.345 
num_B = 456.789
print(f'{num_A}')
print(f'{num_B}')
```

#### 對齊
- `<` 靠左對齊 
- `>` 靠右對齊 (默認)
- `^` 置中對齊


```python
# 觀察
# 12.345  => 6個位元
# 456.789 => 7個位元
num_A = 12.345 
num_B = 456.789
print(f'{num_A:15}') # 輸出字串共15個位元，不足自動填空格
print(f'{num_B:15}')
print(f'{num_B:<15})
```

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202502262200878.png)


#### 靠左對齊
```python
num_A = 12.345 
num_B = 456.789
print(f'{num_A:<15}')
print(f'{num_B:15}')
```

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202409101647014.png)


**補0**

```python
num_A = 12.345 
num_B = 456.789
print(f'{num_A:07}')
print(f'{num_B:07}')
```

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202402280216982.png)

**精度(取小數點後 n 位)**
注意，格式輸出僅改變輸出到屏幕的狀態，並非改變變數的值。
在對應的位置加上 `:.nf`
```python
num_A = 12.345 
num_B = 456.789
print(f'{num_A:.2f}')
print(f'{num_B:.1f}')
```

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202402280219610.png)

## 儲存容器

思考一個問題：如果我要記錄 3 個學生的信息 包含：姓名、學號、年級

```python
stu1_name = ""

stu2_name = ""

stu3_name = ""

stu4_name = ""

stu5_name = ""
```

如果我要再記錄 10 個學生的更多信息 ? 100 個?

這樣的寫法，需要非常多的變數。隨著人數，要記錄的東西愈多，變數就需要愈多，這顯然是無必要的。

因此我們先行引入**儲存容器**的概念

### 儲存容器 - List(列表、陣列)

List 是 Python 中最基本的數據結構。List 中的每個值都有對應的位置值，稱之為索引(index)，第一個索引是 0，第二個索引是 1，依此類推。

#### 定義一個 List，使用\[ ]

```python
list_exp = ["red", "green", "blue", "yellow", "white", "black"]

print(list_exp[0]) # red

print(list_exp[-1]) # black
```

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202403110034722.png)

#### List 的特性

1. List 是有順序的，會按照 index 由0、1、2、...下去
2. 存取方式與 string 一樣，使用 `變數名[index]`進行元素存取
3. 列表的元素**不需要具有相同的類型**
4. List 中的元素可以作新增、修改、刪除(後續再詳講)
5. List 是一個**迭代對象(iterable)**

```python
# 這個是合法的 List
list_exp = [1 , "green", True] 
```

回歸剛才的問題，如果我要再記錄 10 個學生的更多信息，我們可以這樣處理。

```python
student_name = ["Leo Tam", "Mary", "John", ... ,"cpttm"]
```

# for-in 循環/迴圈

除了 While 迴圈外，For 迴圈也是在Python中十分常用的。兩者本質意義上十分相似，作用都是重覆執行語句。

但實際上還是有一些區別：

* While 循環條件是由我們定義，滿足一定條件下迴圈便會繼續執行
* For 循環是一種”遍歷”機制，用於遍歷`可迭代對象(iterable)`，例如列表(list)、字串(string)、元組(tuple)等。迴圈將依序處理可迭代對象中的每個元素，直到所有元素都被處理完畢。

如果明確知道**循環執行的次數**或者要對一個容器進行迭代，那麼我們推薦使用`for迴圈`。

### for迴圈 結構

```python
for 臨時變數 in 可迭代對象:
    執行語句
```

* 臨時變數用於存放每一個可迭代對象
* 較常用於 for 迴圈的可迭代對象 - range()

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202403110040045.png)

#### range(start, stop, step)

範圍可以透過`range()`函數生成，可以接收3個參數(start, stop, step)，取頭不取尾：

```python
# 基本用法
range(10)    # 0,1,2,3,4,5,6,7,8,9
range(1, 10) # 1,2,3,4,5,6,7,8,9

# 加上step
range(0, 10, 2) # 0,2,4,6,8 
range(0, 10, 3) # 0,3,6,9

# 負數
range(0, -10) # 錯誤，range默認只會累加
range(0, -10, -1) # 0,-1,-2,-3...-9
```

### 練習1：輸出 1-100

```python
for i in range(1,101): 
    print(f"{i:3}")
```

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202402280207309.png)

### 練習2：統計

定義一個內容：`Today is monday, I go to school by bus.` 統計一下有幾個字母 ”o” ?

```python
temp_str = "Today is monday, I go to school by bus."

count = 0

for i in temp_str:
    if(i == "o"):
        count = count + 1
        
print(count)
```

### 練習3：9x9 乘法表

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202403110044234.png)

```python
i = 1
while (i <= 9):
    j = 1
    while (j <= 9):
        result = i * j
        print(f"{i}x{j}={result:<3}",end=" ")
        j = j + 1
    print()
    i = i + 1
```

## 迴圈 - 跳過某一步 (continue)

在迴圈中，我們可能有部份執行語句會因應不同情況而不出現，此時可以用`continue`語句，由檢測到continue關鍵字起跳過本次循環，直接進入下一次循環。

#### 輸出 1-10，跳過2,9

```python
# for 版本
for i in range(1,11): 
    if(i==2) or (i==9):
        continue
    print(i)

# while 版本
count = 1
while(count <= 10):
    if(count == 2 or count == 9):
        count = count + 1
        continue
    print(count)
    count = count + 1
```

### 迴圈 - 跳出迴圈 (break)

**break** 即跳出迴圈的意思，程式當遇到特定條件時，執行 **break** 語句即會跳出迴圈。

## 字串 cptTm，當遇到 `T` 時跳出

```python
for letter in 'cptTm':
   if(letter == 'T'):
      break
   print ('當前字母為 :', letter)
```

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202402290132352.png)
