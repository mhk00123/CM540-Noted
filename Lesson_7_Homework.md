# 功課 : 21 點遊戲增強(final)
嘗試重構以function形式把”動作”function化
2人玩家 dealer 、player

```python
import random

################################### def function ###################################
# 生成 52 張牌
def card_for_13():
    temp = []
    for i in range(0, 13):
        temp.append(int(0))
    return temp

# 取牌
def get_card(player, count_card):
    decor_list = ["黑桃", "紅心","梅花","方塊"]
    
    while True:
        decor = decor_list[random.randint(0, 3)]
        num = random.randint(1, 13)
        
        if count_card[decor][num-1] == 1:
            continue
        else:
            break
    
    count_card[decor][num-1] = 1
    
    print(f"\n{player['name']} 拿到的是 {decor}{num} ")
    
    temp_card = str(decor) + str(num)
    player["card_list"].append(temp_card)
    
    return num

# 計算目前的點數
def get_sum(player, num):
    player["sum"] = player["sum"] + num
    
# 判斷目前的點數是否等於21點、大於21點
def isOver(player):
    if player["sum"] == 21:
        print(f"恭喜 {player['name']} 取得21點 贏得遊戲!")
        player["flag"] = 3
        exit()
    
    if player["sum"] > 21:
        print(f"目前點數為：{player['sum']}點，{player['name']}爆炸了，遊戲結束")
        player["flag"] = 3
        exit()
    
    return False

# Game Function
def game(player):
    # 透過 flag 的狀態控制是否進行抽牌
    if player["flag"] == 1:
        temp = input(f"\n請問{player['name']}需要取牌嗎? 如需要取牌請輸入:get，如要結束請輸入:bye : ")
        
        if temp == "bye":
            print(f"{player['name']}選擇結束遊戲")
            player["flag"] = 3
            return
        
        if temp == "get":
            num = get_card(player, count_card)
            get_sum(player, num)
            
            # 每次取完牌後都需要判定目前有沒有等於21點、或大於21點
            if isOver(player):
                player["flag"] = 2
            return
            
        else:
            print("輸入錯誤")
            
    else:
        pass       

# 若雙方都輸入 bye ，則判斷目前誰的點數較大
def compare_score(dealer, player):
    dealer_score = dealer["sum"]
    player_score = player["sum"]
    
    if dealer_score > player_score:
        print(f"Dealer 獲勝！Dealer點數：{dealer_score}，Player點數：{player_score}")
    elif player_score > dealer_score:
        print(f"Player 獲勝！Player點數：{player_score}，Dealer點數：{dealer_score}")
    else:
        print("平局！")

# 輸出目前手牌 card_list
def print_card(p1,p2):
    print("##############################################")
    print(f"目前 {p1['name']} 手牌：{p1['card_list']}，目前的點數：{p1['sum']}")
    print(f"目前 {p2['name']} 手牌：{p2['card_list']}，目前的點數：{p2['sum']}")

################################### 全域變數 ###################################

# 生成玩家 - dealer
dealer = {
    "name" : "dealer",
    "card_list": [],
    "sum": 0,
    "flag": 1
}

# 生成玩家 - p1
p1 = {
    "name" : "player1",
    "card_list": [],
    "sum": 0,
    "flag": 1
}

# Card
count_card = {
    "黑桃": card_for_13(),
    "紅心": card_for_13(),
    "梅花": card_for_13(),
    "方塊": card_for_13()
}

################################### Main Function ###################################
if __name__ == "__main__":
    
    print(count_card)
    
    while True:

        print_card(p1, dealer)
        game(p1)

        print_card(p1, dealer)
        game(dealer)
        
        if p1["flag"] == 3 and dealer["flag"] == 3:
            compare_score(dealer, p1)
            break
```
