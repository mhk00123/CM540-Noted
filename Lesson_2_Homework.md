# Lesson2 - 作業1 詳解

# 功課 1
作業1 : 共 2 題
由於系統限制只能上傳 1 個檔案，您可以
1. 壓縮成 `.zip` `.rar` 繳交 
2. 把 2 個作業的程式碼寫在同1個py檔案中

[https://hamster.cpttm.org.mo/spaces/iG7O6rYBK4mfmZkG5Y-2FA/upload](https://hamster.cpttm.org.mo/spaces/iG7O6rYBK4mfmZkG5Y-2FA/upload)
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
"""
題目 1 :  計算BMI指數
請寫一個程式，提示使用者輸入他們的身高(cm)和體重(kg)然後計算並輸出他們的BMI指數。

BMI = (身高 / (身高)*2)

BMI < 18.5 : 體重過輕
18.5 <= BMI <= 24.9 : 正常範圍
25 <= BMI <= 29.9 : 超重
BMI >= 30 : 肥胖
"""

# 1. 請使用者輸入身高(cm)、體重(kg)
height_cm = int(input("請使用者輸入身高(cm)："))
weight_kg = int(input("請使用者輸入體重(kg)："))

# 2. 令身高(cm) 轉為 (m) 
height_m = float(height_cm) / 100

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

## 題目２： 學生成績評級
請寫一個程式，提示使用者輸入 3 個科目的成績，然後根據以下標準進行評級和總評：

科目分數判斷：
- 每個科目的成績範圍為 0 到 100 分。
- 如果任一科目的成績低於 60 分，則該科目評級為「不及格」。

總評：
___
- 如果三個科目的平均成績低於 60 分，則總評為「不及格」。
- 如果三個科目的平均成績在 60 分（含）以上且小於 70 分，則總評為「及格」。
- 如果三個科目的平均成績在 70 分（含）以上且小於 80 分，則總評為「中等」。
- 如果三個科目的平均成績在 80 分（含）以上且小於 90 分，則總評為「優良」。
- 如果三個科目的平均成績在 90 分（含）以上，則總評為「優秀」。

```python
"""
請寫一個程式，提示使用者輸入 3 個科目的成績，然後根據以下標準進行評級和總評：

科目分數判斷：
---------------
- 每個科目的成績範圍為 0 到 100 分。
- 如果任一科目的成績低於 60 分，則該科目評級為「不及格」。

總評：
---------------
- 如果三個科目的平均成績低於 60 分，則總評為「不及格」。
- 如果三個科目的平均成績在 60 分（含）以上且小於 70 分，則總評為「及格」。
- 如果三個科目的平均成績在 70 分（含）以上且小於 80 分，則總評為「中等」。
- 如果三個科目的平均成績在 80 分（含）以上且小於 90 分，則總評為「優良」。
- 如果三個科目的平均成績在 90 分（含）以上，則總評為「優秀」。
"""

# 1. 使用者輸入三個科目的成績
subject1 = int(input("請輸入中文科目的成績："))
subject2 = int(input("請輸入英文科目的成績："))
subject3 = int(input("請輸入數學科目的成績："))

# 2. 判斷每個科目的評級 (由於3個科目都要單獨判斷，因此不用elif)
if(subject1 < 60):
    grade1 = "中文科評級：不合格"
else:
    grade1 = "中文科評級：合格"
    
if(subject2 < 60):
    grade2 = "英文科評級：不合格"
else:
    grade2 = "英文科評級：合格"
    
if(subject3 < 60):
    grade3 = "數學科評級：不合格"
else:
    grade3 = "數學科評級：合格"

# 3. 計算平均成績
average_score = (subject1 + subject2 + subject3) / 3

# 4. 判斷總評
if (average_score < 60):
    overall_grade = "不及格"
elif (average_score < 70):
    overall_grade = "及格"
elif (average_score < 80):
    overall_grade = "中等"
elif (average_score < 90):
    overall_grade = "優良"
else:
    overall_grade = "優秀"

# 5. 輸出評級和總評
print(f"科目 1 分數：{subject1} 評級：{grade1}")
print(f"科目 2 分數：{subject2} 評級：{grade2}")
print(f"科目 3 分數：{subject3} 評級：{grade3}")
print("總評：", overall_grade)
```