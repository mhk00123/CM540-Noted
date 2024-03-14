# Lesson_3_Homework

## 功課2
作業2 : 共 2 題
由於系統限制只能上傳 1 個檔案，您可以
1. 壓縮成 `.zip` `.rar` 繳交 
2. 把 2 個作業的程式碼寫在同1個py檔案中

[https://tinyurl.com/msx9wect](https://tinyurl.com/msx9wect)

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

print(lucky_num)
```

```python
# 生成隨機數的函數如下(隨機生成 1-100 的整數)
import random

print("###### Game Start ######")

# 取得 luncky number
lucky_num = random.randint(1, 100)

# 測試輸出答案
print(lucky_num)

# 需要 2 個變數記錄區間
min = 1
max = 100

while(True):
    print("------------------")
    
    # 1. 請用戶輸入
    # 由於我們需要判斷數字有"bye"，因此先透過 temp 變數接收
    temp = input(f"請輸入 {min} - {max} 的數字：")
    
    # 2. 判斷是否打了 bye
    if(temp == "bye"):
        print("Bye Bye!")
        break
    
    # 3. 若沒有則轉換為 int 作下一階判斷
    user_input = int(temp)
 
    # 若輸入不正確
    if( (user_input > max) or (user_input < min) ):
        print("### 輸入錯誤 ###")
        continue
    
    # 4. 比較
    if(user_input == lucky_num):
        print("### 恭喜估中了！！！ ###")
        break

    elif(user_input > lucky_num):
        print("再小一點")
        max = user_input
    
    elif(user_input < lucky_num):
        print("再大一點")
        min = user_input
    
print("###### End ######")
```


### 題目 2： 三角型的9x9乘法表

請嘗試以迴圈輸出：

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202403110049230.png)

```python
# 上半部份
for i in range(1, 10):
    for j in range(1,10):
        if(j>i):
            continue # 在這個內迴圈中，break和continue最終效果一樣
        print(f"{i}x{j}={i*j:<3}", end ="")
    print()

# 下半部份    
for i in range(8,0,-1):
    for j in range(1,10):
        if(j>i):
            continue # 在這個內迴圈中，break和continue最終效果一樣
        print(f"{i}x{j}={i*j:<3}", end="")
    print()
```
