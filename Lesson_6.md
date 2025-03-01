# Lesson 6 - 儲存容器 - Dictionary、錯誤捕捉

**tags: `python`** **`CM-540`** **`Lesson6`**

Dictionary、錯誤捕捉、21點遊戲

## Slide
課件：[https://docs.google.com/presentation/d/1P6d7MLJ2wQ575pxFVLx80tfqFBggMq8CJRwg9EzeZO0/edit?usp=sharing](https://docs.google.com/presentation/d/1P6d7MLJ2wQ575pxFVLx80tfqFBggMq8CJRwg9EzeZO0/edit?usp=sharing)

# 功課：21 點遊戲單人版(Version2.5)
我們對verion2 的程式碼再進行重構，繳交網址：
[https://hamster.cpttm.org.mo/spaces/8YqV6pIa1T0I7rpnVUKBTQ/upload](https://hamster.cpttm.org.mo/spaces/8YqV6pIa1T0I7rpnVUKBTQ/upload)

截止日期：2024-11-26
1. 把牌組分開花式 (提示：使用 dict 加 list 的組合)
2. 加入判斷：取得J、Q、K時全部定義作10點(+10

# 自定義函數/方法 - 參數、返回值
我們也可以在函數中加入參數和返回值，而這2個值的作用範圍只在函數有效。

```python
def function_name(參數1, 參數2, 參數3, ...):
    {code}
    return 結果
```

- 參數可以為空
- 函數可以沒有 return 語句，如果沒有 return 語句，函數將返回一個特殊的值 None

## 參數的意義
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

## 作用域
- 全域變數 : 在整個程式中均有效
- 局部變數 : 只在該變數處於的區域有效
- 優先搜索局部變數

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202405211534155.png)

```python
def test_value_ref(a, b):
    a = a.append(4)
    b = b + 1

a_list = [1,2,3]
b_int = 1

print("執行function前")
print(a_list)
print(b_int)
print("--------")

test_value_ref(a_list, b_int)

print("執行function後")
print(a_list)
print(b_int)
print("--------")
```

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202404161653002.png)


## 傳值(Value)、還是傳址(Address)的問題
Pass by value and pass by reference問題，在Python中，任何儲存容器的資料類型，在進行參數傳遞時為傳址(Address)

**即 function 中的修改，會直接改變原資料**

而其他普通參數(int、float)等為傳值(Value)

**只是把值放到參數中，function 不能改變原資料。**


![Img](https://www.mathwarehouse.com/programming/images/pass-by-reference-vs-pass-by-value-animation.gif)

```python
def modify_list(lst):
    lst.append(4)  # 修改可變對象

def reassign_value(x):
    x = 10  # 只是改變了局部變量的引用

my_list = [1, 2, 3]
modify_list(my_list)
print(my_list)  # 輸出: [1, 2, 3, 4]

value = 5
reassign_value(value)
print(value)  # 輸出: 5
```


## 返回值(return)

### return 後空白
```python
def 函數名(參數):
    {code}
    return
# 在這裡，return 的意義是：結束函式，因為沒有定義資料，所以回傳 None
# 這裡的 None 我們稱為返回值。
```

### return 帶變數
```python
def 函數名(參數):
    {code}
    return 資料

# 在這裡，return 的意義是：結束函式，回傳「資料」
# 這裡的資料我們稱為返回值。
```
```python
def add(a, b):
  sum = a + b
  return sum

print(add(1,5))

# 推薦使用變數裝回
rs = add(1,5)
print(rs)
```

# 什麼時候會使用到 Dictionary(字典) 呢 ?
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


