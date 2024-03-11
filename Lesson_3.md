# Lesson 3 - 邏輯判斷、循環結構

## Lesson 3

邏輯判斷、循環結構

**tags: `python`** **`CM-540`** **`Lesson3`**

## Slide

課件：[https://tinyurl.com/4d2em7er](https://tinyurl.com/4d2em7er)

### 循環/迴圈結構

#### 應用場景

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

#### 無限迴圈

相較於 for 迴圈，While 迴圈中含有讓程式判斷的條件，因此有機會出現**無限迴圈**，即迴圈條件永遠都成立，不會跳出。在正式開發程序中，我們必須避免出現無限迴圈，這會使服務端死機。

```python
count = 1

while(count < 101): # 條件為 count < 101時"執行"
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

### 巢狀迴圈

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
stu1_num = ""
stu1_class = ""

stu2_name = ""
stu2_num = ""
stu2_class = ""

stu3_name = ""
stu3_num = ""
stu3_class = ""
```

如果我要再記錄 10 個學生的更多信息 ?

這樣的寫法，需要非常多的變數。隨著人數，要記錄的東西愈多，變數就需要愈，這顯然是無必要的。

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
student1 = ["Leo Tam", "cpttm-01","一年級"]
student2 = ["Mary Lo", "cpttm-02","二年級"]
student3 = ["Daniel Chan", "cpttm-03","三年級"]
.
.
.
student10 = ["Thomas Tai", "cpttm-10", "二年級"]

student_list =[student1, student2, student3, …, student10]
```

### for-in 循環/迴圈

除了 While 迴圈外，For 迴圈也是在Python中十分常用的。兩者本質意義上十分相似，作用都是重覆執行語句。

但實際上還是有一些區別：

* While 循環條件是由我們定義，滿足一定條件下迴圈便會繼續執行
* For 循環是一種”遍歷”機制，用於遍歷`可迭代對象(iterable)`，例如列表(list)、字串(string)、元組(tuple)等。迴圈將依序處理可迭代對象中的每個元素，直到所有元素都被處理完畢。

如果明確知道**循環執行的次數**或者要對一個容器進行迭代，那麼我們推薦使用`for迴圈`。

#### for迴圈 結構

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

### 迴圈 - 跳過某一步 (continue)

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

#### 字串 cptTm，當遇到 `T` 時跳出

```python
for letter in 'cptTm':
   if letter == 'T':
      break
   print ('當前字母為 :', letter)
```

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202402290132352.png =300x400)


## 功課2

### 題目 1： 超級無敵開口中

奬門人節目內的超級無敵開口中， 玩法是電腦隨機抽出一個 1 - 100 之間的號碼作為幸運號碼，參加者輪流說出一個數字，電腦會根據答案和參加者的數字，將可選範圍縮窄，直到最後幸運號碼被估中為止。

要求：
* 系統提示：需要告知目標數字比目前估的數字大或細
* 若使用者輸入”bye”，則輸出答案和結束遊戲

> 由於目前還沒有教到導入模塊的部份，因此先提供隨機數生成方法

```python
# 生成隨機數的函數如下(隨機生成 1-100 的整數)
import random
lucky_num = random.randint(1, 100)

print(target)
```

### 題目 2： 三角型的9x9乘法表

請嘗試以迴圈輸出：

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202403110049230.png)
