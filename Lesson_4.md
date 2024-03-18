# Lesson 4 - 函數/方法、儲存容器

**tags: `python`** **`CM-540`** **`Lesson4`**

函數/方法、儲存容器

## Slide

課件：[https://tinyurl.com/5n8vy2nd](https://tinyurl.com/5n8vy2nd)

# 函數 Function
函數(Function)，Python自定了很多不同的已經寫好的Function，所謂函數就是『敘述的集合』，並且以一個函數名稱來代表此敘述集合。
是一種已組織好的，可以重覆使用的，實現特定功能的代碼段。

試想想，為何我們為何能隨時使用 print()  ?
- 是提前寫好的?
- 可以重覆使用?
- 實現輸出功能的一個功能段?

### print() 函數 在 python 中的定義

> 可以在 VS code 中按著 ctrl，再用滑鼠點擊 print

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202403150021636.png)

## 例子 len()
len() 方法返回對像（字符、列表、元組等）長度或項目個數。
```python
# 定義一個String
str1 = "My name is Leo Tam."

# 快速獲得它的長度
len_str1 = len(str1)

print(len_str1) # 19
```

### 練習
不使用 len()，我們手寫一個出來，並統計以下 3 組 String 的長度。
```python
str1 = "My name is Leo Tam."
str2 = "I'm the teacher of CM540."
str3 = "I'm hungry."
```
## 自定義函數/方法
由於 python 是自上而下進行編譯和執行，因此定義函數一定要執行函數前完成。若在沒有定義前，就執行函數，會報錯。

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202403150031027.png)

```python
 # 定義最簡單的函數
def 函數名():
    需要執行的程式塊
# 執行
函數名()

def print_hello():
  for i in range(0,2):
    print("Hello")

print_hello()

```

## 自定義函數/方法 - 參數
我們也可以在函數中加入**參數**和**返回值**，而這 2 個值的作用範圍只在函數有效。
```python
def function_name(參數1, 參數2, 參數3, ...):
    需要執行的程式塊
    return 結果
```
1. 參數可以為空
2. 可以沒有 return 語句，如果沒有 return 語句，函數將返回一個特殊的值 None

### 參數的意義
以剛才的例子，range中每次都寫死了range(0,2)，若我希望這個range()內的值是由執行的時候決定，我們可以這樣改寫
```python
def print_hello(min, max):
  for i in range(min, max):
    print("Hello")

print_hello(2, 10)
print_hello(1, 11)
```
> 參數的作用範圍僅在函數中

## 自定義函數/方法 - 返回值
在函數或方法中，也可以定義一個返回值，讓最後結果可以返回主函式中。
```python
def 函數名(參數):
    需要執行的程式塊
    return
# 在這裡，return 的意義是：結束函式，因為沒有定義資料，所以回傳 None
# 這裡的 None 我們稱為返回值。

def 函數名(參數):
    需要執行的程式塊
    return 資料
   
# 在這裡，return 的意義是：結束函式，回傳「資料」
# 這裡的資料我們稱為返回值。
```

例如我們需要自行寫一個 **相加** 的函數，其中呼叫函數時帶有 2 個參數，然後回傳結果。
```python
def add(a, b):
  sum = a + b
  return sum

print(add(1,5))

# 推薦使用變數裝回
rs = add(1,5)
print(rs)
```

## 作用域

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202403150037768.png)

- 全域變數 : 在整個程式中均有效
- 局部變數 : 只在該變數處於的區域有效
- **程式優先判斷局部變數**

大家可以細閱這段程式碼的結果
```python
# 全域變數 a1, b1, i, j
a1 = 10
b1 = 20
i = 9
j = 10

def add(a1, b1):   
    sum = a1 + b1 # 局部變數 a1, b1
    return sum    # 局部變數 sum


for i in range(0,2):
    print(i)  # 局部變數 i
    print(a1) # 全域變數 a1
```

# 儲存容器
容器的意義：可以容納多份數據、容納的每一份數據可以稱為 1 個元素。

每 1 個元素：可以是任意類型的數據、int、float、String、Bool等。

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202403150043552.png)

容器根據特別不同作區分，如：
- 是否支持重覆元素
- 是否可以對元素中任意值修改
- 是否元素是否有順序 等


## 目前 Python 中儲存容器分為 5 類：
- String
- list (列表)
- dict (字典)
- tuple (元組)
- set (集合)

# 儲存容器 - List(列表、陣列)

List 是 Python 中最基本的數據結構。List 中的每個值都有對應的位置值，稱之為索引(index)，第一個索引是 0，第二個索引是 1，依此類推。

```python
# 定義一個空 List，使用[ ]
list_empty = []

# 定義一個含數據的 List 
list_exp = ["red", "green", "blue", "yellow", "white", "black"]
```

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202403110034722.png)

## List 的特性
1. List 是有順序的，會按照 index 由0、1、2、...下去
2. 存取方式與 string 一樣，使用變數名[index] 進行元素存取
3. 列表的元素不需要具有相同的類型
```python
list_exp = [1 , "green", True] # 這個是合法的
```
4. List 中的元素可以作新增、修改、刪除(後續再詳講)
5. List 是一個迭代對象(iterable)

## 多維列表
Python陣列有多種形式，包括一維陣列、二維陣列和多維陣列。一維陣列類似於列表，而二維陣列則可以想像成一個表格，多維陣列則可以擴展到更高維度的數據。

```python
# 記錄同學信息
leo_tam_M = [65, 88, 13]
alice_chan_M = [99, 100, 102]

# 寫法2
mark_1 = [“Leo Tam”, 65, 88, 13]
mark_2 = [“Alice Chan”, 99, 100, 102]

# 二維方式
# mark = [mark_1, mark_2]

mark = [
    [“Leo Tam”, 65, 88, 13], 
    [“Alice Chan”, 99, 100, 102]
]
```

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202403150047315.png)


### 二維列表存取方式
```python
# 二維方式
# mark = [mark_1, mark_2]
mark = [
    [“Leo Tam”, 65, 88, 13], 
    [“Alice Chan”, 99, 100, 102]
]

print(mark[0][0]) # Leo Tam
print(mark[1][3]) # 102
```

### 二維列表歷遍

```python
# 二維方式
# mark = [mark_1, mark_2]
mark = [
    [“Leo Tam”, 65, 88, 13], 
    [“Alice Chan”, 99, 100, 102]
]

print(mark[0][0]) # Leo Tam
print(mark[1][3]) # 102

```

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202403150047278.png)

## 列表常用的操作和函數(function)
1. 修改特定下標的值
2. 列表長度
3. 查找某元素所在的位置、如查找元素不在會報錯
4. 在指定位置插入一個元素
5. 在列表尾部加入 1 個 元素
6. 在列表尾部加入 1 批 元素
7. 刪除元素
8. 刪除指定元素在List中的第一個匹配項目
9. 清空列表
10. 統計列表內某元素的值

```python
# 1. 修改特定下標的值
# 修改 第3個元素
list_ex[2] = "Ken"

# 2.列表長度
length = len(list_ex)
print(f"列表長度：{length}")

# 3. 查找某元素所在的位置、如查找元素不在會報錯
# index()
# 例如我想查看 May 的位置
index = list_ex.index("May")
print(f"May的index：{index}")

# 4. 在指定index插入一個元素 (會改變整個列表) 
# insert(index, 值)
# 例如我想在 index = 2 的位置插入 "Angela"
print(f"原列表：{list_ex}")
list_ex.insert(2, "Angela")
print(f"修改後的列表：{list_ex}")

# 5. 在列表尾部加入 1 個 元素
# append(值)
# 在最後增加 John
print(f"原列表：{list_ex}")
list_ex.append("John")
print(f"修改後的列表：{list_ex}")


# 6. 在列表尾部加入 1 批 元素
# extend(list)
# 把 list2 加入到 list_ex的最後
print(f"原列表：{list_ex}")
list2 = ["Kate", "Tom", "Ella"]
list_ex.extend(list2)
print(f"修改後的列表：{list_ex}")

# 7. 刪除元素(2種方法)
# 7.1 刪除指定下標的元素
# pop(index)
# 例如我想刪除目前列表第5個元素
print(f"原列表：{list_ex}")
list_ex.pop(5)
print(f"修改後的列表：{list_ex}")

# 8. 刪除指定元素在List中的第一個匹配項目
# remove(值)
# 例如我想要移除 Ella
print(f"原列表：{list_ex}")
list_ex.remove("Ella")
print(f"修改後的列表：{list_ex}")

# 9. 清空列表
# clear()
# print(f"原列表：{list_ex}")
# list_ex.clear()
# print(f"修改後的列表：{list_ex}")

# 10. 統計列表內某元素的值
# count
list_ex = ['Leo', 'Allen', 'Angela', 'Leo', 'Celia', 'Leo', 'Kate', 'Leo']
rs_Leo = list_ex.count("Leo")
print(f"列表中有 {rs_Leo} 個Leo")
```

{% hint style="info" %}
列表的方法功能有非常多，但不建議硬記，學習編程，不僅是語言本身，以後會根據個人興趣向不同方向發展

除了經常使用的，大多是靠記憶記不下來的。

我們只需要有一個較為模糊的印像，知道大約有這些用法就可以。

若有需要，請隨時Google即可! 
{% endhint %}


# 堂上練習+功課 : 21 點遊戲修正

繳交：[https://tinyurl.com/23ywzyhj](https://tinyurl.com/23ywzyhj)

- 扑克牌(52張) :1 - 13 表示
- 每個數字最多 4 隻

## 我們要做的：
- 每 1  輪人手發牌 - 指定點數
- 若輸入超過 4 張牌，請玩家重新輸入
- 記錄點數，點數是累加的
- 記錄點數必須引導玩家繼續發牌
- 若剛好等於 21 點，贏了，遊戲結束
- 若大於 21 點，輸了，遊戲結束
- 輸入 `bye` 遊戲結束妥

