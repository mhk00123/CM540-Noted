# 功課 : 21 點遊戲(final)
- 嘗試重構程式
- 2人玩家 Dealer 、Player
- 每一步取牌後輸出當時時間
- 把整個遊戲過程輸出到txt中作記錄 *(嘗試)

```python
import random
from datetime import datetime

# 定義全域變數 Card dict
def card():
    return list(range(1, 14))

def print_time():
    now = datetime.now()
    str_now = now.strftime("%H:%M:%S")
    print(f"({str_now})",end="")
    my_file.write(f"({str_now}): ")

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
            
            if card_point == "X":  # 已抽過的牌
                continue # 直至抽到未被其他人抽到牌為止
            
            # 若成功抽到 #
            card_dict[card_type][rand_2] = "X"  # 標記 X 為已抽
            self.player_card_list.append(f"{card_type}{card_point}") # 增加 Player 手上的 Card list
            self.card_sum(card_point) # 增加 Player 手上的點數
            self.show()
            break
        
    def card_sum(self, card_point):
        if card_point >= 10:
            self.player_sum += 10  # J, Q, K 算作 10
        elif card_point == 1: # A can be 1 or 11
            if self.player_sum + 11 <= 21:
                self.player_sum += 11
            else:
                self.player_sum += 1
        else:
            self.player_sum += card_point
            
    def show(self):
        print_time()
        print(f"{self.player_name} 目前已取牌 {self.player_card_list} , 目前的點數：{self.player_sum}")
        my_file.write(f"{self.player_name} 目前已取牌 {self.player_card_list} , 目前的點數：{self.player_sum}\n")


# 定義 全域變數
card_type_list = ["黑桃", "紅心", "梅花", "方塊"]
card_dict = {
    "黑桃": card(),
    "紅心": card(),
    "梅花": card(),
    "方塊": card()
}

try:
    my_file = open("record.txt", "a+", encoding="UTF-8")

except Exception as E:
    print(E)

# 定義遊戲邏輯
def play_game():

    num_players = 3

    players = []  # 建立一個空的列表來存放 Player 物件
    for i in range(num_players):
        player_name = f"P{i+1}"  # 建立玩家名稱，例如 P1, P2, P3
        player = Player(player_name)  # 建立一個 Player 物件
        players.append(player)  # 將建立好的 Player 物件加入到 players 列表中


    # 玩家輪流抽牌
    while(True):
        all_stopped = True  # 用於檢查是否所有玩家都停止抽牌 / 爆
        for player in players: 
            
            if(player.flag):  # 只有當玩家 flag 為 True 時才抽牌
                print()
                my_file.write("\n")
                print_time()
                print(f"現在是 --- {player.player_name} --- 的回合：")
                my_file.write(f"現在是 --- {player.player_name} --- 的回合：\n")
                player.show()
                action = input(f"{player.player_name} 是否要再抽一張牌？(get/bye): ")
                if(action.lower() == 'get'):
                    player.get_card()
                    if(player.player_sum > 21):
                        print_time()
                        print(f"{player.player_name} 超過 21 點，輸了！")
                        my_file.write(f"{player.player_name} 超過 21 點，輸了！\n")
                        player.flag = False  # 設置 flag 為 False，表示停止抽牌
                else:
                    print_time()
                    print(f"{player.player_name} 選擇停止取牌。")
                    my_file.write(f"{player.player_name} 選擇停止取牌。\n")
                    player.flag = False  # 設置 flag 為 False，表示停止抽牌
                # print_card() # 每抽完一次牌都展示牌組
            
            # 檢查是否所有玩家都停止抽牌
            if(player.flag):
                all_stopped = False
        
        if(all_stopped):  # 如果所有玩家的 flag 都是 False，則結束遊戲
            break

    # 結束遊戲，顯示所有玩家的結果
    
    print("\n########### 遊戲結束！結果如下 ###########\n")
    my_file.write("\n ########### 遊戲結束！結果如下 ########### \n")
    
    # Find the winner
    winners = []
    for player in players:
        if player.player_sum <= 21:
            winners.append(player)

    if not winners:
        print_time()
        print("所有玩家都超過 21 點，沒人贏！")
        my_file.write("所有玩家都超過 21 點，沒人贏！\n")
    else:
        # 找出贏家
        win_player = winners[0]  # 先假設第一個是贏家
        for player in winners:
            if player.player_sum > win_player.player_sum:
                win_player = player
        
        for player in players:
            print_time()
            print(f" {player.player_name} : {player.player_sum}點 {player.player_card_list}")
            my_file.write(f" {player.player_name} : {player.player_sum}點 {player.player_card_list}\n")
        
        print_time()
        print(f"最終贏家是 --- {win_player.player_name} ---、點數 {win_player.player_sum} 點")
        my_file.write(f"最終贏家是 --- {win_player.player_name} ---、點數 {win_player.player_sum} 點\n")
    my_file.close()

# 開始遊戲
if __name__ == "__main__":
    my_file.write("\n ------ 現在開始遊戲 ------ \n")
    play_game()

```

![Img](https://cdn.jsdelivr.net/gh/mhk00123/my-img@main/2024/202410151610455.png)


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
