# Lesson 5 - 儲存容器、Function、排序演算法

**tags: `python`** **`CM-540`** **`Lesson5`**

儲存容器、Function、排序演算法

# Slide
[https://docs.google.com/presentation/d/1SHZm3jpyAL2EsYFXPe944Z-mqsmDCwbEjc32wopYKss/edit?usp=sharing](https://docs.google.com/presentation/d/1SHZm3jpyAL2EsYFXPe944Z-mqsmDCwbEjc32wopYKss/edit?usp=sharing)

# 功課：21 點遊戲單人版(Version2)
我們對verion1 的程式碼進行重構，繳交網址：
[[Link](https://hamster.cpttm.org.mo/spaces/D0zskV6HZGBIk6CI9ApoQA/upload)](https://hamster.cpttm.org.mo/spaces/D0zskV6HZGBIk6CI9ApoQA/upload)

截止日期：2025-03-13

我們要做的：
- 以 list 方式把所有牌分開花式及點數(hints：二維list)
- 每 1 輪發牌 - 改以 `Random` 方式
- 把發牌這個動作打包成 function，可以把取得的牌 return 出來
- 每一輪顯示目前手上有什麼牌(連同花式)及總點數(hints：把print這個動作也打包成function)



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

## 一維列表(常用)

```python
shopping_cart = ["蘋果", "橙", "藍莓", "香蕉", "鳳梨"]
```

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202405171051443.png)

### 一維列表存取 1 個元素
一維列表是有順序的，可以透過`列表名[index]`取得1個元素

```python
shopping_cart[0] # 蘋果
shopping_cart[1] # 橙
shopping_cart[2] # 藍莓
shopping_cart[3] # 香蕉
shopping_cart[4] # 鳳梨
```

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202405171053836.png)

### 一維列表存取所有元素
由於 list 為可代物件，因此我們可以使用 for 迴圈訪問每一個元素
```python
shopping_cart = ["蘋果", "橙", "藍莓", "香蕉", "鳳梨"]

for i in shopping_cart:
    print(i)
```

## 多維列表
Python陣列有多種形式，包括一維陣列、二維陣列和多維陣列。一維陣列類似於列表，而二維陣列則可以想像成一個表格，多維陣列則可以擴展到更高維度的數據。

```python
list_all = [
    list1[], list2[], list3[], ...
]
```


![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202405171058555.png)


```python
cart = [
    ["蘋果", "橙", "藍莓", "香蕉", "鳳梨"],
    ["橙", "蘋果", "鳳梨", "藍莓", "香蕉"],
    ["橙", "香蕉", "香蕉"]
]
```
![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202405171059334.png)


### 二維列表存取方式
```python
cart = [
    ["蘋果", "橙", "藍莓", "香蕉", "鳳梨"],
    ["橙", "蘋果", "鳳梨", "藍莓", "香蕉"],
    ["橙", "香蕉", "香蕉"]
]

# 列表名[行][列]
# 第 2 行、第 2 個元素 - 蘋果
cart[1][1]

# 第 3 行、第 1 個元素 - 橙
cart[2][0]
```

### 二維列表歷遍

```python
cart = [
    ["蘋果", "橙", "藍莓", "香蕉", "鳳梨"],
    ["橙", "蘋果", "鳳梨", "藍莓", "香蕉"],
    ["橙", "香蕉", "香蕉"]
]

# for 迴圈
for row in cart:
    for col in row:
        print(col)
```

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
list_ex = ["Tom", "Kate", "Mart", "Leo"]
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

# 4. 在列表尾部加入 1 個 元素 (超常用)
# append()
# 在最後增加 John
print(f"原列表：{list_ex}")
list_ex.append("John")
print(f"修改後的列表：{list_ex}")

# 5. 在指定index插入一個元素 (會改變整個列表) 
# insert(index, 值)
# 例如我想在 index = 2 的位置插入 "Angela"
print(f"原列表：{list_ex}")
list_ex.insert(2, "Angela")
print(f"修改後的列表：{list_ex}")

# 6. 兩列表合併
# list1.extend(list2)
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
# remove()
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
# count()
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


# 一維列表常用的操作 - 排序
我們可以在列中使用`.sort()`函數進行快速的排序操作。
其中、可以透過參數`reverse`控制由大到小還是由小到大。
```python
cart = [2, 1, 3, 8, 5]

# sort function # 由小至大(默認)
cart.sort(reverse=False) #[1,2,3,5,8]

# sort function # 由大到小
cart.sort(reverse=True) #[8,5,3,2,1]
```

# 練習
輸入 N 個數字，輸入”bye”時結束，按順序輸入到表(List)中。

1. 輸出列表
2. 輸出用戶共輸入了多少個數字
3. 排列整組數據( 按小到大 )
4. 排列整組數據( 按大到小 )
5. 最小的數、最大的數
6. 此組數據的平均值

```python
# 1. 定義 1 個空list
list_num = []

# 2. 循環輸入
while(True):
    temp = input("請輸入數字：") # type:String
    if(temp == "bye"): # 如果輸入的的為 bye 則跳出迴圈
        break
    else:
        user_input = int(temp)
        list_num.append(user_input)

# 3.1 輸出列表 
print(f"列表：{list_num}")

# 3.2 輸出用戶共輸入了多少個數字
length_list_num = len(list_num)
print(f"用戶共輸入了 {length_list_num} 個數字")

# 3.3 排列整組數據( 按小到大 )
temp_1 = list_num
temp_1.sort()
print(f"排列整組數據(按小到大)：{temp_1}")

# 3.4 排列整組數據( 按大到小 )
temp_2 = list_num[::-1]
print(f"排列整組數據(按大到小)：{temp_2}")

# 3.5 最小的數、最大的數
min = list_num[0]
max = list_num[0]

for item in list_num:
    if(item < min):
        min = item
    if(item > max):
        max = item

print(f"列表中最小的值是：{min}")
print(f"列表中最大的值是：{max}")

# 3.6 此組數據的平均值
sum = 0
for item in list_num:
    sum = sum + item

avg_list_num = sum / len(list_num)

print(f"此列表的平均值為：{avg_list_num}")
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

### len() 
len() 方法返回對像（字符、列表、元組等）長度或項目個數。

```python
# 定義一個String
str1 = "My name is Leo Tam."

# 快速獲得它的長度
len_str1 = len(str1)

print(len_str1) # 19
```

### 練習
不使用 `len()`，我們嘗試手寫一個出來，並計算以下 1 組 String 的總長度。

```python
str1 = "My name is Leo Tam."
str2 = "My name is Leo Tam 12345."
```
解：
```python
str1 = "My name is Leo Tam."
str2 = "My name is Leo Tam 12345."

count = 0
for i in str1:
  count = count + 1

print(f"str1的字串長度為{count}")

count = 0
for i in str2:
    count = count + 1

print(f"str2的字串長度為{count}")
```

## 自定義函數/方法
由於 python 是自上而下進行編譯和執行，因此定義函數一定要執行函數前完成。
```python
# 定義最簡單的函數
def 函數名():
    需要執行的程式塊

# 執行
函數名()
```
```python
def print_hello():
  for i in range(0,2):
    print("Hello")

print_hello()
```

## 自定義函數/方法 - 參數、返回值
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

```Python
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

## 練習：自製 `len()` 函數
```python
def len_handmade(?):
    {code?}
    
str1 = "My name is Leo Tam."
str2 = "I'm the teacher of CM540."
str3 = "I'm hungry."

print(len_handmade(str1)) # 數字： str1的長度
print(len_handmade(str2)) # 數字： str2的長度
print(len_handmade(str3)) # 數字： str3的長度
```

```python
def len_handmade(input_string):
    count = 0 
    for i in input_string:
        count = count + 1
    return count
```

# 演算法
「演算法」這三個字近幾年可說是相當的火熱，感覺很容易就會聽到 youtube、facebook 又改演算法啦，也會很常聽見人家在討論什麼人工智慧演算法之類的。 
在聽了很多人云亦云的概念後，那麼到底什麼是演算法? ​
如果我們從定義上來看：

**由有限步驟所構成的集合，可以用於解決某一個特定的問題。**

假設我們今天要解決的那一個特定問題是「把蘋果做成一杯蘋果汁」
那我們可以透過以下幾個步驟來實現：
1. 清洗蘋果
2. 將蘋果削皮、去籽
3. 將 經過步驟 (2) 處理的蘋果 放入果汁機
4. 在果汁機中加入一定比例的水
5. 按下果汁機啟動按鈕
6. 將果汁機裡面的蘋果汁倒入玻璃杯中

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202405211615444.jpg)

我們可以把剛才那6個步驟叫作 " 把蘋果做成一杯蘋果汁 " 的演算法。

而在電腦科學的領域也是如此，透過設計一連串的指令、動作，讓電腦去執行，以便協助我們解決一些特定問題。

而演算法就是一種解決問題的邏輯思維！這樣的思維邏輯可以用文字，或者透過代碼、流程圖、電子電路、數學等等之類的​方式做描述。

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202405211616861.png)


## 著名的排序演算法：冒泡排序（Bubble Sort）
冒泡排序（Bubble Sort）也是一種簡單直觀的排序算法。

他會反複地歷遍要排序的列表，一次比較兩個元素，如果他們的順序錯誤就把他們交換過來。歷遍數列的工作是重覆地進行直到沒有數字需交換，即表示列表已經排序完成。

1. 測量列表的長度(i)，列表長度為比較回合總數
2. 測量每回合需要比較的次數(j-i-1)
3. 每一輪循環中由左至右比較兩個元素arr[j]、arr[j+1]，如果如果arr[j]比arr[j+1]大就把他們交換過來，否則不用理會。
4. 每一輪結束後，整個列表最大的值應會在右手面。
5. 重覆步驟3

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202405211620013.png)

### 交換操作
```python
if arr[j] > arr[j+1]:
    temp = arr[j]
    arr[j] = arr[j+1]
    arr[j+1] = temp
```

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202405211631085.png)


## 堂上練習：實現 bubble sort
```python
def bubbleSort(arr):
    # 步驟1. 測量列表的長度
    for i in range(0, len(arr)): 
        # 步驟2. 測量每回合需要比較的次數(j-i-1)
        for j in range(0, len(arr)-i-1):
            #步驟3. 
            if arr[j] > arr[j+1]:
                temp = arr[j]
                arr[j] = arr[j+1]
                arr[j+1] = temp
    return arr

list_ex = [4,6,8,1,32,6,2,4,8,9,11]

print(bubbleSort(list_ex))
```