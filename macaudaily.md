# 爬取澳門日報

```python
import requests
from bs4 import BeautifulSoup
from datetime import datetime

######################### Step 1 : 尋找報紙所有頁面中的 Links #########################

# 0. 用戶輸入日期
day_get = input("請輸入日期（格式：YYYY-MM-DD）：")
date_obj = datetime.strptime(day_get, "%Y-%m-%d")

# 格式化為 YYYY-MM/DD
formatted_date = f"{date_obj.year}-{date_obj.month:02}/{date_obj.day:02}"
print(formatted_date)
# 1. 目標 url
url = f"http://macaodaily.com/html/{formatted_date}/node_2.htm"
print(url)

# 2. 向目標發送請求(request)
response = requests.get(url)
html_data = response.content.decode("utf-8")
soup = BeautifulSoup(html_data, "html.parser") 

# 3. 找出所有右方table中的link

page_links = []
tables = soup.find_all(id='pageLink') #定位 id = "pageLink" 的 Table td

for td in tables: # 按照網頁結構，每個Table中也包含 Table，用 For 迴圈處理
    href = td.get("href")
    p_link = f"http://macaodaily.com/html/{formatted_date}/{href}"
    page_links.append(p_link)

print(page_links)

######################### Step 2 : 每一個版面進行訪問取得文章連結 #########################

target_links = []
for page_link in page_links:
    url = page_link
    response = requests.get(url)
    html_data = response.content.decode("utf-8")
    soup = BeautifulSoup(html_data, "html.parser")
    tables = soup.find_all('table')

    count = 0
    for i in tables[5]:
        try:
            links = i.find_all("a") # 由於return 回來的 HTML 不純正，會包含\n，因此會出Error
        except:
            continue # 若 Error 則遇到 \n，跳過即可
        
        for target in links:
            try:
                href = target.find("div")["id"][2:] # 由於return 回來的 HTML 不純正，會包含\n，因此會出Error
            except:
                continue # 若 Error 則遇到 \n，跳過即可
            
            p_link = f"http://macaodaily.com/html/{formatted_date}/content_{href}.htm"

            target_links.append(p_link)
            print(p_link)

print(target_links)

######################### Step 3 : 訪問每一文章連結取得文章內容 #########################

with open("news.txt", "w", encoding="utf-8") as myFile:
    for target_link in target_links:        
        url = target_link
        response = requests.get(url)
        html_data = response.content.decode("utf-8")
        soup = BeautifulSoup(html_data, "html.parser")
        tables = soup.find('founder-content')
        
        print("###################################")
        print(target_link)
        myFile.write("\n###################################\n")
        myFile.write(f"{target_link}\n\n")
        
        for i in tables:
            t_text = i.getText()
            print(t_text)
            myFile.write(f"{t_text}\n")
            
        print("###################################")      
        myFile.write("\n###################################\n")
```
