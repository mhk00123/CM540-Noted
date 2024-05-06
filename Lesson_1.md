# Lesson 1
認識 Python、環境搭建、變數、變數類型

**tags: `python`** **`CM-540`** **`Lesson1`**

# Slide
課件：[https://shorturl.at/stvQT](https://shorturl.at/stvQT)

Python 3.11 官方手冊：[https://docs.python.org/zh-tw/3.11/](https://docs.python.org/zh-tw/3.11/)

# 作業/考試 繳交
請在家中的電腦嘗試使用Anaconda安裝Python環境、以及Visual Studio Code，完成後截圖並上傳。

繳交網址 : [https://hamster.cpttm.org.mo/spaces/1Bwtj5LHBMa6FDYIblKx4g/upload](https://hamster.cpttm.org.mo/spaces/1Bwtj5LHBMa6FDYIblKx4g/upload)


# Python 是甚麼 ?

Python眾多程式語言中的一種，它是一種直譯式的程式語言，也是一種膠合語言。屬於直譯式的原因是，它的程式在執行時是一行接著一行的，也就是說，系統會先翻譯一行執行它，如果順利執行之後，再翻譯下一行，再執行。

英國發音：/ˈpaɪθən/ 美國發音：/ˈpaɪθɑːn/

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202403021530581.png)

Python亦稱為膠水語言，主要源於以下幾個原因：

* Python 是一種解釋型語言：這表示開發過程中沒有了編譯這個環節。類似於PHP和Perl語言。
* Python 是互動式語言：這意味著，您可以在一個Python 提示符號>>>後直接執行程式碼。
* Python 是初學者的語言： Python 對初級程式設計師而言，是一種很棒的語言，它支援廣泛的應用程式開發，從簡單的文字處理到WWW 瀏覽器再到遊戲。
* Python可以在多環境下執行：Windows、Linux、iOS......等平台均可以執行。

## 程式運行原理

一般來說，程序有分二大類，**1. 編譯式語言**、**2. 直譯式語言**

* **編譯式語言(Compiled language)**

其實電腦只看得懂1跟0，也就是機器語言。不過要我們人去寫機器語言，也太強人所難了；不只不好思考，我們處理滿篇的0與1也不可能比電腦快，這樣效率太低了。

於是乎，人類發明了：**編譯器(compiler)**

我們可以透過用接近人類語言的程式語言，將程式碼寫好之後，再交給編譯器去幫我們「翻譯」成電腦看得懂的機器語言(也就是翻譯成滿篇的0與1)，再請電腦執行翻譯過後的程式。

這類型的語言多半都是強型別的語言(strongly-typed)，有非常嚴格的檢查機制。不過它們的執行速度非常快，畢竟已經翻譯成電腦看得懂的語言了。著名的編譯語言有：`C`、`C++`、`Java`、`C#`、`Rust`、`Swift`等等。

* **直譯式語言(Interpreted language)**

既然電腦只看得懂0與1的機器語言，直譯式語言一樣會把程式語言翻譯成機器語言，差別在於它是一行一行翻譯，而不是一口氣將整篇翻好。直譯式語言會從上到下，由左至右，翻譯完一行之後，執行一行。有點像專業的口譯翻譯員，聽完一段翻譯一段，而編譯式則比較像筆譯翻譯員，將整篇文章讀完，再將整篇翻譯。

直譯式的語言多半為弱類型的語言(weakly-typed)，語法非常簡單易懂，甚至快跟平常說的英文一樣了，非常易學。著名的語言有：`Python`、`JavaScript`、`Ruby`、`PHP`、

不過直譯式語言這麼做的代價當然就是，速度很慢。畢竟你想想，整篇翻完執行，跟一行一行翻譯然後一邊執行，哪邊比較快呢？當然是整篇翻完得比較快。需要追求速度的程式，基本上都是用C++去寫的。但直譯式語言雖然執行速度慢，但開發速度就很快了，除錯也比編譯式快，畢竟你一寫完可以馬上執行馬上看結果，不用等編譯過程。

直譯式語言也有其優點，像是寫自動化測試等等。這種可以寫一點然後馬上測試看結果的，非常適合直譯式語言。

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img/2024/202402041629329.png)

## Hello World 寫法比較

### Java

```java
// 使用 Java 令電腦輸出Hello World
package helloworld;

public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello World!");
    }
}
```

### C++

```cpp
// 使用 C++ 令電腦輸出Hello World
#include <iostream.h>
Main() {
    cout << "Hello World!" << endl;
    return 0;
}
```

### Python

```python
# 使用 Python 令電腦輸出Hello World
print("Hello World")
```

# 如何運行Python?

* 本課程基於 `Python 3.11.7` 版本 (若有語法更新，請自行查詢手冊)

由於Python是直譯式的程式語言，因此執行Python有著很多很多的方法，本課程將會教大家 2 種方法執行，大家可以按照個人喜好選擇。

> 注意：在爬蟲的章節，由於套件問題建議使用本機環境方式執行

## 環境搭建(1) - 本機(Local)形式

在本機中直接安裝Python執行環境、配合 Visual Studio Code 完成開發

### 一、安裝 Python 環境

1. 先到 Python 官方網站下載 : https://www.python.org/

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img/2024/202402041607246.png)

2. 選擇 `Windows 64-bit` 版本 (亦可按照自身需求，選擇macOS、32-bit、ARM版本)

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img/2024/202402041610443.png)

3. 為方便後續管理，請把 `Add python.exe to PATH` 打勾

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img/2024/202402041618824.png)

4. 安裝完成後，我們可以在Windows開始菜單中，找到Python 3.11 相關程式

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img/2024/202402041626154.png)

5. 打開`IDLE(Python3.11 64-bit)`，並輸入以下代碼。若有成功顯示，表示則Python環境已經順利安裝到電腦中。

```python
print("Hello World!")
```

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img/2024/202402041633572.png)

### 二、撰寫您的第一個程式 Hello World

1. 首先在 IDEL 的左上方點擊 File -> New File

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img/2024/202402041748782.png)

2. 在這個地方輸入程式碼

```python
print("Hello World 1")

print("Hello World 2")

print("Hello World 3")
```

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img/2024/202402041751080.png)

3. 儲存檔案 `HelloWorld.py`

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img/2024/202402041753562.png)

4. 點擊 Run -> Run Module 執行程式碼

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img/2024/202402041755050.png)

5. Shell顯示執行成功

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img/2024/202402041756721.png)

## 安裝整合執行環境(Anaconda) - 推薦
有了本機安裝的環境，一般已足夠滿足部份用戶，但我們仍然推薦使用整合的環境。

### Python 環境分區
由於每個Python版本都相互獨立，在開發中，難免有時會遇到客戶指定的套件/功能在持定的版本才有，因此，若使用方法1在本機安裝，那麼在開發和調試中會遇到很多不方便的情況。

此時我們可以整合執行環境 - Anaconda解決問題，他的原理是，透過Conda工具，開設一個虛擬的環境(Virtual Environment)，在此環境中開發者可以指定不同的Python版本，不同的套件，以方便管理。
![](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202403021803092.png)


到Anaconda官方網站下載安裝檔案 : [https://www.anaconda.com/](https://www.anaconda.com/)

1. **執行安裝程式**

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202403021753367.png)

2. 注意勾選 **Add Anaconda3 to my_PATH environment variable**

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202403021754828.png)

3. 完成後可看到 Anacaonda3 程式界面

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202403021755356.png)

Anaconda 會為我們默認配置一個虛擬的可執行Python的環境(Env)，打開Anacaonda Prompt

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202403021759062.png)

即可看到 `(base)` 字樣

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202403021759254.png)

4. 透過命令我們可以看到此虛擬環境的版本為 `3.11.7`
```bash
python --version
```

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202403021800394.png)

## 創建指定版本的 env
Ex : 創建一個Python版本為3.11.7的env

1. 透過命令提示輸入 `conda create -n 環境名 python=版本號`
```bash
conda create -n py311 python=3.11.7
```

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202403021816688.png)

2. 成功後會看到

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202403021816451.png)

3. 進入環境
透過命令提示輸入 `conda activate 環境名稱`
```bash
conda activate py311
```

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202403021819440.png)

## Conda 命令
- 查看已創建環境
```bash
conda info --env
```

- 創建環境
```bash
conda create -n py311 python=3.11.7
```

- 創建環境
```bash
conda remove -n py311 -all
```
- 進入環境
```bash
conda activate py311
```

- 退出環境
```bash
conda deactivate
```

### 三、安裝 IDE - Visual Studio Code

一般來說，大部份開發者都會更傾向於使用IDE作為開發工具，因為其很高的整合性，以及自動補全、除錯能力等都會更有利開發者使用。在此我們使用目前市面上較高知名度的Visual Studio Code成為本課程的IDE工具。

VS Code 下載: https://code.visualstudio.com/download

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img/2024/202402041804826.png)

1. 重新打開 `HelloWorld.py`，並按下鍵盤 F5 -> Python File 執行

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img/2024/202402041807495.png)

2. 執行成功

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img/2024/202402041809954.png)

3. 選取不同版本的 Conda Env
可以按下鍵盤的`ctrl`+`shift`+`p` 並輸入 `Select Interpreter`

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202403021902262.png)

VS Code會自動檢查系統中包含的所有環境，在這里可以選擇Conda創建的`py311` env。

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202403021903518.png)



## 環境搭建(2) - Jupyter

### 一、Jupyter Notebook

由於Python為直譯式語言，因此有開發者推出可以一行一行執行的執行環境 - Jupyter Notebook，Jupyter Notebook是以網頁的形式打開，可以在網頁頁面中直接編寫程式碼和執行程式碼，程式碼的運行結果也會直接在程式碼區塊下顯示的程式。如在程式設計過程中需要編寫說明文檔，可在同一個頁面中直接編寫，以便於作及時的說明和解釋。

由於透過Jupyter執行可以一行一行地顯示當前程式碼的執行結果，因此特別方便用於資料分析的使用者。

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img/2024/202402041853337.png)

Jupyter可以透過本機佈署、可以使用Plugin型式安裝在Visual Studio Code中、也可以直接透過網頁版執行。

本課程推薦使用 Google Colab 服務直接取用 Jupyter Notebook，以節省配置時間。

### 二、Anaconda 內建 Jupyter
我們所安裝的Anaconda中，會自帶 Jupyter，我們可以直接在執行。

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202403022002460.png)

選擇對應的Python 3編譯器

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202403022003538.png)

Jupyter 檔案不是以 .py 結尾，是以 .ipynb 結尾

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202403022004774.png)

輸入 `print("Hello World")` 後按下執行即會顯示結果

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202403022005662.png)

### 輸出 .ipynb 文件至 .py文件

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202403022020588.png)


### 三、Google Colab

1. 登入您的 Google 帳號
2. 進入 Google Colab 服務：https://colab.research.google.com/
3. 新增一個"記事本"，所有有關Google Colab的文件將會存放在你的個人Google Drive中

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img/2024/202402041857579.png)

4. 為該檔案更改名稱，`HelloWord.ipynb`，使用Jupyter的檔案以`.ipynb`結尾

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img/2024/202402041902180.png)

5. 同樣地，可以嘗試輸入剛才`HelloWord.py`中的內容

```python
print("Hello World 1")
 
print("Hello World 2")
 
print("Hello World 3")
```

6. 按下執行即可顯示結果

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img/2024/202402041903668.png)

# Python的組成：
1. 變數
2. 資料型態: `int`、`float`、`str`、`bool`。
3. 儲存容器: `list`、`tuple`、`set`、`dict`。
4. 輸出與輸入: `print()`、`input()`。
5. 運算子、運算式：加減乘除、大小等於。
6. 流程控制(選擇性敘述): `if`、`elif`、`else`
7. 重複執行的迴圈: `for`、`while`、`switch`。
7. 例外狀況處理: `try` `except`。

## 程式語言中的變量/變數是什麼?

```python
print("Hello World!")
```

觀察到程式碼的 Hello World 用了一對引號`" "`包起來，引號包起來的東西我們叫`字串 String`，是Python中的一種數據類型，目前這個字串是固定狀態的，俗稱hard-coding(寫死的)，即若我們如果需要輸出另外的文字，我們需要直接改變程式中的引號的內容，這顯然是不合理的，因此在這章我們引入變數的概念，令這個固定的內容可以隨著不同的需求，而動態作更改。

### 定義／宣告 變數

**變數就是存放資料值的容器**，我們可以使用英文字母 + 數字，去表示去定義變數。

```python
a = 1
```

這里的意思是：

1. 把數字 `1` **放進** 物件容器當中
2. 指定該容器的名稱為 `a` (等於符號的作用)

* 這里的等於符號並不是指相等的意思，在大部份程式語言中，這個等於符號的意思是**給予/賦予**的意思 ![](https://cdn.jsdelivr.net/gh/mhk00123/my-img/2024/202402042342728.png)

#### 變數命名

按照Python官方的限制，變數的命名有以下限制：

* 英文字母：**a-z**、**A-Z** (變數區分大小寫)
* 數字：**0-9**
* 符號：只能使用**底線/下劃線** `_`
* **變數名稱不得以數字開頭**

```python
# 合法變數命名
a = 1
cpttm = 2
Cpttm = 3
LeOtam = 4
Leo_tam = 5
_LEotam = 6

# 不合法變數
1Leo = 7 # 以數字開頭
CM-540 = 8 # 包含非法符號破折號 - 
%m53$ = 9 # 包含非法符號
```

改寫 `HelloWorld.py`

```python
a = "Hello World"
print(a)
# Hello World

b = "CM-540"
print(b)
# CM-540

# 如果 a + b 呢?
print( a + b )
```

#### 變數命名規則

事實上對於電腦來說，變數名稱的好壞並不重要。 真正重要的好壞，是變數命名習慣將影響整個程式的可讀性及可維護性。

{% hint style="info" %}
因為變數是給人看的。
{% endhint %}

命名習慣的好壞可由以下2點判斷:

* 可讀性
* 一致性

**可讀性**

我們剛才的例子中，都是使用a、b、c....等作為變數名稱，實際上，隔了一段時間後再看回程式碼的話，我們很大概率會忘記這些變數的意思，若是面對更複雜的 function 或是整個大結構的程式，我們會很難讀懂程式的運作。

實務上，對於大型程式的變數，我們一般會把該變數的作用以英文方式作命名。

**一致性**

一致性是指必須要用相同的規則命名整個程式的變數，可以是合作的工程師口頭約定也可以是一份 Code Style 文字文件。

如果採用了駝峰式就必須一直使用駝峰式，如果將使用者名稱命名成userName 就不要在中途改成 accountName 或只剩下 user，維持整個工程代碼的命名一致性。

### 主流命名方式

#### Camel Case (駝峰式命名法)

第一個字母為小寫，之後每一個單字的開頭為大寫，不包含空格。例如:

* userName
* fileName

#### Snake Case 命名法

單字皆為小寫，單字以底線\_分離。例如:

* user\_name
* file\_name

#### Screaming Case 命名法

跟Snake Case類似，單字皆為全大寫，一般用於**常量**(後續會介紹)。例如:

* USER\_NAME
* FILE\_NAME

### 變數類型、資料型態

Python 的內建型態主要分為以下幾種：

1. 整數(`int`)：1、100、-50
2. 浮點數(`float`)：3.14、2.0、-6.7
3. 字串(`string`)：用來表示文字，必須用單引號或雙引號括住，"Hello World"、 'Hello World'
4. 布林型態(`bool`) ：用來表示真或假，只有兩個值`True` 和 `False`

資料型態在程式中很重要，它們決定了資料的處理方式和運算規則，因此在撰寫程式時需要確保資料型態的一致性和適當使用。

#### 整數(integer)

一般來說，所有沒有小數點的數字，我們都歸類為整數。在 Python2 裡，分`整數 int`跟`長整數 long`，而在 Python3 裡，不管多大的數字，都只會顯示`整數 int`，已經沒有`長整數 long`的概念了，但其他語言仍然還是有`長整數 long`的概念，所以我們還是需要了解一下。

長整數: 即大於等於2^64，一般要在定義變數時加上`L`作標記

正常情況下，整數是有取值範圍的：

* 在32位元的機器上，整數的位數為32位，取值的範圍為 -2^31 \~ 2^31-1 即 -2147483648 \~ 2147483648
* 在64位元的機器上，整數的位數為64位，取值的範圍為 -2^63 \~ 2^63-1 即 -9223372036854775808L \~ 9223372036854775807L

但由於Python3後統一使用長整數類型，不會存在溢出問題，即可以存放任意大小的數值不會出錯。

如果是其他語言的話，存超過限制的話，會發生錯誤的，而在Python裡，則會自動幫你做轉換。

```python
# 定義一個整數

# 隠式定義
a = 1

# 顯式定義
b = int(1)

c = 2**101
```

#### 浮點數(float)

廣義上浮點數就是有小數點的數字，其實不完全正確，還有部份不常用的情況涉及計算機概論知識，礙於篇幅，我們這裡不展開討論，本課程中僅會出現含小數點的情況。

浮點數有兩種表示方式

1. 直接包含小數：`314.159`、 `314159.0`(含有.0也算是浮點數)
2. 小數 + E次冪(E標記是表示 10的冪數)：`52.3E4`即`523000.0`

```python
# 宣告一個浮點數

# 隠式宣告
a = 314.159
b = 314159.0
c = 52.3E4

# 顯式宣告
d = float(314.159)
```

#### Boolean 布林

布林（英語：Boolean）是電腦科學中的**邏輯資料**類型，它是只有兩種值的原始類型，通常是

* 真 `True`
* 假 `False`

#### 字串(String)

字串由一串有順序的字元所組成，也屬於Python 序列(Sequence)的一種，稱為字元序列。字串**成對的引號**來呈現，`單引號`、`雙引號` 、`三個單引號`、`三個雙引號`都可以拿來表示字串。如果想表達文字，卻忘了使用引號，Python 會將你輸入的文字視為變數、數字或是保留字。

```python
# 正常字串宣告
str_1 = 'this'
str_2 = "is"
str_3 = '''a'''
str_4 = """string"""

# 如果想表達文字，卻忘了使用引號，Python 會將你輸入的文字視為變數、數字或是保留字。
temp_str = str_1
# temp_str = 'this'
```

**字元**

剛才我們說字串是**字元序列**，字元又是什麼？像是`字母`、`數字`、`符號`、`空格`或是`換行`都是字元，一個 a 是一個字元，一個空格也是一個字元，它是文書系統裡頭最小的單位。

**字串長度**

既然Python的字串是字元序，那麼，在這個序列中各個字元的位置、以及整個字串的長度，我們應如何計算呢?

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img/2024/202402062340466.png)

1. 在Python中，任何**序列**開端編號(Index)一定為 `0`
2. 每一字元皆佔 1 個長度

以`"Hello World!"`作例子，這個字串的長度為：**12**

**取得字元**

可以透過中括號`[ ]`取得任意字串中的字元

```python
str_1 = "Hello World!"

print(str_1[4]) # o

print(str_1[6]) # W
```

另外，在Python中，也可以**反向**取得字元 

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img/2024/202402062348197.png)

```python
str_1 = "Hello World!"

print(str_1[-2]) # d

print(str_1[-6]) # W
```

**改變字串**

Python 字串是`不可變的 （inmmutable）`，你無法使用方法（Method）對字串進行修改，但可以透過指派一個新的值給變數，來達到修改的效果。也就是說，字串屬於`不可變的資料型態`。

```python
name = "Leo"

# 嘗試把 name[0] 改變為 N
# 系統顯示報錯
name[0] = "N"
```

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202402232325812.png)

因此若我們想改變字串中的內容，可以採用 `replace()` 函數

```python
name = "Leo"

# 把 L 改變為 N
name = name.replace("L","N")
print(name) # Neo
```

**字串相加**

如果要將兩個字串連接起來，在Python中使用 `+`

```python
first_name = "Leo"
last_name ="Tam"
my_phone_num = 28781313

print("Hi, My name is " + first_name + " " + last_name + ", my phone number is " + str(my_phone_num))
# Hi, My name is Leo Tam, my phone numer is 28781313
```

#### 檢查變量型態

可以使用 `type()` 函數去檢查該變量屬於甚麼型態

```python
a = 100
b = 12.345
c = "Hello, World"
d = True

print(type(a))    # <class 'int'>
print(type(b))    # <class 'float'>
print(type(c))    # <class 'str'>
print(type(d))    # <class 'bool'>
```