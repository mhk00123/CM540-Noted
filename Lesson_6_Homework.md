# Lesson_6_Homework
## 21點遊戲

1. 把牌組分開花式 (提示：使用 dict 加 list 的組合)
3. 使用random方式抽牌
4. 每次取牌後記錄輸出變為：花式+點數
5. 加入判斷：取得J、Q、K時全部定義作10點(+10

```python
###  導入 random 模組  ####
import random

###  定義 function  ####

# 生成[1,2,3,4,5,6,7,8,9,10,11,12,13] 
def card():
    temp_list = []
    for i in range(1,14):
            temp_list.append(i)
        
    return temp_list

###  全域變數  ####

# 牌組以dict+list方式儲存、若以取牌則記為0
card_type_list = ["黑桃", "紅心", "梅花", "方塊"]
card_dict = {
    "黑桃":card(),
    "紅心":card(),
    "梅花":card(),
    "方塊":card() 
}

card_input_list = []
sum = 0

###  主程式區  ####
while(True):
    print(f"目前已取牌 {card_input_list} , 目前的點數：{sum}")
    print("##############################################")
    
    temp = input("\n取卡請輸入'get'、結束遊戲請輸入'bye'：")
    
    # 輸入 bye 遊戲結束
    if(temp == "bye"):
        print(f"遊戲結束! 目前手牌：{card_input_list}，點數為：{sum}")
        break
    
    elif(temp == "get"):
        
        while(True):
            # Random 取卡 #
            ## 第1次random拿牌的"花式" index
            rand_1 = random.randint(0,3) # index
            card_type = card_type_list[rand_1]
            
            ## 第2次random拿牌的點數的"index""
            rand_2 = random.randint(0,12) # index
            card_point = card_dict[card_type][rand_2]
        
            print(f"{card_type}{card_point}")
            
            ###  判斷牌是否已取  ####
            # 若 get_card 為 0 ，即已取，重新 random
            if(card_point == 0):
                continue
            
            else:
                card_dict[card_type][rand_2] = 0
                break
        
        # 記錄點數
        card_input_list.append(f"{card_type}{card_point}")
        
        if(card_point>=10):
            sum = sum + 10
        else:
            sum = sum + card_point
        
        # 判斷
        # 若剛好等於 21 點，贏了，遊戲結束
        if(sum == 21):
            print(f"目前已取牌 {card_input_list} , 目前的點數：{sum}")
            print("\n!!!!!!!!!!!!!!!!!!!!")
            print("恭喜你贏得遊戲!")
            break
        
        # 若大於 21 點，輸了，遊戲結束
        if(sum > 21):
            print(f"目前已取牌 {card_input_list} , 目前的點數：{sum}")
            print("\n!!!!!!!!!!!!!!!!!!!!")
            print("已經超過21點啦~爆炸了")
            break
        
        print()
    
    else:
        print("\n輸入無效\n")
        continue
```

## 無注解
```python
import random

def card():
    temp_list = []
    for i in range(1,14):
            temp_list.append(i)
    return temp_list

card_type_list = ["黑桃", "紅心", "梅花", "方塊"]
card_dict = {
    "黑桃":card(),
    "紅心":card(),
    "梅花":card(),
    "方塊":card() 
}

card_input_list = []
sum = 0

while(True):
    print(f"目前已取牌 {card_input_list} , 目前的點數：{sum}")
    print("##############################################")
    
    temp = input("\n取卡請輸入'get'、結束遊戲請輸入'bye'：")

    if(temp == "bye"):
        print(f"遊戲結束! 目前手牌：{card_input_list}，點數為：{sum}")
        break
    
    elif(temp == "get"):
        
        while(True):
            rand_1 = random.randint(0,3)
            card_type = card_type_list[rand_1]
            
            rand_2 = random.randint(0,12)
            card_point = card_dict[card_type][rand_2]
        
            print(f"{card_type}{card_point}")
            
            if(card_point == 0):
                continue
            
            else:
                card_dict[card_type][rand_2] = 0
                break
        
        card_input_list.append(f"{card_type}{card_point}")
        
        if(card_point>=10):
            sum = sum + 10
        else:
            sum = sum + card_point
            
        if(sum == 21):
            print(f"目前已取牌 {card_input_list} , 目前的點數：{sum}")
            print("\n!!!!!!!!!!!!!!!!!!!!")
            print("恭喜你贏得遊戲!")
            break
        
        if(sum > 21):
            print(f"目前已取牌 {card_input_list} , 目前的點數：{sum}")
            print("\n!!!!!!!!!!!!!!!!!!!!")
            print("已經超過21點啦~爆炸了")
            break
        
        print()
    
    else:
        print("\n輸入無效\n")
        continue
```
