# Lesson_2_Homework

{% hint style="info" %}
# 題目 1： 計算BMI指數

[https://hamster.cpttm.org.mo/spaces/THu_NiO5huaQbk42zhIjrw/upload](https://hamster.cpttm.org.mo/spaces/THu_NiO5huaQbk42zhIjrw/upload)

請寫一個程式，提示使用者輸入他們的身高（ cm ）和體重（kg）然後計算並輸出他們的BMI指數。
* 提示：在計算BMI指數時，需要將身高從 cm 轉換為 m

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202502271842351.png)


根據計算結果使用以下標準判斷BMI指數的範圍：

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202502271841302.png)

{% endhint %}

```python
# ''''''''''''''''''''''''''''''
# 1. 請使用者輸入身高(cm)和體重(kg)
# 2. 身高從cm 轉換成 m
# 3. 計算BMI值
# 4. 判斷BMI值的範圍
# ''''''''''''''''''''''''''''''

# 1. 請使用者輸入身高(cm)和體重(kg)
height_cm = float(input("請輸入身高(cm): "))
weight = float(input("請輸入體重(kg): "))

# 2. 身高從cm 轉換成 m
height_m = (height_cm / 100)

# 3. 計算BMI值
bmi = weight / (height_m * height_m)

# 4. 判斷BMI值的範圍
if(bmi < 18.5):
    print("體重過輕")
    
elif(bmi < 25):
    print("體重正常")
    
elif(bmi < 30):
    print("體重超重")
    
else:
    print("體重肥胖")   
```
