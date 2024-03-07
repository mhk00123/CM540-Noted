# Lesson 2 - 變數、資料型態

**tags: `python`** **`CM-540`** **`Lesson2`**

## Slide
課件：[https://tinyurl.com/3uaxcanp](https://tinyurl.com/3uaxcanp)


### 強制轉型

{% hint style="info" %}
補充資料：函數/方法(Function)，Python自定了很多不同的已經寫好的Function，我們先在這邊開一個頭，在後續的章節中我們會再詳講。所謂函數就是『敘述的集合』，並且以一個函數名稱來代表此敘述集合。通常一個函數可以完成某項功能，所以可以把函數想像成是一種對資料的操作方法。一般來說，函數以這樣的返式表示`函數名()`，例如我們接觸到的`print()` `type()`便是Python內建的函數。
{% endhint %}

從剛才的例子中，我們發現不同型態的變數是無法進行相互運算的，那麼若現在有需要把變數指定類型，可以使用Python中內置的函數對變量類型進行強制轉換

* `int()`：將一個數值或字符串轉換成整數，可以指定進制。
* `float()`：將一個字符串轉換成浮點數。
* `str()`：將指定的對像轉換成字符串形式，可以指定編碼。
* `chr()`：將整數轉換成該編碼對應的字符串（一個字符）。
* `ord()`：將字符串（一個字符）轉換成對應的編碼（整數）。

```python
a = 100
b = 12.345

print(type(a)) # <class 'int'>
print(type(b)) # <class 'float'>

c = str(a)
print(c) # 100
print(type(c)) # <class 'str'>

d = int(b)
print(d) # ???
```

#### 輸入及輸出

到目前為止我們都只有在程式中輸出特定的變數，那麼若今天我們需要由使用者輸入變數，那麼就需要使用Python的輸入`input()`功能。`input()` 是 Python 的內置函數，用於從控制台讀取用戶輸入的內容。`input()` 函數總是以**字符串**的形式來處理用戶輸入的內容，所以用戶輸入的內容可以包含任何字符。

```python
a = input("請輸入內容") # 輸入 123

print(a) # 123
print(type(a)) # <class 'str'>
```

若我們需要對變數進行運算，則需要對其進行強制轉型

```python
a = input("請輸入數字1： ") # 輸入 123
b = input("請輸入數字2： ") # 輸入 456

# 強制轉型並重新賦值
a = int(a)
b = int(b)

# 兩個變數相加
rs = a + b

print(rs) # 579

print(type(a))  # <class 'int'>
print(type(b))  # <class 'int'>
print(type(rs)) # <class 'int'>
```

**簡寫**

在Python中，函數可以嵌套，執行順序以括號優先。套用以上例子，我們可以把`input()`的程式碼簡化為：

```python
# 在輸入後，強制轉型並賦值
a = int(input("請輸入數字1： ")) # 輸入 123
b = int(input("請輸入數字2： ")) # 輸入 456

print(type(a))  # <class 'int'>
print(type(b))  # <class 'int'>
```

#### 格式化輸出

在Python3中，提供了簡潔的字串格式化語法，使用方式就是在字串的前方加上`f` 或 `F` 前綴字，接著在 `{}` 符號中，傳入**變數或運算式**，Python會將 `{}` 中的變數資料或運算結果帶出來。

```python
first_name = "Leo"
last_name ="Tam"
my_phone_num = 28781313

print("Hi, My name is " + first_name + " " + last_name + ", my phone number is " + str(my_phone_num))
# Hi, My name is Leo Tam, my phone numer is 28781313

# f-string
print(f"Hi, My name is {first_name} {last_name}, my phone number is {my_phone_num}")
# Hi, My name is Leo Tam, my phone numer is 28781313
```

### 格式化輸出變數的用法

```python
num1 = 12.345 
num2 = 456.789
print(f'{num1}')
print(f'{num2}')
```

#### 對齊
- `<` 靠左對齊 
- `>` 靠右對齊 (默認)
- `^` 置中對齊


```python
# 觀察
# 12.345  => 6個位元
# 456.789 => 7個位元

print(f'{num1:7}')
print(f'{num2:7}')
```

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202402280216877.png)

**補0**

```python
print(f'{num1:07}')
print(f'{num2:07}')
```

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202402280216982.png)

**精度(取小數點後 n 位)**

```python
print(f'{num1:.2}')
print(f'{num2:.1}')
```

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202402280219610.png)
