# Lesson 3 - 邏輯判斷

**tags: `python`** **`CM-540`** **`Lesson3`**

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
    
## 練習1：
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
- 小於 60 分 -> Grade

## 練習3：
計算狗狗的年齡相對人類年齡是多少歲
公式：
- 如果狗狗 1 歲，相當於 14 的人類
- 如果狗狗 2 歲，相當於 22 的人類
- 2歲以後，則為 (狗狗歲數 - 2) * 5 + 22


## 循環/迴圈結構  
### 應用場景
我們在寫程序的時候，一定會遇到需要重復執行某條或某些指令的場景。例如要實現每隔1秒中在屏幕上打印一次“hello, world”並持續打印一個小時，我們肯定不能夠直接把print('hello, world')這句代碼寫3600遍，這裡同樣需要循環結構。

循環結構就是程序中控制某條或某些指令重復執行的結構。在Python中構造循環結構有兩種做法，一種是`for-in`循環，一種是`while`循環。

## for-in 循環/迴圈
如果明確知道**循環執行的次數**或者要對一個容器進行迭代（後面會講到），那麼我們推薦使用`for-in循環`。

### for-in 結構
```python
for 變量名 in 範圍: 
    執行語句(statements)
```

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

## 輸出 1-100
```python
for i in range(1,101): 
    print(i)
```

## 練習

如何輸出成以下的樣式的0-100 ?

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202402280207309.png)

```python
for i in range(1,101): 
    print(f'{i:3d}', end=" ")
    if(i%25==0):
        print("")
```

## While 循環/迴圈
While 循環用於在某條件下，循環執行某段程序

### While 結構
```python
while 判斷條件(condition)：
    執行語句(statements)
```

## 輸出 1-100
```python
# 一般在 While 迴圈中需要有一個變數去讓程式判斷是否條件立
# 一般這個變數需要先在迴圈外先宣告好
count = 1

while(count < 101): # 條件為 count < 101時"執行"
    print(f'Now, count = {count}')
    count = count + 1 # 條件需要在迴圈中有變化，否則變為無限迴圈
```

## 無限迴圈
相較於 for 迴圈，While 迴圈中含有讓程式判斷的條件，因此有機會出現**無限迴圈**，即迴圈條件永遠都成立，不會跳出。一般情況下我們可以按下鍵盤的 `Ctrl` + `c` 終止程序。但在正式開發程序中，我們必須避免出現無限迴圈，這會使服務端死機。


```python
count = 1

while(count < 101): # 條件為 count < 101時"執行"
    print(f'Now, count = {count}')
    count = count - 1 # count 這個變數會永遠 < 1，因此迴圈永遠不會終結
```

## continue 
在迴圈中，我們可能有部份執行語句會因應不同情況而不出現，此時可以用`continue`語句跳過，並執行下次迴圈。

### 輸出 1-10，跳過2,9
```python
# for in 版本
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


## break
**break** 即跳出迴圈的意思，程式當遇到特定條件時，執行 **break** 語句即會跳出迴圈。 

### 字串 cptTm，當遇到 `T` 時跳出   
```python
for letter in 'cptTm':
   if letter == 'T':
      break
   print ('當前字母為 :', letter)
```

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202402290132352.png)
