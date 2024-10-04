# 功課 : 21 點遊戲增強(final)
- 嘗試重構程式
- 2人玩家 Dealer、Player (生成1個Class - 創建2實體p1,p2, 參數 )


```python
import random

# 定義全域變數 Card dict
def card():
    return list(range(1, 14))

card_type_list = ["黑桃", "紅心", "梅花", "方塊"]
card_dict = {
    "黑桃": card(),
    "紅心": card(),
    "梅花": card(),
    "方塊": card()
}

def print_card():
    for i in card_dict:
        print(f"{i}{card_dict[i]}")

# 定義 Player Class
class Player:
    def __init__(self, player_name):
        self.player_name = player_name
        self.player_card_list = []
        self.player_sum = 0
        self.flag = True  # 用於判斷是否繼續抽牌
    
    def get_card(self):
        while True:
            rand_1 = random.randint(0, 3)
            card_type = card_type_list[rand_1]
            rand_2 = random.randint(0, 12)
            card_point = card_dict[card_type][rand_2]
            
            if (card_point == "X"):  # 已抽過的牌
                continue # 直至抽到未被其他人抽到牌為止
            
            # 若成功抽到 #
            card_dict[card_type][rand_2] = "X"  # 標記 X 為已抽
            self.player_card_list.append(f"{card_type}{card_point}") # 增加 Player 手上的 Card list
            self.card_sum(card_point) # 增加 Player 手上的點數
            break
        
    def card_sum(self, card_point):
        if card_point >= 10:
            self.player_sum += 10  # J, Q, K 算作 10
        else:
            self.player_sum += card_point
            
    def show(self):
        print(f"{self.player_name} 目前已取牌 {self.player_card_list} , 目前的點數：{self.player_sum}")

# 定義遊戲邏輯
def play_game():
    num_players = 3
    players = [Player(f"P{i+1}") for i in range(num_players)]
    #players = []
    #for i in range(num_players):
        #players.append(Player(f"Player_{i+1}"))
    
    # 每位玩家初始抽兩張牌
    for player in players:
        for _ in range(2):
            player.get_card()
            
    print_card() # 每抽完一次牌都展示牌組
    
    # 玩家輪流抽牌
    while(True):
        all_stopped = True  # 用於檢查是否所有玩家都停止抽牌 / 爆
        for player in players: 
            
            if(player.flag == True):  # 只有當玩家 flag 為 True 時才抽牌
                print(f"\n現在是 --- {player.player_name} --- 的回合：")
                player.show()

                action = input(f"{player.player_name} 是否要再抽一張牌？(get/bye): ")
                if(action.lower() == 'get'):
                    player.get_card()
                    player.show()
                    if(player.player_sum > 21):
                        print(f"{player.player_name} 超過 21 點，輸了！")
                        player.flag = False  # 設置 flag 為 False，表示停止抽牌
                else:
                    print(f"{player.player_name} 選擇停止取牌。")
                    player.flag = False  # 設置 flag 為 False，表示停止抽牌
            
                print_card() # 每抽完一次牌都展示牌組
            
            # 檢查是否所有玩家都停止抽牌
            if(player.flag):
                all_stopped = False
        
        if(all_stopped == True):  # 如果所有玩家的 flag 都是 False，則結束遊戲
            break

    # 結束遊戲，顯示所有玩家的結果
    print("\n########### 遊戲結束！結果如下 ###########")
    winners = []
    for player in players: 
        if(player.player_sum <= 21):
            winners.append(player)
        
    if(len(winners)==0):
        print("所有玩家都超過 21 點，沒人贏！")
        
    else:
        win_point = 0 # 假定一個最大值
        win_name = "" # 假定一個 winner
        for player in players: 
            print(f" {player.player_name} : {player.player_sum}點 {player.player_card_list}")
            if(player.player_sum > win_point):
                win_point = player.player_sum
                win_name = player.player_name
    
    print(f"\n最終贏家是 --- {win_name} ---、點數 {win_point} 點")

# 開始遊戲
if __name__ == "__main__":
    play_game()
```

## 以list實作另外的牌組
```python
import random

def draw_card(deck):
    card = random.choice(deck)
    deck.remove(card)
    return card

suits = ['黑桃', '紅心', '梅花', '方塊']
ranks = {
    'A': 1,
    '2': 2,
    '3': 3,
    '4': 4,
    '5': 5,
    '6': 6,
    '7': 7,
    '8': 8,
    '9': 9,
    '10': 10,
    'J': 10,
    'Q': 10,
    'K': 10
}

deck = []
for suit in suits:
    for rank in ranks.keys():
        deck.append([suit, rank, ranks[rank]])

random.shuffle(deck)

get_card = draw_card(deck)
print(get_card)
```
