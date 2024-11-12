# Lesson 5 - 儲存容器、Function、排序演算法

**tags: `python`** **`CM-540`** **`Lesson5`**

儲存容器、Function、排序演算法


- 
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
# 函數 Function
函數(Function)，Python自定了很多不同的已經寫好的Function，所謂函數就是『敘述的集合』，並且以一個函數名稱來代表此敘述集合。

**是一種已組織好的，可以重覆使用的，實現特定功能的代碼段。**

試想想，為何我們為何能隨時使用 `print()`?

- 是提前寫好的?
- 可以重覆使用?
- 實現輸出功能的一個功能段?

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
不使用 `len()`，我們嘗試手寫一個出來，並計算以下 3 組 String 的總長度。

```python
str1 = "My name is Leo Tam."
str2 = "I'm the teacher of CM540."
str3 = "I'm hungry."
```
解：
```python
str1 = "My name is Leo Tam."
str2 = "I'm the teacher of CM540."
str3 = "I'm hungry."

count = 0
for i in str1:
  count = count + 1

print(f"str1的字串長度為{count}")

count = 0
for i in str2:
  count = count + 1

print(f"str2的字串長度為{count}")

count = 0
for i in str3:
  count = count + 1

print(f"str3的字串長度為{count}")
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

## 傳值(Value)、還是傳址(Address)的問題
Pass by value and pass by reference問題，在Python中，任何儲存容器的資料類型，在進行參數傳遞時為傳址(Address)

**即 function 中的修改，會直接改變原資料**

而其他普通參數(int、float)等為傳值(Value)

**只是把值放到參數中，function 不能改變原資料。**


![Img](https://www.mathwarehouse.com/programming/images/pass-by-reference-vs-pass-by-value-animation.gif)

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


# 堂上練習+功課 : 21 點遊戲單人版
- 扑克牌(52張)：1 - 13 表示(暫不分開花色)
- 每個數字最多 4 隻

我們要做的：
- 每 1 輪人手發牌 - 指定點數
- 若輸入超過 4 張牌，請玩家重新輸入
- 記錄點數，點數是累加的
- 記錄點數必須引導玩家繼續發牌
- 若剛好等於 21 點，贏了，遊戲結束
- 若大於 21 點，輸了，遊戲結束
- 輸入 bye 遊戲結束
