# Lesson 11 - Pandas、Matplotlib

**tags: `python`** **`CM-540`** **`Lesson11`**

# Slide
課件：[https://docs.google.com/presentation/d/1tPwN2reYVnsRwWkYHi2gzdvIP7XgC_3Ll9mgeiyupv8/edit?usp=sharing](https://docs.google.com/presentation/d/1tPwN2reYVnsRwWkYHi2gzdvIP7XgC_3Ll9mgeiyupv8/edit?usp=sharing)

# Final Project
[https://hamster.cpttm.org.mo/spaces/Dw-FRBOph8D3-_oV4r2qFQ/upload](https://hamster.cpttm.org.mo/spaces/Dw-FRBOph8D3-_oV4r2qFQ/upload)

Deadline：2025-04-18 23:59

# Pandas 統計操作
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

## 新增行列

### 新增行(Row)
內容為List、轉換為DataFrame
```python
# 構建新行
# 構建新行
new_data = ["橙", "水果", "新鮮", "進口", "貨區A3", 10, 8, 56]
new_data2 = {
    "產品":"橙2",
    "種類":"水果",
    "保存方式":"新鮮",
    "原產地":"本地",
    "位址":"貨區 A4",
    "原價":20,
    "優惠價":18.5,
    "貨存":56
}
new_row = pd.DataFrame([new_data], columns=df.columns)
new_row2 = pd.DataFrame([new_data2], columns=df.columns)

# 合併 concat()
df = pd.concat([df, new_row, new_row2], ignore_index=True)
df
```

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202410221604987.png)

### 新增列
```python
new_col = pd.Series([11,22,33,44,55,66,77,88,99,100])
df["已售出"] = new_col
```
![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202410221618356.png)

## 刪除  drop()
```python
# 刪除行(Row)
df = df.drop(index = "row_index")

# 刪除列(Col)
df = df.drop(columns = "col_name")
```

## 常用函式
- 輸出Series為list()
```python
df["某列"].tolist()
```

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


## groupby function
在group by中，我們可以直接使用 for 迴圈存取里面每一個項目。

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

count_by_fruit = df.groupby(by="種類")

for group, content in count_by_fruit:
    print(group)
    print(content)

```


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

## 練習

```python
import pandas as pd
import requests

url = "https://dsat.apigateway.data.gov.mo/car_park_maintance"
headers = {
    "Authorization": "APPCODE 09d43a591fba407fb862412970667de4"
}
response = requests.get(url, headers=headers)

df = pd.read_xml(response.content)

df["Car_CNT"] = df["Car_CNT"].fillna(0)
df["MB_CNT"] = df["MB_CNT"].fillna(0)

labels = ["車位嚴重不足", "車位不足", "車位尚可", "車位充足", "車位非常充足"]
df['私家車位狀態'] = pd.cut(df['Car_CNT'], bins=5, labels=labels, right=False)

result = len(df.loc[df["私家車位狀態"] == "車位不足"])
print(f"車位尚可的停車場數量為 {result} 個")

```


# 資料可視化 Matplotlib
Matplotlib 是一個 python 2D 繪圖庫，主要用作為資料進行可視化處理。
Matplotlib、Pandas、Numpy 這三個 module 便是Python中處理大數據最好的工具。
由於Matplotlib中包含大量不同的參數，本課程由於屬入門課程，只能帶大家入門使用。
```python
import matplotlib.pyplot as plt
```
## 可以繪製的圖表：
[https://matplotlib.org/stable/plot_types/basic/index.html](https://matplotlib.org/stable/plot_types/basic/index.html)

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

## 練習：
整合交通事務局的資料，把私家車停車位大於1000的去除，透過並貼上標籤
```python
bins = [0, 10, 30, 50, 1000]
labels = ["車位嚴重不足", "車位不足", "車位尚可", "車位充足", "車位非常充足"]
```
最終透過畫圖方式展示目前車位狀態。

示意圖：

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202412102105542.png)

```python
import pandas as pd
import requests
import matplotlib.pyplot as plt

url = "https://dsat.apigateway.data.gov.mo/car_park_maintance"
headers = {
    "Authorization": "APPCODE 09d43a591fba407fb862412970667de4"
}
response = requests.get(url, headers=headers)

df = pd.read_xml(response.content)

df["Car_CNT"] = df["Car_CNT"].fillna(0)
df["MB_CNT"] = df["MB_CNT"].fillna(0)

condition = df["Car_CNT"] > 1000
target_index = df.loc[condition].index.tolist()
df = df.drop(index = target_index)

bins = [0, 10, 30, 50, 1000]
labels = ["車位嚴重不足", "車位不足", "車位尚可", "車位充足", "車位非常充足"]
df['私家車位狀態'] = pd.cut(df['Car_CNT'], bins=5, labels=labels, right=False)

df2 = df.groupby("私家車位狀態").size()
df2.plot(kind="bar")
plt.show()
```

## (補充)如何透過 Python 程式向手機發送通知
首先，要向自己的手機發送信息是十分困難的!

由於手機系統中有著非常多的認證機制，以現階段我們的知識未具備以撰寫可通過驗證的程式。

因此我們需要透過第三方工具協助，目前適用於Telegram、微信。
- Telegram：開放API，可直接透過Telegram官方API向指定的群組發送推送。
```python
import requests

def telegram_bot_sendtext(bot_message):

    bot_token = 'your_token'
    bot_chatID = 'your_chatID'
    send_text = 'https://api.telegram.org/bot' + bot_token + '/sendMessage?chat_id=' + bot_chatID + '&parse_mode=Markdown&text=' + bot_message

    response = requests.get(send_text)

    return response.json()
```

- 微信：透過第三應用 `pushplus` 向特定微信帳戶 (pushplus) 發送`post`推送。
```python
def wechat_bot_sendtext(bot_message):

    payload = {
            'token' : 'your_token',
            'content': bot_message
        }
    response = requests.post('http://www.pushplus.plus/send', data=payload)
    
    return response
```

# 如何打包程式碼為可執行檔(exe)
由於在windows中，我們大部份可執行檔都是`.exe`的文件，因此我們也希望，我們最終的程式碼可以打包成為一個`.exe`文件以供執行。

我們將使用 `pyinstaller` module進行打包工作。

1. 打開 Anaconda Prompt
2. 切換到 `py311` 環境
```bash
activate py311
```
3. 安裝 `pyinstaller` module
```bash
pip install pyinstaller
```

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202412060937844.png)


4. 透過 `cd` 命令進入 `.py` 文件所在的資料夾，例如目前程式碼檔案放在 `D:\Code\Blackjack` 中。
5. 如切換盤符(由C->D)，需要先打一次目的地的盤符才可以完成切換。

```bash
D:
cd D:\Code\Blackjack
```

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202412060942943.png)

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202412060944221.png)

6. 透過打包命令，打包對應的執行環境、module文件
`pyinstaller --onefile 文件名`
```bash
pyinstaller --onefile blackjack.py
```
![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202412060946299.png)

7. 最終生成 `build`、`dist`資料夾，及`blackjack.spec`文件。而我們需要的.exe文件則存放在`dict`文件夾中。

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202412060947575.png)

8. 加入專屬logo(.ico)
```bash
pyinstaller --clean --onefile --icon="logo.ico" blackjack.py
```
![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202412061603226.png)
