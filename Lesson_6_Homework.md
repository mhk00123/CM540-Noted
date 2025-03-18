# Lesson_6_Homework
## 21點遊戲 versino2

1. 以 list 方式把所有牌分開花式及點數(hints：二維list)
2. 每 1 輪發牌 - 改以 `Random` 方式
3. 把發牌這個動作打包成 function，可以把取得的牌 return 出來
4. 每一輪顯示目前手上有什麼牌(連同花式)及總點數(hints：把print這個動作也打包成function)

# 有注解版
```python
################# 導入 random 模組 #################
import random

################# 全域變數 #################
## list - card
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
        
    rs.append(card_suit)  # 第0個值為花式
    rs.append(card_point) # 第1個值為點數
    
    return rs 

## function - 輸出玩家目前狀態
def print_player():
    print(f"目前已取牌 {player_card_list} , 目前的點數：{sum}")

################# 主程式區 #################
while(True):
    print_player()
    for i in range(0,4):
        print(card_list[i])
        
    print("##############################################")
    
    temp = input("\n取卡請輸入'get'、結束遊戲請輸入'bye'：")
    
    if(temp == "bye"):
        print("遊戲結束！！！")
        print_player()
        break

    elif(temp == "get"):
        rs_get_card = get_card() # call get_card並接收回傳的 list
        
        card_suit = rs_get_card[0] # 花式
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
def get_card():
    rs = []
    while(True):  
        rand_suits = random.randint(0,3)
        card_suit = card_list[rand_suits][0]
        rand_card = random.randint(1,13)
        card_point = card_list[rand_suits][rand_card]
        print(f"取得的牌為 {card_suit}{card_point}")

        # 若取得的牌為重覆、即==*，則continue 重抽
        if(card_list[rand_suits][rand_card] == "*"): 
            continue
        
        # 若取得的牌不為*，則代表成功抽到，
        # 我們把他的值取出，並把二維list對應的位置記錄為 *
        else:
            card_list[rand_suits][rand_card] = "*"
            break
        
    rs.append(card_suit)
    rs.append(card_point)
    
    return rs 

def print_player():
    print(f"目前已取牌 {player_card_list} , 目前的點數：{sum}")

################# 主程式區 #################
while(True):
    print_player()
    for i in range(0,4):
        print(card_list[i])
        
    print("##############################################")
    
    temp = input("\n取卡請輸入'get'、結束遊戲請輸入'bye'：")
    
    if(temp == "bye"):
        print("遊戲結束！！！")
        print_player()
        break

    elif(temp == "get"):
        rs_get_card = get_card()
        card_suit = rs_get_card[0]
        card_point = rs_get_card[1]
        
        player_card_list.append(f"{card_suit}{card_point}")
        sum = sum + card_point
    
    if(sum == 21):
        print_player()
        print("\n!!!!!!!!!!!!!!!!!!!!")
        print("恭喜你贏得遊戲!")
        break
    
    elif(sum > 21):
        print_player()
        print("\n!!!!!!!!!!!!!!!!!!!!")
        print("已經超過21點啦~爆炸了")
        break
    
    print()
```

# 由李同學提供版本
```python
import random

# 1. 生成牌堆
def initial_deck():
    suits = ["黑桃", "紅桃", "梅花", "方塊"]
    nums = list(range(1, 14))  # 標識 1-13  A - K
    deck = []
    for suit in suits:
        for num in nums:
            deck.append([suit, num])
    return deck

# 2. 開始隨機發牌
def deal_card(deck, num_cards=1):
    dealt_cards = []
    for i in range(num_cards):
        if not deck:
            break  # 牌堆為空
        card_index = random.randint(0, len(deck) - 1)
        dealt_cards.append(deck.pop(card_index))
    return dealt_cards

# 3. 計算點數
def calculate_value(hand):
    total = 0
    has_ace = False
    for card in hand:
        num = card[1]
        if num >= 10:
            total += 10
        elif num == 1:
            total += 11
            has_ace = True
        else:
            total += num
    # 判斷點數是否正確
    while total > 21 and has_ace:
        total -= 10
        has_ace = False
    return total

# 4. print手中點數
def display_hand(hand, total):
    print("你的手牌：")
    for card in hand:
        print(f"{card[0]}{card[1]}", end=" ")
    print(f"\n總點數：{total}")

# 5. 遊戲循環開始
def play_game():
    deck = initial_deck()
    player_hand = []
    game_over = False

    while not game_over:
        print(deck)
        
        # 發牌
        new_cards = deal_card(deck, 1)
        player_hand.extend(new_cards)

        # 計算點數
        total = calculate_value(player_hand)

        # 現有牌花色，點數，總點數
        display_hand(player_hand, total)

        # 判斷結果是否獲勝
        if total == 21:
            print("恭喜，21点！你赢了！")
            game_over = True
        elif total > 21:
            print("爆牌了！你輸了！")
            game_over = True
        else:
            # 是否要牌
            action = input("繼續發牌嗎？ (輸入 'yes' 繼續, 輸入 'bye' 結束): ")
            if action.lower() == "bye":
                game_over = True

# 開始遊戲
play_game()
```
