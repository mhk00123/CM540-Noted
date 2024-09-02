# Lesson 11 - Pandas、Matplotlib

**tags: `python`** **`CM-540`** **`Lesson11`**

# Slide
課件：[https://docs.google.com/presentation/d/1tPwN2reYVnsRwWkYHi2gzdvIP7XgC_3Ll9mgeiyupv8/edit?usp=sharing](https://docs.google.com/presentation/d/1tPwN2reYVnsRwWkYHi2gzdvIP7XgC_3Ll9mgeiyupv8/edit?usp=sharing)

# Final Project
繳交：[https://hamster.cpttm.org.mo/spaces/NCUIE40Tcbd1LcgcdqUUsw/upload](https://hamster.cpttm.org.mo/spaces/NCUIE40Tcbd1LcgcdqUUsw/upload)



# Pandas 操作
## 範例 Data
```python
import pandas as pd
df = pd.DataFrame(
    {
      '產品': ['蘋果','奇異果','檸檬','牛排','肥牛','豬腩肉','雞翅膀','奶酪','牛奶'],
      '種類': ['水果','水果','水果','肉類','肉類','肉類','肉類','奶製品','奶製品'],
      '保存方式': ['新鮮','新鮮','新鮮','新鮮','冷藏','冷藏','新鮮','冷藏','新鮮'],
      '原產地': ['本地','進口','本地','本地','進口','進口','本地','本地','本地'],
      '位址': ['貨區 A1','貨區 A3','貨區 A1','貨區 A2','貨區 B2','貨區 B1','貨區 A4','貨區 B2','貨區 A1'],
      '原價': [3.6, 6.3, 2.4, 10.3, 16.6, 8.5, 6.6, 5.3, 2.4],
      '優惠價': [3.4, 5.7, 1.9, 10.2, 13.9, 7.9, 5.2, 5.1, 1.9],
      '貨存': [67, 70, 80, 98, 91, 40, 70, 86, 72],
    }    
)
```

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202406111122707.png)


## 統計函式
- 共有幾行 - len( )
```python
count_row = len(df)
```

- 平均值 - mean( )
```python
avg_price = df.loc[:, "原價"].mean()
```

- 最小 - min( )
```python
min_price = df["原價"].min()
```

- 最大 - max( )
```python
max_price = df["原價"].max()
```

- 定位行 - df [ 條件判斷 ]
```python
df.loc[df["原價"] == max_price]
```

## 統計區間 - group_by()
我們可以透過 group_by( ) 為我們的數據作分區區間，但一般來說我們無法可視化這個 group by 後的數據。
```python
df.groupby(by=[col_name1, col_name2]).agg({col_name : func1, col_name : func2})
```
使用.size( ) 查看每一個 group 的數量
```python
count_by_fruit = df.groupby(by="種類").size()
```


```python
import pandas as pd

df = pd.DataFrame(
    {
      '產品': ['蘋果','奇異果','檸檬','牛排','肥牛','豬腩肉','雞翅膀','奶酪','牛奶'],
      '種類': ['水果','水果','水果','肉類','肉類','肉類','肉類','奶製品','奶製品'],
      '保存方式': ['新鮮','新鮮','新鮮','新鮮','冷藏','冷藏','新鮮','冷藏','新鮮'],
      '原產地': ['本地','進口','本地','本地','進口','進口','本地','本地','本地'],
      '位址': ['貨區 A1','貨區 A3','貨區 A1','貨區 A2','貨區 B2','貨區 B1','貨區 A4','貨區 B2','貨區 A1'],
      '原價': [3.6, 6.3, 2.4, 10.3, 16.6, 8.5, 6.6, 5.3, 2.4],
      '優惠價': [3.4, 5.7, 1.9, 10.2, 13.9, 7.9, 5.2, 5.1, 1.9],
      '貨存': [67, 70, 80, 98, 91, 40, 70, 86, 72],
    }    
)

count_by_fruit = df.groupby(by="種類").size()
count_by_fruit
```
![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202406111204927.png)

## groupby function
將會用到 `.agg({"col_name":"value".function})`
agg中，使用 dict {列名:函數}
| 數據的處理 | 描述 |
| :--: | :--: |
| `{'col_name': sum}` | 計算這一列裡，每個分組的總和 |
| `{'col_name': min}` | 找出這一列裡，每個分組的最小值 |
| `{'col_name': max}` | 找出這一列裡，每個分組的最大值 |
| `{'col_name': np.mean}` | 計算這一列裡，每個分組的平均值 |
| `{'col_name': std}` | 計算這一列裡，每個分組的標準差 |
| `{'col_name': median}` | 找出這一列裡，每個分組的中位數 |


## 尋找每個組別的數量

```python
df.groupby(by="種類").agg({"產品": len})
```

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202406111254180.png)

## 將文字組合成一行
```python
df.groupby(by="種類").agg({"產品": ", ".join})
```

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202406111253631.png)


## 統計區間 - pd.cut( )
除了使用 group_by( )，我們也可以使用 cut( ) 為資料進行指定的區間劃分。
```python
pd.cut(col_index, bins, labels, right)
```

```python
import pandas as pd

import pandas as pd
df = pd.DataFrame(
    {
      '產品': ['蘋果','奇異果','檸檬','牛排','肥牛','豬腩肉','雞翅膀','奶酪','牛奶'],
      '種類': ['水果','水果','水果','肉類','肉類','肉類','肉類','奶製品','奶製品'],
      '保存方式': ['新鮮','新鮮','新鮮','新鮮','冷藏','冷藏','新鮮','冷藏','新鮮'],
      '原產地': ['本地','進口','本地','本地','進口','進口','本地','本地','本地'],
      '位址': ['貨區 A1','貨區 A3','貨區 A1','貨區 A2','貨區 B2','貨區 B1','貨區 A4','貨區 B2','貨區 A1'],
      '原價': [3.6, 6.3, 2.4, 10.3, 16.6, 8.5, 6.6, 5.3, 2.4],
      '優惠價': [3.4, 5.7, 1.9, 10.2, 13.9, 7.9, 5.2, 5.1, 1.9],
      '貨存': [67, 70, 80, 98, 91, 40, 70, 86, 72],
    }    
)

bins_area = [0,30,60,90,120]
labels = ['缺貨', '需要補貨', '充足', '非常充足']
df['貨存狀態'] = pd.cut(df['貨存'], bins=bins_area, labels=labels, right=False)
df
```

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202406111509265.png)


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

## 設置中文化(colab)
```python
# 在Colab 中添下以下字行

!wget -O TaipeiSansTCBeta-Regular.ttf https://drive.google.com/uc?id=1eGAsTN1HBpJAkeVM57_C7ccp7hbgSz3_&export=download
import matplotlib
matplotlib.font_manager.fontManager.addfont('TaipeiSansTCBeta-Regular.ttf')
matplotlib.rc('font', family='Taipei Sans TC Beta')
```

## 設置中文化(VS Code)
```python
import matplotlib
import matplotlib.font_manager
import matplotlib.pyplot as plt
import pandas as pd

matplotlib.font_manager.fontManager.addfont('TaipeiSansTCBeta-Regular.ttf')
matplotlib.rc('font', family='Taipei Sans TC Beta')
```


## 畫圖
需要使用 matplotlib
```python
import matplotlib.pyplot as plt

df.plot(kind="line")
```

```python
import pandas as pd
import matplotlib.pyplot as plt

df = pd.DataFrame(
    {
      '產品': ['蘋果','奇異果','檸檬','牛排','肥牛','豬腩肉','雞翅膀','奶酪','牛奶'],
      '種類': ['水果','水果','水果','肉類','肉類','肉類','肉類','奶製品','奶製品'],
      '保存方式': ['新鮮','新鮮','新鮮','新鮮','冷藏','冷藏','新鮮','冷藏','新鮮'],
      '原產地': ['本地','進口','本地','本地','進口','進口','本地','本地','本地'],
      '位址': ['貨區 A1','貨區 A3','貨區 A1','貨區 A2','貨區 B2','貨區 B1','貨區 A4','貨區 B2','貨區 A1'],
      '原價': [3.6, 6.3, 2.4, 10.3, 16.6, 8.5, 6.6, 5.3, 2.4],
      '優惠價': [3.4, 5.7, 1.9, 10.2, 13.9, 7.9, 5.2, 5.1, 1.9],
      '貨存': [67, 70, 80, 98, 91, 40, 70, 86, 72],
    }    
)

# 先產品設置至 X 軸
df = df.set_index("產品")

# 透過.plot(kind="")畫出圖表
# 使用 VS Code 的話需要使用 plt.show()
df.plot(kind='line')
plt.show()
```

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202406111601850.png)


## 分類畫圖(group by)
```python
count_by_fruit = df.groupby(by="種類").agg({"種類":len})
count_by_fruit.plot(kind="bar")
plt.show()
```

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202406111602337.png)


## 對比原價、優惠價
```python
df2 = pd.DataFrame(df, columns=["產品", "原價", "優惠價"])
df2 = df2.set_index("產品")
df2.plot(kind="line")
plt.show()
```

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202406111609404.png)

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202406111609463.png)


## 儲存畫好的圖 savefig()
```python
# dpi = 輸出圖片的大小
plt.savefig("draw_plot.png", dpi=250)
```
