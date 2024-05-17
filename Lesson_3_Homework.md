#  Lesson3 作業 詳解(共 3 題)

繳交截止：5月17日23:59

繳交網址：[https://hamster.cpttm.org.mo/spaces/P4-DooqN3wJafULUDdqMKw/upload](https://hamster.cpttm.org.mo/spaces/P4-DooqN3wJafULUDdqMKw/upload)

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

## 題目 3： 三角型的9x9乘法表

請嘗試以迴圈輸出：

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202403110049230.png)

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
