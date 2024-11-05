# Lesson 3 - 邏輯判斷、循環結構

邏輯判斷、循環結構

**tags: `python`** **`CM-540`** **`Lesson3`**

# Slide

課件：[https://docs.google.com/presentation/d/1qh0-se2MSjAxyeE6rOPOm6hnW7SK_aeh6He7Su8Vb04/edit?usp=sharing](https://docs.google.com/presentation/d/1qh0-se2MSjAxyeE6rOPOm6hnW7SK_aeh6He7Su8Vb04/edit?usp=sharing)


## 題目： 超級無敵開口中

繳交網址：[https://hamster.cpttm.org.mo/spaces/CfjcgaM34-x2Uz0X1eEvTQ/upload](https://hamster.cpttm.org.mo/spaces/CfjcgaM34-x2Uz0X1eEvTQ/upload)

奬門人節目內的超級無敵開口中， 玩法是電腦隨機抽出一個 1 - 100 之間的號碼作為幸運號碼，參加者輪流說出一個數字，電腦會根據答案和參加者的數字，將可選範圍縮窄，直到最後幸運號碼被估中為止。

要求：
* 系統提示：需要告知目標數字比目前估的數字大或細
* 若使用者輸入”bye”，則輸出答案和結束遊戲

> 由於目前還沒有教到導入模塊的部份，因此先提供隨機數生成方法

```python
# 生成隨機數的函數如下(隨機生成 1-100 的整數)
import random
lucky_num = random.randint(1, 100)

print(lucky_num)
```

## 題目 2： 三角型的9x9乘法表

繳交網址：[https://hamster.cpttm.org.mo/spaces/9PiKSC39JqA1F8tvSzmh-A/upload](https://hamster.cpttm.org.mo/spaces/9PiKSC39JqA1F8tvSzmh-A/upload)

請嘗試以迴圈輸出：

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202403110049230.png)


# 運算子
| 運算符 | 描述 |
| :--: | :--: |
| `**` | 次方 3**4 = 3 x 3 x 3 x 3 = 81 |
| `*` `/` `%` | 乘、除、取餘數 |
| `+` `-` | 加、减 |
| `<=` `<` `>` `>=` | 小於等於、小於、大於、大於等於 |
| `+` `-` | 加、减 |
| `==` `!=` | 等於、不等於 |
| `is`  `is not` |  |
| `in` `not in` |  |
| `not` `or` `and` | |

# 邏輯判斷
迄今為止，我們寫的Python代碼都是一條一條語句順序執行，這種代碼結構通常稱之為順序結構。

然而僅有順序結構並不能解決所有的問題，比如我們設計一個游戲，游戲第一關的通關條件是玩家獲得1000分，那麼在完成本局游戲後，我們要根據玩家得到分數來決定究竟是進入第二關，還是告訴玩家“Game Over”，這裡就會產生兩個分支，而且這兩個分支只有一個會被執行。

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202402262114223.png)

## and(與)、or(或)、xor(非)
- and : 需要同時為True，才是True
- or：只需有 1 個為True，就是True
- xor：當兩個參數相同時為False、兩個參數不同時為True (不常用)

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202405132331072.png)

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

Python支持多種運算符，下表大致按照優先級從高到低的順序列出了所有的運算符，運算符的優先級指的是多個運算符同時出現時，先做什麼運算然後再做什麼運算。除了我們之前已經用過的賦值運算符和算術運算符，我們稍後會陸續講到其他運算符的使用。

## 練習1
請用戶輸入一個整數數字，判斷屬於正數、負數、還是0 ?

### 思路
1. 令用戶輸入一個數字
2. 轉換輸入為 int
3. 判斷該數字是否等於 0
- 是：輸出 "輸入的是0"
- 不是：
-- 大於 0 : 輸出"正數"
-- 小於 0 : 輸出"負數"

```python
user_input = int(input("請輸入一個整數"))

if(user_input == 0):
    print("你輸入的是0")

else:
    if(user_input > 0):
        print("你輸入的是正數")
    
    else:
        print("你輸入的是負數")
```

## 練習2
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
print(“Hello World”)
print(“Hello World”)
print(“Hello World”)
print(“Hello World”)
print(“Hello World”)
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

#### 練習1：輸出 1-100 的所有偶數。

```python
# 一般在 While 迴圈中需要有一個變數去讓程式判斷是否條件立
# 一般這個變數需要先在迴圈外先宣告好
count = 1

while(count < 101): # 條件為 count < 101時"執行"
    if(count % 2 == 0):
        print(f"{count}", end = " ")
    count = count + 1 # 條件需要在迴圈中有變化，否則變為無限迴圈
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
   if letter == 'T':
      break
   print ('當前字母為 :', letter)
```

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202402290132352.png)


