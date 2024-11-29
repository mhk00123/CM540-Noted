# temp
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


# pandas
Pandas 是一個強大的資料分析工具包，讓你能夠輕鬆地處理和分析結構化數據。
- 自帶很多不同的 function 可以讀取 xml、json、list、xlsx等資料格式
- 通通轉換為 pandas 專用的格式 dataframe
- 透過 dataframe 可以做出十分多不同的計算，像 Excel 中的`fx`一樣

安裝方式：
```bash
pip install pandas
```

慣用導入方式：
```python
import pandas as pd
```

## Pandas 基礎概念
Pandas 提供了兩種類型的類別來處理資料：

- Series：保存任何類型資料的一維數值組合。例如整數、字串、Python 物件等。
> 可以理解為一維 list

- DataFrame：二維資料結構，用於保存數據，例如二維數組或具有行和列的表格。
> 可以理解為 excel 的狀態


## Series (一維)
- `定義`：Series 是一種一維數據結構，可以存儲任何數據類型（整數、字符串、浮點數、Python 對象等）。每個 Series 都會有一個數據類型來定義其值的類型。
- `索引`：Series 擁有一個索引，預設情況下從 0 開始，也可以自定義索引。
- `創建`：你可以從列表、字典或直接從標量值創建 Series。

```python
import pandas as pd

s = pd.Series([1, 3, 5, 7, 9])
```

## DataFrame (二維)
- `定義`：DataFrame 是一種二維數據結構，類似於 Excel 表格，可以存儲不同類型的列。是 Pandas 最常用的數據結構，適用於表示複雜數據和數據分析。
- `結構`：DataFrame 是由多個 Series 組成，每個 Series 成為 DataFrame 的一列。所有的列可以有不同的數據類型。
- `索引`：和 Series 一樣，DataFrame 也有索引，並且每個索引值對應一行數據。同時，每一列也有標籤（列名）。

### 名詞解釋
- 行 (row) - 打橫
- 列 (columns) - 打直

```python
import pandas as pd

data = {
    'apples': [3, 2, 0, 1],
    'oranges': [0, 3, 7, 2]
}

df = pd.DataFrame(data)
```

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202404191702506.png)

# 行與列

### 每一列(Col)
都會有一個index，可以透過以下方式取得 index 的範圍。
```python 
df.columns
```
> Index(['apples', 'oranges'], dtype='object')

### 每一行(row)
都會有一個index，系統默認為int。可以透過以下方式取得 index 的範圍。
```
df.index
```
> RangeIndex(start=0, stop=4, step=1)

### 取得整列(直)
可透過 dataframe[列名]取得
```python
data_column = df[col_name]
```

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202404191709297.png)

### 取得一整行(橫)
可透過 dataframe.loc[index, column]取得
```python
 data_column = df.loc[1]
```

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202404191723588.png)

# 輸出到 Excel - `to_excel()`
透過 `to_excel(檔案名、表名、是否需要加上index)`

```python
df.to_excel('temp.xlsx', sheet_name='sheet1', index=False)
```

# 一維列表常用的操作 - 切片
對於普通一維陣列，有幾種方法可以單獨對他進行切割工作。
切片的結果是一個新的列表，包含原始列表中指定範圍內的元素。
```python
list[start:end:step]
```
- start：起始索引，指定切片的起始位置（包含）。
- end：結束索引，指定切片的結束位置（不包含）。
- step：步長，指定切片的元素間隔（預設為 1）。
操作與字串切割相似

```python
# list[start:end:step]

cart = ["蘋果", "橙", "藍莓", "香蕉", "鳳梨"]

# 由頭到尾
cart_1 = cart[:] # ["蘋果", "橙", "藍莓", "香蕉", "鳳梨"]

# 取得第 2-4 項元素
cart_2 = cart[2:5] # ["藍莓", "香蕉", "鳳梨"]

# 由頭到尾，跳格取得
cart_3 = cart[::2] # ["蘋果", "藍莓", "鳳梨"]

# 倒轉列表 
cart_4 = cart[::-1] # ["鳳梨", "香蕉", "藍莓", "橙", "蘋果"]

```


# 第三方Module下載 - pip
pip 是 Python 的包管理器，用於安裝和管理第三方庫（也稱為包）的工具。它使你能夠輕松地下載、安裝、升級和卸載 Python 包。

pip 是 Python 2.7.9 版本及其後續版本的標准組件，也是 Python 3.4 及其後續版本的標准組件。它在安裝 Python 解釋器時一同安裝。

## Python pip 基本命令
安裝包：
`pip install package_name`

升級包：
`pip install --upgrade package_name`

卸載包：
`pip uninstall package_name`

顯示已安裝的包：
`pip list`

搜索包：
`pip search package_name`