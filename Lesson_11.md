# Lesson 11 - Pandas、Matplotlib、總結

**tags: `python`** **`CM-540`** **`Lesson11`**

# Slide
課件：[https://docs.google.com/presentation/d/1tPwN2reYVnsRwWkYHi2gzdvIP7XgC_3Ll9mgeiyupv8/edit?usp=sharing](https://docs.google.com/presentation/d/1tPwN2reYVnsRwWkYHi2gzdvIP7XgC_3Ll9mgeiyupv8/edit?usp=sharing)

# 作業：
截止時間：2025年6月29日 23:59

{% hint style="info" %}

# Final Project

繳交網址：[https://hamster.cpttm.org.mo/spaces/9iOIDsZc7TLVbref_Ot8AQ/upload](https://hamster.cpttm.org.mo/spaces/9iOIDsZc7TLVbref_Ot8AQ/upload)

自己思考一個題目，任何類型
- 小算盤?
- 待辦行事記錄?
- 資料分析? 停車場車位一些應用?
- 自動檢查退休基金價格?
- 檢查政府工什麼時候開考?
- OCR 應用    

{% endhint %}


# Pandas 缺失值處理
在我們使用pd.read()讀取資料時，有部份資料值存在空白、缺失的情況
![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202506161733655.png)

而在 Pandas 中，我們可以快速處理缺失值

## 定位 NaN 的值
可透過 `df.isnull()`，與早前定位一樣，先寫條件，再定位

``` python
# condition
condition = df[列名稱].isnull()

# 定位
df[condition]
```

``` python
# 判斷 Condition
condition = df["MB_CNT"].isnull()

# 定位
df[condition]
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
# 自己 = 自己代表取代原數據
df["MB_CNT"] = df["MB_CNT"].fillna(0)
```

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202406071634500.png)

# 刪除目標資料
我們可以指定特定行/列進行刪除

```python
# 刪除列(Col)
df = df.drop(columns = "col_index")

# 刪除行(Row)
df = df.drop(index = "row_index")
```

### 刪除Row
由於刪除特定行需要尋找對應的 Row index
可以先定位，再用對應的function定位對應的Row Index

例如 : 刪除所有名稱中包含氹仔的停車場
```python
# 1. 包含某文字的寫法
condition = df["name"].str.contains("氹仔", na=False)

# 1.1 如果為非包含 ==
# condition = df["name"] == "氹仔"

# 2. 尋找對應的 Row index
target_index = df[condition].index.tolist()

# 3. 刪除 row
df = df.drop(index=target_index)
```

## 整理數據後 - 輸出至 Excel to_excel()
透過to_excel(檔案名、表名、是否需要加上index)
```python
df.to_excel('temp.xlsx', sheet_name='test_sheet', index=False)
```

# 資料可視化 Matplotlib
Matplotlib 是一個 python 2D 繪圖庫，主要用作為資料進行可視化處理。
Matplotlib、Pandas、Numpy 這三個 module 便是Python中處理大數據最好的工具。
由於Matplotlib中包含大量不同的參數，本課程由於屬入門課程，只能帶大家入門使用。
```python
import matplotlib
import matplotlib.pyplot as plt
```
## 可以繪製的圖表：
[https://matplotlib.org/stable/plot_types/basic/index.html](https://matplotlib.org/stable/plot_types/basic/index.html)

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202404231703990.png)

## 使用 Matplotlib 的兩個方法
1. 自己生成x,y軸資料，透過 Matplotlib 畫出
2. 直接在Pandas中使用由於在Pandas中已有整合部份Matplotlib功能，只要我們能提供x, y軸資料，便能快速地繪製圖表。

## 設置中文化(colab)
在Colab 中添下以下字行
```python
# 下載台北思源黑體
!wget -O TaipeiSansTCBeta-Regular.ttf https://drive.google.com/uc?id=1eGAsTN1HBpJAkeVM57_C7ccp7hbgSz3_&export=download

import matplotlib
import matplotlib.pyplot as plt 
from matplotlib.font_manager import fontManager

fontManager.addfont('TaipeiSansTCBeta-Regular.ttf')
matplotlib.rc('font', family='Taipei Sans TC Beta')
```

## 設置中文化(VS Code)
```python
import matplotlib
import matplotlib.pyplot as plt

matplotlib.rc('font', family='Microsoft JhengHei')
```

## 1. 使用 Matplotlib 畫圖(線性圖)  `plt.plot()`
需要使用 matplotlib中的 `plt.plot()`
```python
import matplotlib
import matplotlib.pyplot as plt
matplotlib.rc('font', family='Microsoft JhengHei')

## 數據
x = [1, 2, 3, 4, 5]
y = [2, 4, 6, 8, 10]

## 創建圖表(plot 線性圖)
plt.plot(x, y , marker='o', linestyle='-')
## 添加圖例

## 添加標簽和標題
plt.xlabel('X 軸')
plt.ylabel('Y 軸')
plt.title('Test Plot 圖')

## 顯示圖表
plt.show()
```

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202506170105449.png)


## 1. 使用 Matplotlib 畫圖(柱狀圖) `plt.bar()`
需要使用 matplotlib中的 `plt.bar()`
```python
import matplotlib
import matplotlib.pyplot as plt
matplotlib.rc('font', family='Microsoft JhengHei')

## 數據
x = [1, 2, 3, 4, 5]
y = [2, 4, 6, 8, 10]

## 創建圖表(plot 線性圖)
plt.bar(x, y, color='blue')
## 添加圖例

## 添加標簽和標題
plt.xlabel('X 軸')
plt.ylabel('Y 軸')
plt.title('Test Plot 圖')

## 顯示圖表
plt.show()
```

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202506170118223.png)


## 2. 透過Pandas中的內建功能畫圖 `df.plot()`
該方法需要使用對應的 DataFrame Function，因此要先建立好 DataFrame 才可以畫圖。

Ex : 統計暨普查局 : 就業人口月工作收入中位數
Link : [https://data.gov.mo/Detail?id=00d591b9-781c-4583-a440-896e9e89d9fc](https://data.gov.mo/Detail?id=00d591b9-781c-4583-a440-896e9e89d9fc)

1. 先取得資料
- target_url : `https://dsec.apigateway.data.gov.mo/public/KeyIndicator/MedianMonthlyEmploymentEarnOfTheEmployed`
- request method : `POST`
- return type : `json`

```python
import matplotlib
import matplotlib.pyplot as plt
import requests
import json
import pandas as pd

matplotlib.rc('font', family='Microsoft JhengHei')

target_url = 'https://dsec.apigateway.data.gov.mo/public/KeyIndicator/MedianMonthlyEmploymentEarnOfTheEmployed'

playload = {
    'Authorization' : 'APPCODE 09d43a591fba407fb862412970667de4'
}

rs = requests.post(target_url, headers=playload)

# 解釋資料直至可以轉換為 dataframe

json_data = json.loads(rs.text)

target_json_data = json_data['value']['values'] # 是一個 list

df = pd.DataFrame(target_json_data)

print(df)
```

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202506170136057.png)

簡單處理數據，由於畫圖需要所有資料均為數字，此處把`string`轉為`int`
```python
df["value"] = df["value"].astype(int)
```

最後透過`df.plot()`畫出對應圖，系統會自動尋找可以畫圖的數據
另外 x 軸為對應的 row_index
```python
import matplotlib
import matplotlib.pyplot as plt
import requests
import json
import pandas as pd

matplotlib.rc('font', family='Microsoft JhengHei')

target_url = 'https://dsec.apigateway.data.gov.mo/public/KeyIndicator/MedianMonthlyEmploymentEarnOfTheEmployed'

playload = {
    'Authorization' : 'APPCODE 09d43a591fba407fb862412970667de4'
}

rs = requests.post(target_url, headers=playload)

json_data = json.loads(rs.text)

target_json_data = json_data['value']['values'] # list

df = pd.DataFrame(target_json_data)

df["value"] = df["value"].astype(int)

df.plot(marker='o', grid=True)

plt.show()
```

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202506170200996.png)

## 儲存圖片 `plt.save()`
可透過 `plt.save()` 完成儲存

```python
plt.savefig("draw_plot.png", dpi=250)
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


# (補充)如何透過 Python 程式向手機發送通知
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

