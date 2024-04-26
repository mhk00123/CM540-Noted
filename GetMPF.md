# Get MPF

該程式由 3 組 程式碼組成
共有 3 個檔案，需要安裝所有套件才可以正常執行。
- main.py
- get_fulankelam.py
- sd_telegram.py

## main.py
```python
import gspread
from requests_html import HTMLSession
from datetime import date
from sd_telegram import telegram_bot_sendtext
from get_fulankelam import *
import os

url = 'https://www.mpfm.com.mo/cn/index.php'

session = HTMLSession()

r = session.get(url)
print(r)
r.html.render()

rs = r.html.find('.fund_table')[0].text
rs_s = rs.split()

print(rs)

AnYu_price = rs_s[2]
ShingYui_price = rs_s[11]

print(type(AnYu_price))
print(type(ShingYui_price))
print(AnYu_price)

today = str(date.today())

fulanke_price = gt_fulankelam()

# Update At google Sheet

gc = gspread.service_account(filename='service_account.json')
sh = gc.open("退休基金")
wks = sh.worksheet("總表")

val_ShingYui = wks.acell('D4')
val_AnYu = wks.acell('F4')
val_fulankelam = wks.acell("H4")

# AnYu 安裕
wks.update('F4', [[AnYu_price]])
2023
# ShingYui 昇悅
wks.update('D4', [[ShingYui_price]])

# Date
wks.update('I4', [[today]])

# Fulankelam
wks.update('H4', [[fulanke_price]])

# My Price
my_st_value = wks.acell('B4').value
my_st_earn = wks.acell('B7').value
my_st_percent = wks.acell('B8').value

gov_st_value = wks.acell('C4').value
gov_st_earn = wks.acell('C7').value
gov_st_percent = wks.acell('C8').value

comp_st_value = wks.acell('E4').value
comp_st_earn = wks.acell('E7').value
comp_st_percent = wks.acell('E8').value

all_value = wks.acell('B13').value
all_percent = wks.acell('B14').value

fu_value = wks.acell('G4').value
fu_earn = wks.acell('C13').value
fu_percent = wks.acell('C14').value
print(fu_earn)
print(fu_percent)

sd_text_my_st = '我的昇悅St : ' + str(my_st_value) + ' | ' + str(my_st_earn) +' | ' + str(my_st_percent)
sd_text_gov_st = '政府的昇悅 : ' + str(gov_st_value) + ' | ' + str(gov_st_earn) +' | ' + str(gov_st_percent)
sd_text_comp_st = '公司的安裕 : ' + str(comp_st_value) + ' | ' + str(comp_st_earn) +' | ' + str(comp_st_percent)
sd_text_fulan_1 = '已收利息：' + str(fu_value) 
sd_text_fulan_2 = str(fu_earn) + ' | ' + str(fu_percent)
sd_text_all = '合計 : ' + str(all_value) + ' | ' + str(all_percent)

print()
print('##################################################')
print('## ' + str(today))
print("## 安裕 : " + AnYu_price)
print("## 昇悅 : " + ShingYui_price)
print('##################################################')
print('## ' + sd_text_my_st)
print('## ' + sd_text_gov_st)
print('## ' + sd_text_comp_st)
print('##################################################')
print('## ' + sd_text_all)
print('##################################################')
print()

print("富蘭克林")
print('##################################################')
print('## ' + sd_text_fulan_1 + ' | ' + sd_text_fulan_2)
print('##################################################')

telegram_bot_sendtext(str(today) + " 退休基金\n--------------------------\n" + sd_text_my_st + "\n" + sd_text_gov_st + "\n" + sd_text_comp_st + "\n--------------------------\n" + sd_text_all)
telegram_bot_sendtext(str(today) + " 富蘭克林\n--------------------------\n" + sd_text_fulan_1 + "\n合計：" + sd_text_fulan_2)

os.system('pause')
```

get_fulankelam.py
```python
from selenium import webdriver
from selenium.webdriver.chrome.service import Service
from selenium.webdriver.common.by import By

import time

def gt_fulankelam():

    url = 'https://www.franklintempleton.com.hk/zh-hk/our-funds/price-and-performance/mutual-funds/products/4022/2B/%E5%AF%8C%E8%98%AD%E5%85%8B%E6%9E%97%E6%B5%AE%E5%8B%95%E6%81%AF%E7%8E%87%E5%9F%BA%E9%87%91/IE00BK6VSP79'

    chrome_options = webdriver.ChromeOptions()
    chrome_options.add_argument('--headless')
    chrome_options.add_argument("--log-level=3")
    chrome_options.add_argument('--disable-logging')
    
    chrome = webdriver.Chrome(options=chrome_options)

    chrome.get(url)
    xp = "/html/body/app-root/div/page-container/br-page/div[1]/ft-custom-layout/main/ft-product-detail-layout/eds-panel[1]/div/div/div/div[2]/div/div[2]/ft-fund-header-entry/div/ft-summary/ft-summary-international/div/div[1]/div[2]/eds-summary-item/div/div/p"
    f = True
    while f:
        try:
            print("try")
            get_price = chrome.find_element(By.XPATH, xp)
            print("try2")
            f = False
            
        except:
            time.sleep(1)
    
    rs = get_price.text[1:]
        
    print(rs)

    return rs

# gt_fulankelam()
```

## sd_telegram.py
```python
import requests

def telegram_bot_sendtext(bot_message):

    bot_token = ''
    bot_chatID = ''
    send_text = 'https://api.telegram.org/bot' + bot_token + '/sendMessage?chat_id=' + bot_chatID + '&parse_mode=Markdown&text=' + bot_message

    response = requests.get(send_text)

    return response.json()


```
