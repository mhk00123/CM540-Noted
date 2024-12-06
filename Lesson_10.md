# Lesson 10 - 爬蟲、Pandas

**tags: `python`** **`CM-540`** **`Lesson10`**

# Slide
課件：[https://docs.google.com/presentation/d/1BF94gb2vS1jGLhQZnxqJqZX7QN86bvyLvhei7uCcxhU/edit?usp=sharing](https://docs.google.com/presentation/d/1BF94gb2vS1jGLhQZnxqJqZX7QN86bvyLvhei7uCcxhU/edit?usp=sharing)

# Final Project
[https://hamster.cpttm.org.mo/spaces/feCAHUOGzzpHSwzd-DKvGg/upload](https://hamster.cpttm.org.mo/spaces/feCAHUOGzzpHSwzd-DKvGg/upload)

Deadline：2024-12-20 23:59

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



# 爬取 TDM 新聞
TDM 新聞提供 API 我們可以直接調用。
> https://www.tdm.com.mo/api/v1.0/news?IsShowSevenDay=true&Type=image&Date={日期}&Lang=zh
```python
import requests
import json

# 1. date_list
date_list = ["2023-06-01","2023-06-02","2023-06-03","2023-06-04"]

for day in date_list:

    # 1. 目標 url
    url = f"https://www.tdm.com.mo/api/v1.0/news?IsShowSevenDay=true&Type=image&Date={day}&Lang=zh"

    # 2. 向目標發送請求(request)
    response = requests.get(url)

    json_data = json.loads(response.content)

    target_data = json_data["data"]["newsList"]

    for i in target_data:
        for j in i["data"]:
            print(f'{j["date"]} : {j["title"]}')
            print(f'{j["content"]}')
            print("######################")
```

# Google Colab 是什麼？ 
Google Colaboratory 是一個基於雲端的Python開發環境，提供免費的GPU和TPU資源，讓用戶可以在網頁瀏覽器中運行和編寫Python程式。它具有強大的協作功能，可以與他人共享和編輯程式碼。Google Colab支援Jupyter筆記本，並提供預裝的Python套件，方便進行數據分析、機器學習等任務。

- 不必進行任何設定
- 免付費使用 GPU
- 輕鬆共用

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202406070016218.png)

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202406070937761.png)

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
- **若有設置索引，則索引 = index**
- `創建`：你可以從列表、字典或直接從標量值創建 Series。

```python
import pandas as pd

sites = {1: "Google", 2: "Yahoo", 3: "Wiki"}

myvar = pd.Series(sites, index = [1, 2])

myvar

myvar[1] # Google
```

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202406071506098.png)


## DataFrame (二維)
- `定義`：DataFrame 是一種二維數據結構，類似於 Excel 表格，可以存儲不同類型的列。是 Pandas 最常用的數據結構，適用於表示複雜數據和數據分析。
- `結構`：DataFrame 是由多個 Series 組成，每個 Series 成為 DataFrame 的一列。所有的列可以有不同的數據類型。
- `索引`：和 Series 一樣，DataFrame 也有索引，並且每個索引值對應一行數據。同時，每一列也有標籤（列名）。

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202406071500427.png)


### 名詞解釋
- 行 (row) - 打橫
- 列 (columns) - 打直

## 創建 DataFrame

### 由 Dict 創建
```python
import pandas as pd

data = [
    {'name': 'Leo', 'age': 18, 'work': '工程師'},
    {'name': 'Mary', 'age': 25, 'work': '設計師'},
    {'name': 'Ken', 'age': 28, 'work': '老師'}
]
df = pd.DataFrame(data)

```
![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202406071440164.png)

### 由 List 創建
```python
rows = [
    ['Leo', 18, '工程師'],
    ['Mary', 25, '設計師'],
    ['Ken', 28, '老師']
]
col_names = ['name', 'age', 'work']
df = pd.DataFrame(rows, columns=col_names)
df
```

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202406071446493.png)


# 行與列

### 每一列(Col)
都會有一個index，可以透過以下方式取得 index 的範圍。
```python 
df.columns
```

### 每一行(row)
都會有一個index，系統默認為int。可以透過以下方式取得 index 的範圍。
```
df.index
```

#### 總共有多少行
```python
len(df)
```


### 取得整列(直)
可透過 dataframe[列名]取得
```python
data_column = df[col_name]
```

![](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202406071441921.png)

### 取得一整行(橫)
可透過 dataframe.loc[index, column]取得
```python
 data_column = df.loc[1]
```

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202404191723588.png)


## DataFrame 取得列(Col)資料
在 Pandas 中，取得 DataFrame 中的特定欄位（列）數據可以使用多種方法。以下是一些常見的方法：

```python
# 假設 df 是一個 DataFrame
rows = [
    ['Leo', 18, '工程師'],
    ['Mary', 25, '設計師'],
    ['Ken', 28, '老師']
]
col_names = ['name', 'age', 'work']
df = pd.DataFrame(rows, columns=col_names)

df["name"]
# 或
df.name
```

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202406071516044.png)


## DataFrame 取得行(Row)資料
以行定位，需要使用`.loc[row_index][col_index]`

- loc[]: 基於列的欄位名稱取得列。
- iloc[]: 基於列的整數位置（index）來取得列。

```python
rows = [
    ['Leo', 18, '工程師'],
    ['Mary', 25, '設計師'],
    ['Ken', 28, '老師']
]
col_names = ['name', 'age', 'work']
df = pd.DataFrame(rows, columns=col_names)

# 取得一行
df.loc[0]

# 取得指定值
df.loc[0]["name"] # Leo
# 或
df.iloc[0][0] # Leo
```

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202406071546293.png)

## 條件定位
我們可以直接對行/列數據進行每個分析
```python
# 判列所有 age 列中元素是否大於20，會返回一個 True / False的值
df["age"] > 20

```
![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202406071553241.png)

同時我們可以用 `loc[]`方式把所有True的值列出
```python
df.loc[df["age"] > 20]
```

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202406071555006.png)

也可以多條件判斷語法較為特殊，and `&`， or `|`
```python
df.loc[(df["age"] > 20) & (df["work"] == "設計師")]
```

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202406071557633.png)

## Pandas raed()功能
Pandas 提供強大的read功能：
- json : `pd.raed_json()`
- xml : `pd.raed_xml()`
- csv : `pd.raed_csv()`
- xlsx : `pd.raed_xlsx()`

以上這些檔案都可以被 pandas直接讀取並轉換為DataFrame格式

## 讀取交通事務局停車場資訊
-  XML

```python
import pandas as pd
import requests

url = "https://dsat.apigateway.data.gov.mo/car_park_maintance"
headers = {
    "Authorization": "APPCODE 09d43a591fba407fb862412970667de4"
}
response = requests.get(url, headers=headers)

df = pd.read_xml(response.content)
df
```

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202406071621326.png)

### 定位 MB_CNT 為 NaN 的值
``` python
# 判斷
df["MB_CNT"].isnull()

# 定位
df[df["MB_CNT"].isnull()]
```
![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202406071625416.png)

## 缺失值(NaN)處理
可以使用 2 種方法
1. 填充
2. 刪除行

```python
# 使用固定值填充
df = df.fillna(value)

# 2 刪除行
df = df.dropna()
```

```python
df["MB_CNT"] = df["MB_CNT"].fillna(0)
df
```

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202406071634500.png)

## 整理數據後 - 輸出至 Excel to_excel()
透過to_excel(檔案名、表名、是否需要加上index)
```python
df.to_excel('temp.xlsx', sheet_name='沒有電單車位的停車場', index=False)
```

## 課堂練習

尋找私家車停位 < 20 的停車場，並輸出至 Excel

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

df = df.loc[df["Car_CNT"] < 20]

df.to_excel("output.xlsx", index=False)
```

