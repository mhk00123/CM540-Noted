# Lesson 3 - 邏輯判斷

**tags: `python`** **`CM-540`** **`Lesson3`**


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
