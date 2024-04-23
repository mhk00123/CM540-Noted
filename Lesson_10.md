# Lesson 10 - 停車場API、Pandas

**tags: `python`** **`CM-540`** **`Lesson10`**

## Slide
課件：[https://tinyurl.com/bdd9s85t](https://tinyurl.com/bdd9s85t)

# 需驗證的 API
目前我們所遇到的API，一般都是可以直接發送 request 得到 response。因為這些 API 都沒有經過加密，因此我們才可以輕易取得資料。

而實際上，有更多的API是需要透過認證才可以取得資料的。

### 交通事務局 API 

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202404191649488.png)


API Link : [https://dsat.apigateway.data.gov.mo/car_park_maintance](https://dsat.apigateway.data.gov.mo/car_park_maintance)

調用 API 參數：
```
Authorization：APPCODE 09d43a591fba407fb862412970667de4
```
這組 `key` : `value` 正是驗證所需要的資料，我們需要在發送 requests 時附帶這組參數在 header (表頭)中。

## Postman - 測試 API 工具
Postman 為一個測試 API request、response的工具，可以網站、API、伺服器等發送 requests 並附帶各種參數。

Postman : [https://www.postman.com/](https://www.postman.com/)

Postman可以在發送的 requests 中加入需要 header:

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202404191651300.png)

加入 header 後，API通過驗證後便會回傳 response：

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202404191651237.png)

## 在 Requests 中加入 Header
在 Python 的 Requests 套件中，我們可以透過以下方式插入 header: 

透過 payload 變數加入所需的認證參數，以 dict 型式記錄

```python
import requests

url = "https://dsat.apigateway.data.gov.mo/car_park_maintance"

payload = {
    "Authorization": "APPCODE 09d43a591fba407fb862412970667de4"
}

response = requests.get(url, headers = payload)
```

## 交通局 API Response
讀取交通局 Response
```python
import requests
import xmltodict

# 1. 目標 url
url = "https://dsat.apigateway.data.gov.mo/car_park_maintance"

# 2. Header
headers = {
    "Authorization": "APPCODE 09d43a591fba407fb862412970667de4"
}

# 3. 向目標發送請求(request)
response = requests.get(url, headers=headers)

# 4. 讀取 response 並進行 utf-8 decode
xml_data = response.content.decode("utf-8")

# 5. 透過 xmltodict 把 xml 轉換為 dict
data_dict = xmltodict.parse(xml_data)

# 6. 尋找 target 標籤
target_data = data_dict['CarPark']['Car_park_info']

for i in target_data:
    print(i)
```

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
