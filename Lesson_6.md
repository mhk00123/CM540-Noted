# Lesson 6 - 傳參傳址、Dictionary、錯誤捕捉

**tags: `python`** **`CM-540`** **`Lesson6`**

傳參傳址、Dictionary、錯誤捕捉

## Slide
課件：[https://docs.google.com/presentation/d/1P6d7MLJ2wQ575pxFVLx80tfqFBggMq8CJRwg9EzeZO0/edit?usp=sharing](https://docs.google.com/presentation/d/1P6d7MLJ2wQ575pxFVLx80tfqFBggMq8CJRwg9EzeZO0/edit?usp=sharing)

# 作業：
截止時間：2025年6月1日 23:59

{% hint style="info" %}

# 21 點遊戲單人版 Version 2

繳交網址：[https://hamster.cpttm.org.mo/spaces/qiStjaFjLahBUZU-QUqFXg/upload](https://hamster.cpttm.org.mo/spaces/qiStjaFjLahBUZU-QUqFXg/upload)

---
- 以 list/dict 方式把所有牌分開花式及點數(hints：二維list)
- 每 1 輪發牌 - 改以 `Random` 方式
- 把發牌這個動作打包成 function，可以把取得的牌 return 出來
- 每一輪顯示目前手上有什麼牌(連同花式)及總點數(hints：把print這個動作也打包成function)

{% endhint %}

# List 的複製
在Python中，list 的複製不可以直接使用 `=` 符號，是由於 List 在使用等號的時候，只有把 list_1 的地址給予 list_2，因此若我們改變 list_1 的值，list_2也會隨之改變。

```python
list_1 = [1,2,3,4,5]
list_2 = list_1

list_1[0] = 100 # 改變 list_1 index 為 0 的值
print(list_2)   # [100,2,3,4,5] # 列印 list_2
```

## 正確做法
使用 `.copy()`

```python
list_1 = [1,2,3,4,5]
list_2 = list_1.copy()

list_1[0] = 100 # 改變 list_1 index 為 0 的值
print(list_1)   # [100,2,3,4,5] # 列印 list_1
print(list_2)   # [1,2,3,4,5]   # 列印 list_2
```

# 函數 Function
函數(Function)，Python自定了很多不同的已經寫好的Function，所謂函數就是『敘述的集合』，並且以一個函數名稱來代表此敘述集合。

**是一種已組織好的，可以重覆使用的「小工具」或「黑盒子」，實現特定功能的代碼段。**

試想想，為何我們為何能隨時使用 `print()`?

- 是提前寫好的
- 可以重覆使用
- 實現輸出功能的一個功能段

### print() 在 Python 中的定義

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202405211506236.png)

## 自定義函數/方法
由於 python 是自上而下進行編譯和執行，因此定義函數一定要執行(call)函數前完成。
```python
# 定義最簡單的函數
def 函數名():
    需要執行的程式塊

# 執行/call
函數名()
```

定義一個 `print_hello()` 函數，功能是每一次執行時列印2次Hello

```python
def print_hello():
  for i in range(0,2):
    print("Hello")

print_hello()
```

# 自定義函數/方法 - 參數
我們也可以在函數中加入參數，參數作用範圍只在函數有效。

```python
def function_name(參數1, 參數2, 參數3, ...):
    {code}
```

- 參數可以為空

## 例子 : len()
`len()` 方法返回對像（字符、列表、元組等）長度或項目個數。

```python
# 定義一個String
str1 = "My name is Leo Tam."

print(len(str1)) # 這里的 str1 便是參數之一
```

# 參數的意義
以剛才的例子中，我們使用了`range(0,2)`控制迴圈的次數，但試想這個`range()`中每次都寫死了`0,2`，若我希望這個range()內的值是由執行的時候動態決定，我們要如何做？

* **注意：參數的作用範圍僅在函數中**
```python
# 定義最簡單的函數
def print_hello(num1, num2):
  for i in range(num1, num2):
    print("Hello")

print_hello(2, 10)
print_hello(1, 11)
```

## 練習
手寫一個模擬 len() 的方法 count_string()，用於統計傳入的字串string，一共有多少個字元。

<details>

<summary>解答</summary>
解答: 
```python
# 定義 function
def count_string(str1):
    count = 0
    for i in str1:
        count = count + 1

    print(f"你傳入字串:{count}，一共有{count}個字元。")

# 主邏輯區
str_1 = "Hello, World!"

# 執行 function
count_string(str_1)
```

</details>

# 自定義函數/方法 - 返回值
函數除了可以執行一定功能的邏輯外，還可以返回`結果`，並回傳至主函數。

使用 `return` 關鍵字

```python
def 函數名(參數):
    需要執行的程式塊
    return 資料
   
# 在這裡，return 的意義是：結束函式，回傳「資料」
# 這裡的資料我們稱為返回值。
```

```python
def 函數名(參數):
    需要執行的程式塊
    return

# 在這裡，return 後空白的意義是：結束函式，因為沒有定義資料，所以回傳 None
# 這裡的 None 我們稱為返回值。
```

## 接收返回值
我們可以使用變數接收返回值
```python
def count_string(str1):
    count = 0
    for i in str1:
        count = count + 1
    return count

str_1 = "Hello, World!"

count_str1 = count_string(str_1)
# count_string 最終會以 return 方式把結果傳回
# 然後我們使用變數 count_str1 把結果儲存

print(count_str1)
```



# 變數、Function 的順序
我們知道，在變數、Function使用前，必須要進行宣告的動作，對應的功能才可以使用。

## 程式架構順序
在一個正常程式下，宣告的順序如下：
* 由於 function 和 變數 都不會立即執行，因此可交換位置不會影響
* **但全域變數必須放最上方**

```python
####### 宣告區 #######
# 由於 function 和 變數 都不會立即執行，因此可交換位置不會影響(但全域變數必須放最上方)
# 1. 變數
var_1 = "?"
var_2 = "?"

# 2. function 
def function_name(var_1, var_2):
    # code
    return something

####### 主程式/主邏輯區 #######
if(var_1 == var_2):
    print("他們相等")
```

## 變數的作用域
在Python或其他程式語言中也一樣，每一個變數都有屬於它存在的適用範圍，我們稱之為**命名空間(Namespace)**。

如果在最外面(也就是沒有在函式中)命名一個變數的時候，任何人應該都看得到這個變數的存在，並且可以自由使用它，我們稱之為**全域變數(Global)**。但若如果今天這個變數你是在function中宣告的或是臨時變數，則它只在Function中有效，稱為**區域變數(Local)**。

- 全域變數(Global) : 在整個程式中均有效
- 局部變數(Local) : 只在該變數處於的區域有效
- **優先搜索局部變數**

```python
var = 'global' 

def home1():
	print(f"我是在 home1() 中的 print : {var}") # 直接取得全域的變數，不做修改

def home2():
	var = 'Not global' # 定義一個local的變數，所以修改到的變數跟全域的var無關
	print(f"我是在 home2() 中的 print : {var}")
	
def home3():
	global var # 告訴Python現在要用的就是全域的那個var
	var = 'h3'
	print(f"我是在 home3() 中的 print : {var}") # 因此修改後會影響到全域變數的值


print(f'直接輸出全域變數:  {var}')

print()
print(f'執行home1():')
home1()
print(f'完成home1()後的var:  {var}')

print("##############")

print()
print(f'執行home2():')
home2()
print(f'完成home2()後的var:  {var}')

print("##############")

print()
print(f'執行home3():')
home3()
print(f'完成home3()後的var:  {var}')
```

![var](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202505271737105.png)

## 傳值(Value)、還是傳址(Address)的問題
Pass by value and pass by reference問題，在Python中，任何儲存容器的資料類型，在進行參數傳遞時為傳址(Address)

**即 function 中的修改，會直接改變原資料**

**而其他普通參數(int、float、String)等為傳值(Value)**

**只是把值放到參數中，function 不能改變原資料。**


![Img](https://www.mathwarehouse.com/programming/images/pass-by-reference-vs-pass-by-value-animation.gif)

## 1. 傳值(Pass By Value)，即傳入不會改變原有的值
int、float、String 為傳值(Value)
```python
# 傳入的變數為基本資料型態(數值、字串、布林)
def modify(x, y, z):
    x = x + 10
    y = y + " World"
    z = False
    print(f"函數內 : {x}, {y}, {z}")  # 30 Hello False

num1 = 20
string1 = "Hello"
bool1 = True

modify (num1, string1, bool1)
print(f"函數外 : {num1}, {string1}, {bool1}")
```

## 2. 傳址(Pass By Address)，即傳入會改變原有的值
所有容器如列表、字典、集合（list、dict、set 等）都是以傳址方式傳入 Function 中。

```python
def modify_list(lst):
    lst.append(4)
    print(f"函數內:{lst}")  # [1, 2, 3, 4]

my_list = [1, 2, 3]
modify_list(my_list) # 傳遞的是參考，所以會改變原始列表
print(f"函數外:{my_list}")  # [1, 2, 3, 4]（原始列表被修改）
```

---

# Dictionary(字典)
Dictionary 是一種較為複雜的資料結構，對於資料的查找很方便。Python中的字典如同現實世界中的字典，包含了一堆`字`，和這個字所指示的含意，每一個`字`即代表`key`，每一個字對應的的解釋，即代表`value`

在 Python 的字典中，每一個元素都由鍵 (key) 和值 (value) 構成，結構為`key:value` 。不同的元素之間會以逗號分隔，並且以大括號 `{ }` 圍住。

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202403260207827.png)

## 字典宣告:
```python
# 字典變數名 = {key:value}

dict = {key1: value1}
```

## 多個字典的宣告
```python
# 字典變數名 = {key1:value1, key2:value2, key3, value3}

student_eng_score = {
    "Leo": 99,
    "May": 68,
    "Alan": 58
}

student_eng_score ["Leo"]      # 99
student_eng_score ["May"]      # 68
student_eng_score ["Alan"]     # 58
```

## 字典中 Key 的特性
- Key 必須為不可變類型（string、int、float等）
- Key 不能重覆、若重覆則會覆蓋原Value
- Value 可以是任意資料型類，並且可以重覆

```python
temp1 = {3.14 : "我是Pie"}
print(temp1[3.14])   # “我是Pie”


temp2 = {3.14 : "我是Pie", 3.14 : "我是Pie2"}
print(temp2[3.14])  # “我是Pie2”


temp3 = {1:"我是Leo", 2:[1,1,2,3,5,8], "CM540":"Python"}  # 合法宣告
```
## 字典的特性
- 鍵值對(Key : Value)
- 儲存非重覆項目(Key不重覆)
- 沒有順序性，不能靠index進行搜索，只能依懶 Key

## 字典的常用操作
- 存取 key 對應的 value 
- 新增/修改 value
- 刪除 value
- 尋找 / 列出 key 

```python

# 定義一個 dict
fruit = {
    "蘋果":"apple",
    "橙":"orange",
    "香蕉":"banana"
}

# 1. 尋找 key 對應的 value 不出現Error
# get()
rs = fruit.get("蘋果")
print(rs) # apple

rs2 = fruit.get("apple")
# rs2 = fruit["apple"]  # error
print(rs2) # None

# 2. 添加/修改內容
# name[key] = value
# 若 key 不存在，即為新增
# 若 key 存在，即為修改

# 2.1 新增
fruit["藍梅"] = "blueberry"
print(fruit)

# 2.2 修改
fruit["蘋果"] = "Apple"
print(fruit)

# 3. 刪除
# pop(key)
fruit.pop("蘋果")
print(fruit)

# 3.1 pop的參數
# pop(key, "if not found") , return msg
error_msg = fruit.pop("123蘋果", "沒有找到對應的Key")
print(error_msg)

# 4. 尋找 key 是否存在
# in`
flag = "蘋果" in fruit
print(flag)

# 5. 列出所有 key
all_key = fruit.keys()
print(all_key)

for i in all_key:
    print(i)
    print(type(i))

```

# 例外狀況處理: try except
執行 Python 程式的時候，往往會遇到「錯誤」的狀況。如果沒有好好處理錯誤狀況，就會造成整個程式壞掉而停止不動。因此，透過「例外處理」try except 機制。能夠在發生錯誤時進行對應的動作，不僅能保護整個程式的流程，也能夠掌握問題出現的位置，馬上進行修正。

## 錯誤類型

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202403261728234.png)

## 使用 Try 和 Except
```python
try:
    # 需執行的程式碼

except Exception as E:
    # 若有錯誤，錯誤訊息為 E

else:
    # 若沒有錯誤則執行

finally:
    # 不論有沒有錯誤都執行
```

### 例子
```python
a = "Hello"

try:
    b = a + 1 # Error String and Int
except Exception as E:
    print(E)

print("哇，恭喜你的程式可以順利由頭跑到尾")

```

```python
while(True):
    data = input("請輪入一個數字：")

    try:
        num = int(data)
        num = num + 1
        print(f"你輸入的是{num}")
        break
        
    except Exception as E:
        print("輸入錯誤，請重新輸入")
        print(E)
```