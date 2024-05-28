# Lesson_6_Homework
## 21點遊戲

1. 把牌組分開花式 (提示：使用 dict 加 list 的組合)
3. 使用random方式抽牌
4. 每次取牌後記錄輸出變為：花式+點數
5. 加入判斷：取得J、Q、K時全部定義作10點(+10

```python
# Random Module
import random

# 生成一個有4色各13個零的列表
def card_for_13():
    temp = []
    for i in range(0,13):
        temp.append(int(0))
    return temp

count_card = {
    "黑桃":card_for_13(),
    "紅心":card_for_13(),
    "梅花":card_for_13(),
    "方塊":card_for_13()
}

# 全域變數
card_list = []
sum = 0

while(True):
    print(count_card)
        
    print("##############################################")
    print(f"目前手牌：{card_list}, 目前的點數：{sum}")
    
    # 判定是否取牌
    temp = input("\n請問需要取牌嗎? 如需要取牌請輸入:get，如要結束請輸入:bye : ")
    
    # 輸入 bye 遊戲結束
    if(temp == "bye"):
        print(f"遊戲結束! 目前手牌：，點數為：{sum}")
        break
    
    # 判斷是否輸入 get
    if(temp == "get"):
        
        # 隨機取得一張牌
        decor_list = ["黑桃", "紅心","梅花","方塊"]
        
        while(True):
            decor = decor_list[random.randint(0,3)]
            num = random.randint(1,13)
            
            if(count_card[decor][num-1] == 1):
                continue
            else:
                break
        
        ##  輸入正確  ####
        # 記錄取得的 card 在 dict 中
        count_card[decor][num-1] = 1
        
        print(f"\n這次拿到的是{decor}{num}")
        
        # 記錄目前已取得的 card 
        temp_card = str(decor) + str(num)
        card_list.append(temp_card)
    
    else:
        print("輸入錯誤")
        continue
    
    # 若通通上方判斷，則進行點數相加
    if(num>=10):
        sum = sum + 10
    else:
        sum = sum + num
    
    # 判斷 若剛好等於 21 點，贏了，遊戲結束
    if(sum == 21):
        print("恭喜你贏得遊戲!")
        break
    
    # 若大於 21 點，輸了，遊戲結束
    if(sum > 21):
        print(f"目前點數為：{sum}點，爆炸了，遊戲結束")
        break

```
