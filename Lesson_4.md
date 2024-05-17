# Lesson 4 - 儲存容器

**tags: `python`** **`CM-540`** **`Lesson4`**

函數/方法、儲存容器

## Slide

課件：[https://docs.google.com/presentation/d/1TA_VG_QN7NaPTX-RQXtA1tl86_b0GSyAtfa-BC40y1g/edit?usp=sharing](https://docs.google.com/presentation/d/1TA_VG_QN7NaPTX-RQXtA1tl86_b0GSyAtfa-BC40y1g/edit?usp=sharing)


# 儲存容器
容器的意義：可以容納多份數據、容納的每一份數據可以稱為 1 個元素。

每 1 個元素：可以是任意類型的數據、int、float、String、Bool等。

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202403150043552.png)

## 為什麼要使用儲存容器?
儲存容器可以看在一個購物車，這個購物車中可以放入各種不同類型的商品，做到集合的作用。

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202405171048874.png)


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

### 一維列表存取 所有 元素
由於 list 為可代物件，因此我們可以使用 for 迴圈訪問每一個元素
```python
shopping_cart = ["蘋果", "橙", "藍莓", "香蕉", "鳳梨"]

for i in shopping_cart:
    print(i)
```

## 多維列表
Python陣列有多種形式，包括一維陣列、二維陣列和多維陣列。一維陣列類似於列表，而二維陣列則可以想像成一個表格，多維陣列則可以擴展到更高維度的數據。

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