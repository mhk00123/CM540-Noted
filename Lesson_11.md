# Lesson 11 - Pandas、Matplotlib

**tags: `python`** **`CM-540`** **`Lesson11`**

## Slide
課件：[https://tinyurl.com/3nnxxcs7](https://tinyurl.com/3nnxxcs7)

# Pandas 操作

### Data
```python
import pandas as pd

data = [
    {'姓名': 'Leo', '年紀': 24, '工作': '工程師'},
    {'姓名': 'Alice', '年紀': 30, '工作': '設計師'},
    {'姓名': 'Tom', '年紀': 28, '工作': '老師'},
    {'姓名': 'Mary', '年紀': 24, '工作': '學生'},
    {'姓名': 'Ken', '年紀': 28, '工作': '工程師'},
    {'姓名': 'Leo Tam', '年紀': 28, '工作': '老師'},
]

df = pd.DataFrame(data)
```

## 增加列 (Column)
在 Pandas 中，增加列較為簡單，只需要使用仍未使用的列index即可
```python
# 語法
df[new_col_index] = newData
```
```python
import pandas as pd

data = [
    {'姓名': 'Leo', '年紀': 24, '工作': '工程師'},
    {'姓名': 'Alice', '年紀': 30, '工作': '設計師'},
    {'姓名': 'Tom', '年紀': 28, '工作': '老師'},
    {'姓名': 'Mary', '年紀': 24, '工作': '學生'},
    {'姓名': 'Ken', '年紀': 28, '工作': '工程師'},
    {'姓名': 'Leo Tam', '年紀': 28, '工作': '老師'},
]

df = pd.DataFrame(data)

# 新增列 (Column)
new_col = ["M","L","M","L","M","M"]
df["sex"] = new_col
```

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202404231512386.png)


## 增加行 (Row)
增加行則較為麻煩，需要使用`concat`函數，有2個參數`新和舊的DataFrame`、`ignore_index`
```python
df = pd.concat([df, df_new], ignore_index = True/False)
```

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202404231518744.png)


```python
import pandas as pd

data = [
    {'姓名': 'Leo', '年紀': 24, '工作': '工程師'},
    {'姓名': 'Alice', '年紀': 30, '工作': '設計師'},
    {'姓名': 'Tom', '年紀': 28, '工作': '老師'},
    {'姓名': 'Mary', '年紀': 24, '工作': '學生'},
    {'姓名': 'Ken', '年紀': 28, '工作': '工程師'},
    {'姓名': 'Leo Tam', '年紀': 28, '工作': '老師'},
]

df = pd.DataFrame(data)

# 新增列 (Column)
new_col = ["M","L","M","L","M","M"]
df["sex"] = new_col

# 新增行 (Row)
new_row = [
            {
              '姓名': 'CPTTM', 
              '年紀': 50,
              '工作': '教育中心',
              'sex':None
            }
          ]

df2 = pd.DataFrame(new_row)

df = pd.concat([df, df2], ignore_index = True)
```

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202404231518104.png)

## 定位到某行 (Row)
可以使用 df.loc[條件]
```python
df.loc[條件]
```
```python
import pandas as pd

data = [
    {'姓名': 'Leo', '年紀': 24, '工作': '工程師'},
    {'姓名': 'Alice', '年紀': 30, '工作': '設計師'},
    {'姓名': 'Tom', '年紀': 28, '工作': '老師'},
    {'姓名': 'Mary', '年紀': 24, '工作': '學生'},
    {'姓名': 'Ken', '年紀': 28, '工作': '工程師'},
    {'姓名': 'Leo Tam', '年紀': 28, '工作': '老師'},
]

df = pd.DataFrame(data)

# 尋找所有 工作 為 工程師 的數據
df.loc[df["工作"] == "工程師"]
```

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202404231542206.png)

# 刪除行Drop
我們可以指定特定行/列進行刪除

## 刪除行 Row (常用)
可以使用 `drop(index)`
```python
df = df.drop(index = "row_index")
```

```python
df.loc[條件]
```
```python
import pandas as pd

data = [
    {'姓名': 'Leo', '年紀': 24, '工作': '工程師'},
    {'姓名': 'Alice', '年紀': 30, '工作': '設計師'},
    {'姓名': 'Tom', '年紀': 28, '工作': '老師'},
    {'姓名': 'Mary', '年紀': 24, '工作': '學生'},
    {'姓名': 'Ken', '年紀': 28, '工作': '工程師'},
    {'姓名': 'Leo Tam', '年紀': 28, '工作': '老師'},
]

df = pd.DataFrame(data)

# 刪除最後新增的 CPTTM 
df = df.drop(index = 6)
```

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202404231618982.png)

刪除`工作`為`工程師`的行
```python
#1. 先尋找工作為工程師的行index
target = df[df["工作"] == "工程師"].index.tolist()

#2. 刪除該 index 所在的 Row
df = df.drop(target)
```

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202404231625224.png)

# 統計函式
- 共有幾行 - len( )
```pyton
count_row = len(df)
```

- 平均值 - mean( )
```pyton
avg_age = df.loc[:, "年紀"].mean()
```

- 最小 - min( )
```pyton
min_age = df["年紀"].min()
```

- 最大 - max( )
```pyton
max_age = df["年紀"].max()
```

- 定位行 - df [ 條件判斷 ]
```pyton
df[df["年紀"] == max_age]
```

## 統計區間 - group_by()
我們可以透過 group_by( ) 為我們的數據作分區區間，但一般來說我們無法可視化這個 group by 後的數據。
```python
df.groupby("年紀")
```
使用.size( ) 查看每一個 group 的數量
```python
count_by_age = df.groupby('年紀').size()
```

```python
import pandas as pd

data = [
    {'姓名': 'Leo', '年紀': 24, '工作': '工程師'},
    {'姓名': 'Alice', '年紀': 30, '工作': '設計師'},
    {'姓名': 'Tom', '年紀': 28, '工作': '老師'},
    {'姓名': 'Mary', '年紀': 24, '工作': '學生'},
    {'姓名': 'Ken', '年紀': 28, '工作': '工程師'},
    {'姓名': 'Leo Tam', '年紀': 28, '工作': '老師'},
]

df = pd.DataFrame(data)

df.groupby("年紀")
count_by_age = df.groupby('年紀').size()
```

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202404231655684.png)

## 統計區間 - pd.cut( )
除了使用 group_by( )，我們也可以使用 cut( ) 為資料進行指定的區間劃分。
```python
pd.cut(col_index, bins, labels, right)
```

```python
import pandas as pd

data = [
    {'姓名': 'Leo', '年紀': 24, '工作': '工程師'},
    {'姓名': 'Alice', '年紀': 30, '工作': '設計師'},
    {'姓名': 'Tom', '年紀': 28, '工作': '老師'},
    {'姓名': 'Mary', '年紀': 24, '工作': '學生'},
    {'姓名': 'Ken', '年紀': 28, '工作': '工程師'},
    {'姓名': 'Leo Tam', '年紀': 28, '工作': '老師'},
]

df = pd.DataFrame(data)

bins_area = [0, 20, 25, 30, 35]
labels = ['0-20', '21-25', '26-30', '31-35']
df['年齡區間'] = pd.cut(df['年紀'], bins=bins_area, labels=labels, right=False)
```

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202404231657591.png)

# 資料可視化 Matplotlib
Matplotlib 是一個 python 2D 繪圖庫，主要用作為資料進行可視化處理。
Matplotlib、Pandas、Numpy 這三個 module 便是Python中處理大數據最好的工具。
由於Matplotlib中包含大量不同的參數，本課程由於屬入門課程，只能帶大家入門使用。
```python
import matplotlib.pyplot as plt
```
## 可以繪製的圖表：
https://matplotlib.org/stable/plot_types/basic/index.html

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202404231703990.png)

## 在pandas中使用`plot()`
由於在Pandas中已有整合部份Matplotlib功能，只要我們能提供x, y軸資料。
便能快速地繪製圖表。

```python
import pandas as pd
 
data = [
    {'姓名': 'Leo', '年紀': 24, '工作': '工程師'},
    {'姓名': 'Alice', '年紀': 30, '工作': '設計師'},
    {'姓名': 'Tom', '年紀': 28, '工作': '老師'},
    {'姓名': 'Mary', '年紀': 24, '工作': '學生'},
    {'姓名': 'Ken', '年紀': 28, '工作': '工程師'},
    {'姓名': 'Leo Tam', '年紀': 28, '工作': '老師'},
]
 
df = pd.DataFrame(data)

count_by_age = df.groupby('年紀').size()
count_by_age
count_by_age.plot(kind='bar')
```

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202404231707789.png)

## 區間分組
```python
import pandas as pd
 
data = [
    {'姓名': 'Leo', '年紀': 24, '工作': '工程師'},
    {'姓名': 'Alice', '年紀': 30, '工作': '設計師'},
    {'姓名': 'Tom', '年紀': 28, '工作': '老師'},
    {'姓名': 'Mary', '年紀': 24, '工作': '學生'},
    {'姓名': 'Ken', '年紀': 28, '工作': '工程師'},
    {'姓名': 'Leo Tam', '年紀': 28, '工作': '老師'},
]
 
df = pd.DataFrame(data)

bins_area = [0, 20, 25, 30, 35]
labels = ['0-20', '21-25', '26-30', '31-35']
df['年齡區間'] = pd.cut(df['年紀'], bins=bins_area, labels=labels, right=False)
count_by_age_range = df.groupby('年齡區間').size()
count_by_age_range.plot(kind='bar')
```

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202404231709079.png)
