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
        
        # 判斷該位置是否為 *
        # 若是則該牌已取，再Random重抽
        if(card_list[rand_suits][rand_card] == "*"): 
            continue
        
        else: # 取牌後把對應位置變為 * 以作記錄
            card_list[rand_suits][rand_card] = "*"
            print(f"取得的牌為 {card_suit}{card_point}")
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

        if(card_list[rand_suits][rand_card] == "*"): 
            continue
        
        else:
            card_list[rand_suits][rand_card] = "*"
            print(f"取得的牌為 {card_suit}{card_point}")
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

# 陳同學參考答案
```python
import random

# 初始化牌堆
suits = ['♥', '♦', '♣', '♠']
ranks = [
    ('A', 1), ('2', 2), ('3', 3), ('4', 4), ('5', 5),
    ('6', 6), ('7', 7), ('8', 8), ('9', 9), ('10', 10),
    ('J', 10), ('Q', 10), ('K', 10)
]


def initialize_deck():
    """初始化並洗牌"""
    deck = [[suit, rank[0], rank[1]] for suit in suits for rank in ranks]
    random.shuffle(deck)
    return deck


def deal_card(deck):
    """發牌函數"""
    if not deck:
        return None
    return deck.pop()


def display_hand(hand, total_points):
    """顯示當前手牌和總點數"""
    print("\n當前手牌: ", end="")
    for card in hand:
        print(f"{card[0]}{card[1]}", end=" ")
    print(f"\n總點數: {total_points}")


def display_deck_status(deck):
    """顯示牌堆狀態"""
    print("\n=== 牌堆狀態 ===")
    print(f"總剩餘: {len(deck)}張")

    rank_counts = {rank[0]: 0 for rank in ranks}
    for card in deck:
        rank_counts[card[1]] += 1

    for rank in ranks:
        if rank_counts[rank[0]] > 0:
            print(f"{rank[0]}: {rank_counts[rank[0]]}張", end=" | ")
    print("\n" + "=" * 20)


# 遊戲主程式
def play_blackjack():
    deck = initialize_deck()
    hand = []
    total_points = 0

    while True:
        display_deck_status(deck)

        # 自動發牌
        card = deal_card(deck)
        if card is None:
            print("牌堆已空！遊戲結束。")
            break

        hand.append(card)
        total_points += card[2]

        print(f"\n發到: {card[0]}{card[1]} (+{card[2]}點)")
        display_hand(hand, total_points)

        # 檢查遊戲結果
        if total_points == 21:
            print("恭喜！21點！")
            break
        elif total_points > 21:
            print(f"爆牌！總點數 {total_points} 超過21點")
            break

        # 詢問是否繼續
        choice = input("\n繼續要牌嗎？ (y/n): ").lower().strip()
        if choice != 'y':
            print(f"遊戲結束，最終點數: {total_points}")
            break


# 啟動遊戲
if __name__ == "__main__":
    play_blackjack()
```


# 潘同學參考答案
```python
import random


def create_deck():
    """創建一副完整的撲克牌(52張)，使用二維list表示"""
    suits = ["♠", "♥", "♦", "♣"]  # 黑桃、紅心、方塊、梅花
    ranks = ["A", "2", "3", "4", "5", "6", "7", "8", "9", "10", "J", "Q", "K"]

    deck = []
    for suit in suits:
        for rank in ranks:
            deck.append([suit, rank])

    return deck


def draw_card(deck):
    """從牌堆中隨機抽取一張牌並返回"""
    if not deck:
        return None

    # 隨機選擇一張牌
    card_index = random.randint(0, len(deck) - 1)
    card = deck.pop(card_index)

    return card


def get_card_value(rank):
    """根據牌面獲取點數值"""
    if rank == "A":
        return 1
    elif rank in ["J", "Q", "K"]:
        return 10
    else:
        return int(rank)


def display_hand_and_points(hand, total_points):
    """顯示目前手上的牌和總點數"""
    print("\n=== 您目前的手牌 ===")
    for i, card in enumerate(hand, 1):
        suit, rank = card
        print(f"{i}. {suit}{rank}")

    print(f"\n總點數: {total_points}")
    print("=" * 20)


def twenty_one_game():
    """21點遊戲主函數"""
    # 創建牌堆
    deck = create_deck()
    # 玩家手牌
    player_hand = []
    # 總點數
    total_points = 0

    print("歡迎來到21點遊戲 2.0！")
    print("遊戲將隨機為您發牌")
    print("按 Enter 鍵抽牌，輸入 'bye' 結束遊戲")

    while True:
        # 顯示當前手牌和點數
        if player_hand:
            display_hand_and_points(player_hand, total_points)
        else:
            print(f"\n您目前的點數是: {total_points}")

        # 獲取玩家輸入
        user_input = input("\n按 Enter 鍵抽牌 (或輸入 'bye' 結束遊戲): ")

        # 檢查是否要結束遊戲
        if user_input.lower() == "bye":
            print(f"遊戲結束！您的最終點數是: {total_points}")
            if player_hand:
                print("\n最終手牌:")
                display_hand_and_points(player_hand, total_points)
            break

        # 檢查牌堆是否還有牌
        if not deck:
            print("牌堆已空，遊戲結束！")
            break

        # 抽牌
        card = draw_card(deck)
        if card is None:
            print("無法抽牌，遊戲結束！")
            break

        # 將牌加入手牌
        player_hand.append(card)

        # 計算點數
        suit, rank = card
        card_value = get_card_value(rank)
        total_points += card_value

        # 顯示抽到的牌
        print(f"\n您抽到了: {suit}{rank} (點數: {card_value})")

        # 檢查遊戲結果
        if total_points == 21:
            display_hand_and_points(player_hand, total_points)
            print("🎉 恭喜！您得到了21點，贏了！")
            break
        elif total_points > 21:
            display_hand_and_points(player_hand, total_points)
            print("💥 很遺憾，您的點數超過了21點，輸了！")
            break

        # 顯示剩餘牌數
        print(f"牌堆剩餘: {len(deck)} 張牌")


# 執行遊戲
if __name__ == "__main__":
    twenty_one_game()
```
