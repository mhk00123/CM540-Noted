# Lesson 1 - 認識 Python
###### tags: `python` `CM-540` `Lesson1`

## 認識Python、搭建編程環境
+ [ ] 認識Python
+ [ ] 本機搭建
+ [ ] Jupyter Notebook
+ [ ] 執行你的第一個 Python 程式 - `HelloWord.py`


## Python 是甚麼 ?
Python 是一個高層次的結合了解釋性、編譯性、互動性和物件導向的腳本語言。Python 的設計具有很強的可讀性，相比其他語言經常使用英文關鍵字，其他語言的一些標點符號，它具有比其他語言更有特色語法結構。


英國發音：/ˈpaɪθən/
美國發音：/ˈpaɪθɑːn/

Python亦稱為膠水語言，主要源於以下幾個原因：
- Python 是一種解釋型語言：這表示開發過程中沒有了編譯這個環節。類似於PHP和Perl語言。

- Python 是互動式語言：這意味著，您可以在一個Python 提示符號>>>後直接執行程式碼。

- Python 是初學者的語言： Python 對初級程式設計師而言，是一種很棒的語言，它支援廣泛的應用程式開發，從簡單的文字處理到WWW 瀏覽器再到遊戲。    

- Python可以在多環境下執行：Windows、Linux、iOS......等平台均可以執行。

## 程式運行原理
一般來說，程序有分二大類，**1. 編譯式語言**、**2. 直譯式語言**

- ### 編譯式語言(Compiled language)

其實電腦只看得懂1跟0，也就是機器語言。不過要我們人去寫機器語言，也太強人所難了；不只不好思考，我們處理滿篇的0與1也不可能比電腦快，這樣效率太低了。

於是乎，人類發明了：**編譯器(compiler)**

我們可以透過用接近人類語言的程式語言，將程式碼寫好之後，再交給編譯器去幫我們「翻譯」成電腦看得懂的機器語言(也就是翻譯成滿篇的0與1)，再請電腦執行翻譯過後的程式。

這類型的語言多半都是強型別的語言(strongly-typed)，有非常嚴格的檢查機制。不過它們的執行速度非常快，畢竟已經翻譯成電腦看得懂的語言了。著名的編譯語言有：`C`、`C++`、`Java`、`C#`、`Rust`、`Swift`等等。

- ### 直譯式語言(Interpreted language)

既然電腦只看得懂0與1的機器語言，直譯式語言一樣會把程式語言翻譯成機器語言，差別在於它是一行一行翻譯，而不是一口氣將整篇翻好。直譯式語言會從上到下，由左至右，翻譯完一行之後，執行一行。有點像專業的口譯翻譯員，聽完一段翻譯一段，而編譯式則比較像筆譯翻譯員，將整篇文章讀完，再將整篇翻譯。

直譯式的語言多半為弱類型的語言(weakly-typed)，語法非常簡單易懂，甚至快跟平常說的英文一樣了，非常易學。著名的語言有：`Python`、`JavaScript`、`Ruby`、`PHP`、

不過直譯式語言這麼做的代價當然就是，速度很慢。畢竟你想想，整篇翻完執行，跟一行一行翻譯然後一邊執行，哪邊比較快呢？當然是整篇翻完得比較快。需要追求速度的程式，基本上都是用C++去寫的。但直譯式語言雖然執行速度慢，但開發速度就很快了，除錯也比編譯式快，畢竟你一寫完可以馬上執行馬上看結果，不用等編譯過程。

直譯式語言也有其優點，像是寫自動化測試等等。這種可以寫一點然後馬上測試看結果的，非常適合直譯式語言。

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img/2024/202402041629329.png)


## Hello World 寫法比較
### Java
``` Java
// 使用 Java 令電腦輸出Hello World
package helloworld;

public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello World!");
    }
}
```
### C++
``` C++
// 使用 C++ 令電腦輸出Hello World
#include <iostream.h>
Main() {
    cout << "Hello World!" << endl;
    return 0;
}
```

### Python
``` Python
# 使用Python 令電腦輸出Hello World
print("Hello World")
```

## 如何運行Python?
需要在安裝了Python環境的計算機系統中運行(Mac 自帶 Python 2.x版本)。
Windows 則需要安裝對應的環境才可以執行Python程式碼。

## 環境搭建
 - 本課程基於 `Python 3.11.7` 版本 (若有語法更新，請自行查詢手冊)

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
