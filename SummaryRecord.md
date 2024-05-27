# Table of contents
* [CM540 課程資料](README.md)
* [Lesson 1 - 認識 Python、環境搭建、變數、變數類型](Lesson\_1.md)
* [Lesson 2 - 變數、資料型態、輸入輸出、邏輯判斷](Lesson\_2.md)
* [Lesson 3 - 邏輯判斷、循環結構](Lesson\_3.md)
* [Lesson 4 - 函數(方法)、儲存容器](Lesson\_4.md)
* [Lesson 5 - 儲存容器、List](Lesson\_5.md)
* [Lesson 6 - 儲存容器 - Dictionary、錯誤捕捉](Lesson\_6.md)
* [Lesson 7 - Module(time、os)、輸入流輸出流、pip](Lesson\_7.md)
* [Lesson 8 - pip、API、爬蟲入門](Lesson\_8.md)
* [Lesson 9 - API、爬蟲](Lesson\_9.md)
* [Lesson 10 - 交通局停車場API、Pandas介紹](Lesson\_10.md)
* [Lesson 11 - Pandas基礎、Matplotlib基礎](Lesson\_11.md)
* [\*\*\*Final Project\*\*\*](Final\_Project.md)
* [變數命名參考守則](變數命名參考守則.md)
* [運算符優先順序](運算符優先順序.md)
* [Lesson 2 - 作業答案](Lesson\_2\_Homework.md)
* [Lesson 3 - 作業答案](Lesson\_3\_Homework.md)
* [Lesson 5 - 21點遊戲實作 答案](Lesson\_5\_Homework.md)
* [Lesson 6 - 21點遊戲增強 答案](Lesson\_6\_Homework.md)
* [Lesson 7 - 21點遊戲(Final) 答案](Lesson\_7\_Homework.md)
* [Get MPF 程式碼範例](GetMPF.md)# SummaryRecord


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

# 1. 使用者輸入三個科目的成績
subject1 = int(input("請輸入中文科目的成績："))
subject2 = int(input("請輸入英文科目的成績："))
subject3 = int(input("請輸入數學科目的成績："))

if((subject1 < 0) or (subject2 < 0) or (subject3 < 0)):
    print("輸入錯誤，請輸入大於 0 的分數")
    exit()

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
