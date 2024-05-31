# 功課 : 21 點遊戲增強(final)
- 嘗試重構程式
- 2人玩家 Dealer、Player (生成1個Class - 創建2實體p1,p2, 參數 )
- 每一步取牌後輸出當時時間
- 把整個遊戲過程輸出到txt中作記錄 *(嘗試)

```python
import random
from datetime import datetime

# Class : Player
class Player:
    def __init__(self, name):
        self.name = name
        self.card_list = []
        self.sum = 0
        self.flag = 1

################################### def function ###################################
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
    g_card_time = datetime.now()
    str_time = g_card_time.strftime("%H:%M:%S")
    
    print(f"\n({str_time}) {player.name} 拿到的是 {decor}{num} ")
    writetxt(f"\n({str_time}) {player.name} 拿到的是 {decor}{num} ")
    
    temp_card = str(decor) + str(num)
    player.card_list.append(temp_card)
    
    return num

# 計算目前的點數
def get_sum(player, num):
    if(num>=10):
       player.sum = player.sum + 10
    else:
        player.sum = player.sum + num
    
# 判斷目前的點數是否等於21點、大於21點
def isOver(player):
    if player.sum == 21:
        print(f"恭喜 {player.name} 取得21點 贏得遊戲!")
        writetxt(f"恭喜 {player.name} 取得21點 贏得遊戲!")
        player.flag = 3
        exit()
    
    if player.sum > 21:
        print(f"目前點數為：{player.sum}點，{player.name}爆炸了，遊戲結束")
        writetxt(f"目前點數為：{player.sum}點，{player.name}爆炸了，遊戲結束")
        player.flag = 3
        exit()
    
    return False

# Game Function
def game(player):
    # 透過 flag 的狀態控制是否進行抽牌
    if player.flag == 1:
        temp = input(f"\n請問{player.name}需要取牌嗎? 如需要取牌請輸入:get，如要結束請輸入:bye : ")
        
        if temp == "bye":
            print(f"{player.name}選擇結束遊戲")
            writetxt(f"{player.name}選擇結束遊戲")
            player.flag = 3
            return
        
        if temp == "get":
            num = get_card(player, count_card)
            get_sum(player, num)
            
            # 每次取完牌後都需要判定目前有沒有等於21點、或大於21點
            if isOver(player):
                player.flag = 2
            return
            
        else:
            print("輸入錯誤")  

# 輸出目前手牌 card_list
def print_card(player_list):
    print("##############################################")
    for i in player_list:
        print(f"{i.name} 目前的點數：{i.sum}、手牌：{i.card_list}")

# 若雙方都輸入 bye ，則判斷目前誰的點數較大
def compare_score(player_list):
    dealer_score = player_list[0].sum
    
    sum_list = []
    i = 1
    while(i<len(player_list)):
        sum_list.append(player_list[i].sum)
        i = i+1
    
    player_max = max(sum_list)

    if dealer_score > player_max:
        print(f"Dealer 獲勝！Dealer點數：{dealer_score}，Player點數：{player_max}")
        writetxt(f"Dealer 獲勝！Dealer點數：{dealer_score}，Player點數：{player_max}")
    elif player_max > dealer_score:
        print(f"Player 獲勝！Player點數：{player_max}，Dealer點數：{dealer_score}")
        writetxt(f"Player 獲勝！Player點數：{player_max}，Dealer點數：{dealer_score}")
    else:
        print("平局！")
        writetxt("平局！")

    # Compare 完成後結束遊戲 
    exit()

# Function : 輸出txt函數
def writetxt(w_text):
    try:
        with open(f"{game_start_time}.txt", "a") as my_file:
            my_file.write(w_text)
            
    except Exception as E:
        print(E)

# Function : 生成 52 張牌
def card_for_13():
    temp = []
    for i in range(0, 13):
        temp.append(int(0))
    return temp

###################### Main function ###################### 
if __name__ == "__main__":
    
    # Time
    game_start_time = datetime.now().strftime("%Y-%m-%d_%H%M%S")

    # Card
    count_card = {
        "黑桃": card_for_13(),
        "紅心": card_for_13(),
        "梅花": card_for_13(),
        "方塊": card_for_13()
    }

    # 創建Player
    dealer = Player("Dealer")
    player1 = Player("Player1")
    player2 = Player("Player2")
    player_list = [dealer, player1, player2]
    
    while True:

        for i in player_list:
            print_card(player_list)
            game(i)
            
        for i in player_list:
            if(i.flag!=3):
                break
            compare_score(player_list)
```