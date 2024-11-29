# 功課 : 21 點遊戲增強(final)
- 嘗試重構程式
- 2人玩家 Dealer 、Player
- 每一步取牌後輸出當時時間

```python
################# 導入 random 模組 #################
import random
from datetime import datetime

################# Class Player #################
class Player:
    def __init__(self, player_name):
        self.player_name = player_name
        self.player_card_list = []
        self.player_sum = 0
        self.player_flag = True
        
    def get_card(self):
        while(True):  
            rand_suits = random.randint(0,3)
            card_suit = card_list[rand_suits][0]
            
            rand_card = random.randint(1,13)
            card_point = card_list[rand_suits][rand_card]
            print(f"---- {card_suit}{card_point} ----")
            
            # 判斷該位置是否為 *
            # 若是則該牌已取，再Random重抽
            if(card_list[rand_suits][rand_card] == "*"): 
                continue
            
            else: # 取牌後把對應位置變為 * 以作記錄
                card_list[rand_suits][rand_card] = "*"
                break # break 跳出抽牌的這個迴圈
            
        self.player_card_list.append(f"{card_suit}{card_point}")  # 第0個值為花式
        
        if card_point >= 10:
            self.player_sum += 10  # J, Q, K 算作 10
        else:
            self.player_sum += card_point
    
    def show(self):
        print_time()
        print(f"{self.player_name} 目前已取牌 {self.player_card_list} , 點數：{self.player_sum}")
        

################# 定義 function #################
def print_time():
    now = datetime.now()
    str_now = now.strftime("%H:%M:%S")
    print(f"({str_now})",end=" ")

def print_card_list():
    for i in range(0,4):
        print(card_list[i]) 

################# 全域變數 #################
## list - card
card_list = [
    ["黑桃",1,2,3,4,5,6,7,8,9,10,11,12,13],
    ["紅心",1,2,3,4,5,6,7,8,9,10,11,12,13],
    ["梅花",1,2,3,4,5,6,7,8,9,10,11,12,13],
    ["方塊",1,2,3,4,5,6,7,8,9,10,11,12,13],
]

################# 主程式區 #################

# 創建玩家
dealer = Player("Dealer")
p1 = Player("Player 1")

players_list = [dealer, p1]

# Game Start
flag_all_stoped = True
while(flag_all_stoped):
    
    for player in players_list:
        if(player.player_flag == True):
            print_time()
            print(f"現在是 ------ {player.player_name} ------ 的回合")
            player.show()
            
            while(True):
                temp = input("取牌請輸入'get'、結束遊戲請輸入'bye'：")
                temp = temp.lower()
                if(temp == "get" or temp == "bye"):
                    break
                else:
                    print(f"輸入錯誤，請重新輸入")
            
            if(temp == "get"):
                player.get_card()
                player.show()
            
            elif(temp == "bye"):
                print(f"{player.player_name} 放棄取牌，點數為：{player.player_sum}")
                player.player_flag = False
            print()
            
            # 判斷over21點
            if(player.player_sum == 21):
                print(f"{player.player_name} 獲得勝利！！！")
                exit() # 結束遊戲
            
            elif(player.player_sum > 21):
                print(f"{player.player_name} 已超過 21 點！！！")
                player.player_flag = False
    
    # 檢查是否全部人都"bye
    for player in players_list:
        if(player.player_flag == True):
            break
        else:
            flag_all_stoped = False # While 迴圈將暫停

# 若全部人都按下 bye 且未有人 over 21點，則需全部做對比並找出最大值
max_name = ""
max_sum = 0
sum_list = []
for player in players_list:
    sum_list.append(f"{player.player_name}：{player.player_sum}點")
    if(player.player_sum > max_sum and player.player_sum <= 21):
        max_name = player.player_name
        max_sum = player.player_sum
        
# 結果
print(sum_list)
print(f"最終贏家為：*** {max_name} ***，點數為：*** {max_sum}點 ***")
```
