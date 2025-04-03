# Lesson 10 - 爬蟲、Pandas

**tags: `python`** **`CM-540`** **`Lesson10`**

# Slide
課件：[https://docs.google.com/presentation/d/1BF94gb2vS1jGLhQZnxqJqZX7QN86bvyLvhei7uCcxhU/edit?usp=sharing](https://docs.google.com/presentation/d/1BF94gb2vS1jGLhQZnxqJqZX7QN86bvyLvhei7uCcxhU/edit?usp=sharing)

# Final Project
[https://hamster.cpttm.org.mo/spaces/feCAHUOGzzpHSwzd-DKvGg/upload](https://hamster.cpttm.org.mo/spaces/feCAHUOGzzpHSwzd-DKvGg/upload)

Deadline：2024-12-20 23:59

# Requests 中加入 header

透過 payload 變數加入所需的認證參數，以 dict 型式記錄
在 requests 的參數中加入 headers

```python
import requests

url = "https://dsat.apigateway.data.gov.mo/car_park_maintance"

payload = {
    "Authorization": "APPCODE 09d43a591fba407fb862412970667de4"
}

response = requests.get(url, headers = payload)
```

## 取得交通事務局中的資料
```python
import requests
import xmltodict
import json
 
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
print(target_data)

# 7. 輸出到 txt 方便放到 pareser中
with open("data.txt", "w", encoding="utf-8") as myfile:
    write_data = json.dumps(data_dict, ensure_ascii=False)
    myfile.write(write_data)
```

## XML練習：尋找目前澳門沒有電單車車位的停車場
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
    if(i["@MB_CNT"] == "" or i["@MB_CNT"] == "0"):
        print(f'{i["@name"]} - 沒有電單車停車場')
```

# json
json 檔案一開始於用 javascript 中，是一種輕量級的資料交換格式。它的使用範圍很廣，並成為ECMA 標準，可以使用在多種程式語言中，用於前後端之間的資料傳輸、儲存和交換資料。可以說是“用更少的編碼，有更快的處理速度”，所以深受廣大程式設計師的喜愛。

json 格式以 `{ }` 作為開始，如有新一層也是以`{ }`分開並加上 `,`，結束和python的dict相似。

```json
{
    "person information" : {
        "name": "Leo Tam",
        "age": 27,
        "city": "Macau"
    },
    
    "company information" : {
        "name": "CPTTM",
        "title": "Teacher"
    }
}
```

## Python中讀取json、輸出json

Python 自帶讀取json格式的module：`json`

- 讀取 (loads)、轉換成 `json` 格式
- 輸出 (dumps)、由 `json` 轉換為 `string`
```python
import json

file = open('test.json', encoding='utf-8')

data = json.loads(file)

dump_data = json.dumps(data)

with open("data.txt", "w",encoding="utf-8") as my_file:
    # json中含有utf-8的操作
    write_data = json.dumps(dump_data, ensure_ascii=False)
    my_file.write(write_data)
```

## 民航局-澳門國際機場航班時間表 API 
[https://data.gov.mo/Detail?id=ea50a770-cc35-47cc-a3ba-7f60092d4bc4](https://data.gov.mo/Detail?id=ea50a770-cc35-47cc-a3ba-7f60092d4bc4)

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202406032302183.png)


# 練習 - 尋找所有目的地為北京的航班
```python
import requests
import xmltodict
import json

# 1. 目標 url
url = "https://aacm.apigateway.data.gov.mo/api/open/listFlightTimetable"

# 2. Header
headers = {
    "Authorization": "APPCODE 09d43a591fba407fb862412970667de4"
}

# 3. 向目標發送請求(request)
response = requests.get(url, headers=headers)

print(response)

# 4. 讀取 response 並進行 utf-8 decode
# 使用 loads
json_data = json.loads(response.content)

# 5. 尋找目的地為北京的 Beijing 的所有航空
for i in json_data:
    if("Beijin" in i['destination']):
        print(f"{i['airline']} - {i['weekDay']}，航行周期：{i['periodStartDate']} 至 {i['periodEndDate']}")
```

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
