# Lesson_6_Homework

{% hint style="info" %}

# 21 點遊戲單人版 Version 2

繳交網址：[https://hamster.cpttm.org.mo/spaces/qiStjaFjLahBUZU-QUqFXg/upload](https://hamster.cpttm.org.mo/spaces/qiStjaFjLahBUZU-QUqFXg/upload)

---
- 以 list/dict 方式把所有牌分開花式及點數(hints：二維list)
- 每 1 輪發牌 - 改以 `Random` 方式
- 把發牌這個動作打包成 function，可以把取得的牌 return 出來
- 每一輪顯示目前手上有什麼牌(連同花式)及總點數(hints：把print這個動作也打包成function)

{% endhint %}

# 有注解版
```python
################# 導入 random 模組 #################
import random

################# 全域變數 #################
## list - card
## index = 0 為花式
## index 1-13 為對應的點數

card_list = [
    ["黑桃",1,2,3,4,5,6,7,8,9,10,11,12,13],
    ["紅心",1,2,3,4,5,6,7,8,9,10,11,12,13],
    ["梅花",1,2,3,4,5,6,7,8,9,10,11,12,13],
    ["方塊",1,2,3,4,5,6,7,8,9,10,11,12,13],
]

## int - 玩家點數
sum = 0

## list - 玩家已取的牌 
player_card_list = []

################# 定義 function #################
## function - 取牌
def get_card():
    rs = [] # 定義回傳的為一個 list
    
    while(True): 
        rand_suits = random.randint(0,3)
        card_suit = card_list[rand_suits][0]
        
        rand_card = random.randint(1,13)
        card_point = card_list[rand_suits][rand_card]
        print(f"取得的牌為 {card_suit}{card_point}")
        
        # 判斷該位置是否為 *
        # 若是則該牌已取，再Random重抽
        if(card_list[rand_suits][rand_card] == "*"): 
            continue
        
        else: # 取牌後把對應位置變為 * 以作記錄
            card_list[rand_suits][rand_card] = "*"
            break # break 跳出抽牌的這個迴圈
    
    # rs 為一個 list 
    rs.append(card_suit)  # index =  0 個值為花式
    rs.append(card_point) # index =  1 個值為點數
    
    return rs 

## function - 輸出玩家目前狀態
def print_player():
    print(f"目前已取牌 {player_card_list} , 目前的點數：{sum}")

################# 主程式區 #################
while(True):
    print_player()

    user_input = input("\n取卡請輸入'get'、結束遊戲請輸入'bye'：")
    
    if(user_input == "bye"):
        print("遊戲結束！！！")
        print_player()
        break

    elif(user_input == "get"):
        rs_get_card = get_card()    # call get_card並接收回傳的 list
        
        card_suit = rs_get_card[0]  # 花式
        card_point = rs_get_card[1] # 點數
        
        player_card_list.append(f"{card_suit}{card_point}")
        sum = sum + card_point
    
    # 判斷若剛好等於 21 點，贏了，遊戲結束
    if(sum == 21):
        print_player()
        print("\n!!!!!!!!!!!!!!!!!!!!")
        print("恭喜你贏得遊戲!")
        break
    
    # 若大於 21 點，輸了，遊戲結束
    elif(sum > 21):
        print_player()
        print("\n!!!!!!!!!!!!!!!!!!!!")
        print("已經超過21點啦~爆炸了")
        break
    
    print()
```

# 無注解版
```python
################# 導入 random 模組 #################
import random

################# 全域變數 #################
card_list = [
    ["黑桃",1,2,3,4,5,6,7,8,9,10,11,12,13],
    ["紅心",1,2,3,4,5,6,7,8,9,10,11,12,13],
    ["梅花",1,2,3,4,5,6,7,8,9,10,11,12,13],
    ["方塊",1,2,3,4,5,6,7,8,9,10,11,12,13],
]

sum = 0
player_card_list = []

################# 定義 function #################
## function - 取得一張牌
def get_card():
    rs = []
    
    while(True): 
        rand_suits = random.randint(0,3)
        card_suit = card_list[rand_suits][0]
        
        rand_card = random.randint(1,13)
        card_point = card_list[rand_suits][rand_card]
        print(f"取得的牌為 {card_suit}{card_point}")
        
        if(card_list[rand_suits][rand_card] == "*"): 
            continue
        
        else:
            card_list[rand_suits][rand_card] = "*"
            break
    
    rs.append(card_suit)
    rs.append(card_point)
    
    return rs 

## function - 輸出玩家目前狀態
def print_player():
    print(f"目前已取牌 {player_card_list} , 目前的點數：{sum}")

################# 主程式區 #################
while(True):
    print_player()

    user_input = input("\n取卡請輸入'get'、結束遊戲請輸入'bye'：")
    
    if(user_input == "bye"):
        print("遊戲結束！！！")
        print_player()
        break

    elif(user_input == "get"):
        rs_get_card = get_card()
        
        card_suit = rs_get_card[0]
        card_point = rs_get_card[1]
        
        player_card_list.append(f"{card_suit}{card_point}")
        sum = sum + card_point
    
    # 判斷若剛好等於 21 點，贏了，遊戲結束
    if(sum == 21):
        print_player()
        print("\n!!!!!!!!!!!!!!!!!!!!")
        print("恭喜你贏得遊戲!")
        break
    
    # 若大於 21 點，輸了，遊戲結束
    elif(sum > 21):
        print_player()
        print("\n!!!!!!!!!!!!!!!!!!!!")
        print("已經超過21點啦~爆炸了")
        break
    
    print()
```
