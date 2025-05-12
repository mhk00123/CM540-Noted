# Table of contents
* [CM540 課程資料](README.md)
* [Lesson 1 - 認識 Python、環境搭建、變數、變數類型](Lesson\_1.md)
* [Lesson 2 - 變數、資料型態、輸入輸出、邏輯判斷](Lesson\_2.md)
* [Lesson 3 - 邏輯判斷、循環結構](Lesson\_3.md)
* [Lesson 4 - 循環結構、儲存容器](Lesson\_4.md)
* [Lesson 5 - 儲存容器、Function、排序演算法](Lesson\_5.md)
* [Lesson 6 - Dictionary、錯誤捕捉](Lesson\_6.md)
* [Lesson 7 - OOP、Module(time、os)、輸入流輸出流、pip](Lesson\_7.md)
* [Lesson 8 - Module、pip、API、爬蟲入門](Lesson\_8.md)
* [Lesson 9 - API、爬蟲](Lesson\_9.md)
* [Lesson 10 - 爬蟲進階、Pandas介紹](Lesson\_10.md)
* [Lesson 11 - Panda 進階分類、Matplotlib](Lesson\_11.md)


* #########
* [Lesson 3 - 作業答案3題](Lesson\_3\_Homework.md)
* [Lesson 4 - 21點遊戲實作 答案](Lesson\_5\_Homework.md)
* [Lesson 6 - 21點遊戲v2 答案](Lesson\_6\_Homework.md)
* [Lesson 8 - 21點遊戲(Final) 答案](Lesson\_7\_Homework\_v1.md)


* #########
* [如何帶走你的程式碼](HowToBringCode.md)
* [澳門日報 - 程式分享](macaudaily.md)

## 題目 1： 計算BMI指數
繳交網址：[https://hamster.cpttm.org.mo/spaces/bKzjHGCdFKafBQ2jrFNoAQ/upload](https://hamster.cpttm.org.mo/spaces/bKzjHGCdFKafBQ2jrFNoAQ/upload)

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

## 題目 2： 學生成績評級
繳交網址：[https://hamster.cpttm.org.mo/spaces/R9t3AH3_AKZIA5Uo8cY9sA/upload](https://hamster.cpttm.org.mo/spaces/R9t3AH3_AKZIA5Uo8cY9sA/upload)

# 如何打包程式碼為可執行檔(exe)
由於在windows中，我們大部份可執行檔都是`.exe`的文件，因此我們也希望，我們最終的程式碼可以打包成為一個`.exe`文件以供執行。

我們將使用 `pyinstaller` module進行打包工作。

1. 打開 Anaconda Prompt
2. 切換到 `py311` 環境
```bash
activate py311
```
3. 安裝 `pyinstaller` module
```bash
pip install pyinstaller
```

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202412060937844.png)


4. 透過 `cd` 命令進入 `.py` 文件所在的資料夾，例如目前程式碼檔案放在 `D:\Code\Blackjack` 中。
5. 如切換盤符(由C->D)，需要先打一次目的地的盤符才可以完成切換。

```bash
D:
cd D:\Code\Blackjack
```

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202412060942943.png)

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202412060944221.png)

6. 透過打包命令，打包對應的執行環境、module文件
`pyinstaller --onefile 文件名`
```bash
pyinstaller --onefile blackjack.py
```
![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202412060946299.png)

7. 最終生成 `build`、`dist`資料夾，及`blackjack.spec`文件。而我們需要的.exe文件則存放在`dict`文件夾中。

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202412060947575.png)

8. 加入專屬logo(.ico)
```bash
pyinstaller --clean --onefile --icon="logo.ico" blackjack.py
```
![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202412061603226.png)
