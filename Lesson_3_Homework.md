#  Lesson3 作業 詳解(共 3 題)

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

```python
# ''''''''''''''''''''''''''''''
# 1. 用戶輸入三個科目的分數
# 2. 判斷各科目是否不及格
# 3. 計算平均分數
# 4. 根據平均分數進行總評判斷
# 5. 輸出總評結果
# ''''''''''''''''''''''''''''''

# 1. 輸入三個科目的分數
score_1 = int(input("請輸入第 1 科成績："))
score_2 = int(input("請輸入第 2 科成績："))
score_3 = int(input("請輸入第 3 科成績："))

# 2. 判斷各科目是否不及格
if (score_1 < 60):
    print("第 1 科：不及格")
if (score_2 < 60):
    print("第 2 科：不及格")
if (score_3 < 60):
    print("第 3 科：不及格")

# 3. 計算平均分數
average_score = (score_1 + score_2 + score_3) / 3

# 4. 根據平均分數進行總評判斷
if(average_score >= 90):
    total_rating = "優秀"
elif(average_score >= 80) and (average_score < 90):
    total_rating = "優良"
elif(average_score >= 70) and (average_score < 80):
    total_rating = "中等"
elif(average_score >= 60) and (average_score < 70):
    total_rating = "及格"
elif(average_score < 60):
    total_rating = "不及格"
else:
    total_rating = "輸入錯誤"

# 5. 輸出總評結果
print(f"平均分數：{average_score:.2f}，總評結果：{total_rating}")
```
---
{% hint style="info" %}
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
# ''''''''''''''''''''''''''''''
# 1. 導入 random 模組
# 2. (定義變數)取得 luncky number、隨機生成 1-100 的整數
# 3. (定義變數)生成記錄區間，上界及下界，迴圈控制變量
# 4. 遊戲開始
# 5. 請用戶輸入
# 6. 優先判斷是否打了 bye
# 7. 若沒有輸入 bye、轉換為 int 作下一階判斷
# 8. 用戶輸入的數字比較上下界
# ''''''''''''''''''''''''''''''

# 1. 導入 random 模組
import random 

print("###### Game Start ######")

# 2. 取得 luncky number 
# random.randint(1, 100) 會隨機生成 1-100 的整數
lucky_num = random.randint(1, 100)

# 測試輸出答案
print(lucky_num)

# 3. 生成記錄區間，上界及下界，控制變量
min = 1       # min 是用來控制用戶輸入的下界範圍
max = 100     # max 是用來控制用戶輸入的上界範圍
flag = True   # flag 是用來控制迴圈的變量

while(flag):
    print("------------------")
    
    # 5. 請用戶輸入
    # 由於我們需要優先判斷數字有"bye"，因此先透過 temp 變數接收
    temp = input(f"請輸入 {min} - {max} 的數字：")
    
    # 6. 判斷是否打了 bye
    if(temp == "bye"):     # 判斷輸入的類型是否為字串
        print("### Bye Bye ###")
        flag = False       # 迴圈會跳出
        
    # 若沒有輸入 bye
    else:          
        # 7. 轉換為 int 作下一階判斷
        user_input = int(temp)
    
        # 若輸入不正確，continue 重新輸入
        if( (user_input < min) or (user_input > max) ):
            print("### 輸入錯誤 ###")
            continue          # 重新開始迴圈，繼續請用戶輸入
        
        # 8. 用戶輸入的數字比較上下界
        if(user_input == lucky_num):
            print("### 恭喜估中了！！！ ###")
            flag = False      # 迴圈會跳出

        elif(user_input > lucky_num):
            print("再小一點")
            max = user_input  # 如果用戶輸入的數字大於 lucky_num，則將 max 設為用戶輸入的數字
        
        elif(user_input < lucky_num):
            print("再大一點")
            min = user_input  # 如果用戶輸入的數字小於 lucky_num，則將 min 設為用戶輸入的數字
    
print("###### End ######")
```
{% endhint %}


## 題目 3： 三角型的9x9乘法表

請嘗試以迴圈輸出：

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202403110049230.png)

## 思路
### 上半部分
- 當 i = 1 時，j 執行 1 次(1)
- 當 i = 2 時，j 執行 2 次(1、2)
- 當 i = 3 時，j 執行 3 次(1、2、3)
- 當 i = 4 時，j 執行 3 次(1、2、3、4)
...
- 當 i = 9 時，j 執行 9 次(由1、2、3、4、5、6、7、8、9)

**外迴圈 i 的值由 1至9、每次+1**
**內迴圈 j 的值由 1至i (j<=i)、每次+1**



### 下半部分
- 當 i = 8 時，j 執行 8 次(1、2、3、4、5、6、7、8)
- 當 i = 7 時，j 執行 7 次(1、2、3、4、5、6、7)
- 當 i = 6 時，j 執行 6 次(1、2、3、4、5、6)
   ...
- 當 i = 2 時，j 執行 2 次(1、2)
- 當 i = 1 時，j 執行 1 次(1)
- 
**外迴圈 i 的值由 8至1、每次-1**
**內迴圈 j 的值由 1至i (j<=i)、每次+1**

### While 迴圈版本
```python
# 上半部份
i = 1
while(i <= 9):
    j = 1
    while(j <= i): # 關鍵邏輯 : 當 j <= i 時，才會有輸出
        print(f"{i}x{j}={i*j:<3}", end="")
        j = j + 1
    print()
    i = i + 1

# 下半部份
i = 8
while(i >= 1):
    j = 1
    while(j <= i): # 關鍵邏輯 : 當 j <= i 時，才會有輸出
        print(f"{i}x{j}={i*j:<3}", end="")
        j = j + 1
    print()
    i = i - 1
```

## For 迴圈版本
```python
# 上半部份
for i in range(1, 10):    # i的值由 1->9
    for j in range(1,10): # j的值由 1->9
        if( j>i ):
            continue # 在這個內迴圈中，break和continue最終效果一樣
        print(f"{i}x{j}={i*j:<3}", end ="")
    print()

# 下半部份    
for i in range(8,0,-1):   # i的值由 8->1 
    for j in range(1,9):  # j的值由 1->8
        if(j>i):
            continue # 在這個內迴圈中，break和continue最終效果一樣
        print(f"{i}x{j}={i*j:<3}", end="")
    print()
```
