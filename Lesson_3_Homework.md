#  Lesson3 作業 詳解(共 3 題)

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

```python
# 1. 請使用者輸入身高(cm)、體重(kg)
height_cm = int(input("請使用者輸入身高(cm)："))
weight_kg = int(input("請使用者輸入體重(kg)："))

# 2. 令身高(cm) 轉為 (m) 
height_m = float(height_cm) / 100

if((weight_kg < 0) or (height_cm < 0)):
    print("輸入錯誤，請輸入大於 0 的數字")
    exit()

# 3. 計算BMI
bmi = (weight_kg / (height_m * height_m))
# bmi = (weight_kg / (height_m)**2)

print(f"您的 BMI 指數是：{bmi:.2f}")

if(bmi<18.5):
    print("屬於體重過輕")

elif((bmi >= 18.5) and (bmi <= 24.9)):
    print("屬於正常範圍")
    
elif((bmi >= 25) and (bmi <= 29.9)):
    print("屬於超重")

elif(bmi >= 30):
    print("屬於肥胖")

else:
    print("BMI計誤錯誤，請重新輸入！")
```

## 題目 2： 超級無敵開口中

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
flag = True

while(flag):
    print("------------------")
    
    # 1. 請用戶輸入
    # 由於我們需要判斷數字有"bye"，因此先透過 temp 變數接收
    temp = input(f"請輸入 {min} - {max} 的數字：")
    
    # 2. 判斷是否打了 bye
    # 輸入 bye
    if(temp == "bye"):
        print(f"結果是：{lucky_num}!")
        print("Bye Bye!")
        flag = False # 迴圈會跳出

    # 沒有輸入 bye
    else:          
        # 3. 轉換為 int 作下一階判斷
        user_input = int(temp)
    
        # 若輸入不正確，continue 重新輸入
        if( (user_input < min) or (user_input > max) ):
            print("### 輸入錯誤 ###")
            continue
        
        # 4. 比較
        if(user_input == lucky_num):
            print("### 恭喜估中了！！！ ###")
            flag = False # 迴圈會跳出

        elif(user_input > lucky_num):
            print("再小一點")
            max = user_input
        
        elif(user_input < lucky_num):
            print("再大一點")
            min = user_input
    
print("###### End ######")
```

## 題目 3： 三角型的9x9乘法表

請嘗試以迴圈輸出：

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202403110049230.png)

## 思路
上半部分
- 當 i = 1 時，j 執行 1 次(由1->1)
- 當 i = 2 時，j 執行 2 次(由1->2)
- 當 i = 3 時，j 執行 3 次(由1->3)
...
- 當 i = 9 時，j 執行 9 次(由1->9)

下半部分
- 當 i = 8 時，j 執行 8 次(由1->8)
- 當 i = 7 時，j 執行 7 次(由1->7)
- 當 i = 6 時，j 執行 6 次(由1->6)
- 

### While 迴圈版本
```python
i = 1
while(i <= 9):
    j = 1
    while(j <= i):
        print(f"{i}x{j}={i*j:<3}", end="")
        j = j + 1
    print()
    i = i + 1
    
i = 8
while(i >= 1):
    j = 1
    while(j <= i):
        print(f"{i}x{j}={i*j:<3}", end="")
        j = j + 1
    print()
    i = i - 1
    
```

## For 迴圈版本
```python
# 上半部份
for i in range(1, 10): # 1-9
    for j in range(1,10): # 1-9
        if(j>i):
            continue # 在這個內迴圈中，break和continue最終效果一樣
        print(f"{i}x{j}={i*j:<3}", end ="")
    print()

# 下半部份    
for i in range(8,0,-1): # 8-1 
    for j in range(1,9): # 1-8
        if(j>i):
            continue # 在這個內迴圈中，break和continue最終效果一樣
        print(f"{i}x{j}={i*j:<3}", end="")
    print()
```
