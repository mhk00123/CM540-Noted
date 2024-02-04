# Lesson 1 - 認識 Python

**tags: `python`** **`CM-540`** **`Lesson1`**

## 認識Python、搭建編程環境

* [ ] 認識Python
* [ ] 本機搭建
* [ ] Jupyter Notebook
* [ ] 執行你的第一個 Python 程式 - `HelloWord.py`

## Python 是甚麼 ?

Python眾多程式語言中的一種，它是一種直譯式的程式語言，也是一種膠合語言。屬於直譯式的原因是，它的程式在執行時是一行接著一行的，也就是說，系統會先翻譯一行執行它，如果順利執行之後，再翻譯下一行，再執行。

英國發音：/ˈpaɪθən/ 美國發音：/ˈpaɪθɑːn/

Python亦稱為膠水語言，主要源於以下幾個原因：

* Python 是一種解釋型語言：這表示開發過程中沒有了編譯這個環節。類似於PHP和Perl語言。
* Python 是互動式語言：這意味著，您可以在一個Python 提示符號>>>後直接執行程式碼。
* Python 是初學者的語言： Python 對初級程式設計師而言，是一種很棒的語言，它支援廣泛的應用程式開發，從簡單的文字處理到WWW 瀏覽器再到遊戲。
* Python可以在多環境下執行：Windows、Linux、iOS......等平台均可以執行。

## 程式運行原理

一般來說，程序有分二大類，**1. 編譯式語言**、**2. 直譯式語言**

* #### 編譯式語言(Compiled language)

其實電腦只看得懂1跟0，也就是機器語言。不過要我們人去寫機器語言，也太強人所難了；不只不好思考，我們處理滿篇的0與1也不可能比電腦快，這樣效率太低了。

於是乎，人類發明了：**編譯器(compiler)**

我們可以透過用接近人類語言的程式語言，將程式碼寫好之後，再交給編譯器去幫我們「翻譯」成電腦看得懂的機器語言(也就是翻譯成滿篇的0與1)，再請電腦執行翻譯過後的程式。

這類型的語言多半都是強型別的語言(strongly-typed)，有非常嚴格的檢查機制。不過它們的執行速度非常快，畢竟已經翻譯成電腦看得懂的語言了。著名的編譯語言有：`C`、`C++`、`Java`、`C#`、`Rust`、`Swift`等等。

* #### 直譯式語言(Interpreted language)

既然電腦只看得懂0與1的機器語言，直譯式語言一樣會把程式語言翻譯成機器語言，差別在於它是一行一行翻譯，而不是一口氣將整篇翻好。直譯式語言會從上到下，由左至右，翻譯完一行之後，執行一行。有點像專業的口譯翻譯員，聽完一段翻譯一段，而編譯式則比較像筆譯翻譯員，將整篇文章讀完，再將整篇翻譯。

直譯式的語言多半為弱類型的語言(weakly-typed)，語法非常簡單易懂，甚至快跟平常說的英文一樣了，非常易學。著名的語言有：`Python`、`JavaScript`、`Ruby`、`PHP`、

不過直譯式語言這麼做的代價當然就是，速度很慢。畢竟你想想，整篇翻完執行，跟一行一行翻譯然後一邊執行，哪邊比較快呢？當然是整篇翻完得比較快。需要追求速度的程式，基本上都是用C++去寫的。但直譯式語言雖然執行速度慢，但開發速度就很快了，除錯也比編譯式快，畢竟你一寫完可以馬上執行馬上看結果，不用等編譯過程。

直譯式語言也有其優點，像是寫自動化測試等等。這種可以寫一點然後馬上測試看結果的，非常適合直譯式語言。

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img/2024/202402041629329.png)

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
# 使用Python 令電腦輸出Hello World
print("Hello World")
```

## 如何運行Python?
* 本課程基於 `Python 3.11.7` 版本 (若有語法更新，請自行查詢手冊)

由於Python是直譯式的程式語言，因此執行Python有著很多很多的方法，本課程將會教大家 2 種方法執行，大家可以按照個人喜好選擇。 
> 注意：在爬蟲的章節，由於套件問題建議使用本機環境方式執行

## 環境搭建(1) - 本機(Local)形式
在本機中直接安裝Python執行環境、配合 Visual Studio Code 完成開發

### 一、安裝 Python 環境
1. 先到 Python 官方網站下載 : https://www.python.org/

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img/2024/202402041607246.png)

2. 選擇 `Windows 64-bit` 版本 (亦可按照自身需求，選擇macOS、32-bit、ARM版本)

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img/2024/202402041610443.png)

3. 為方便後續管理，請把 `Add python.exe to PATH` 打勾

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img/2024/202402041618824.png)

4. 安裝完成後，我們可以在Windows開始菜單中，找到Python 3.11 相關程式

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img/2024/202402041626154.png)

5. 打開`IDLE(Python3.11 64-bit)`，並輸入以下代碼。若有成功顯示，表示則Python環境已經順利安裝到電腦中。

```python
print("Hello World!")
```

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img/2024/202402041633572.png)

### 二、撰寫您的第一個程式 Hello World
1. 首先在 IDEL 的左上方點擊 File -> New File

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img/2024/202402041748782.png)

2. 在這個地方輸入程式碼
``` python
print("Hello World 1")

print("Hello World 2")

print("Hello World 3")
```

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img/2024/202402041751080.png)

3. 儲存檔案 `HelloWorld.py`

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img/2024/202402041753562.png)

4. 點擊 Run -> Run Module 執行程式碼

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img/2024/202402041755050.png)

5. Shell顯示執行成功

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img/2024/202402041756721.png)

### 三、安裝 IDE - Visual Studio Code
一般來說，大部份開發者都會更傾向於使用IDE作為開發工具，因為其很高的整合性，以及自動補全、除錯能力等都會更有利開發者使用。在此我們使用目前市面上較高知名度的Visual Studio Code成為本課程的IDE工具。

VS Code 下載: https://code.visualstudio.com/download

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img/2024/202402041804826.png)

1. 重新打開 `HelloWorld.py`，並按下鍵盤 F5 -> Python File 執行

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img/2024/202402041807495.png)

2. 執行成功

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img/2024/202402041809954.png)
