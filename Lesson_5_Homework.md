# Lesson_5_Homework

## 21點遊戲 version 1

- 扑克牌(52張) :1 - 13 表示
- 每個數字最多 4 隻(list)

我們要做的：
- 每 1  輪人手發牌 - 指定點數
- 若輸入超過 4 張牌，請玩家重新輸入
- 記錄點數，點數是累加的
- 記錄點數必須引導玩家繼續發牌
- 若剛好等於 21 點，贏了，遊戲結束
- 若大於 21 點，輸了，遊戲結束
- 輸入 bye 遊戲結束

```python
# 扑克牌(52張) :1 - 13 表示
# 每個數字最多 4 隻(list)---

# 生成一個有13個4的列表
# index 對應位置 0->1, 1->2, ... ,11->Q, 12->K
card_list = [4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4]

user_input_list = []
sum = 0

while(True):
    print(f"目前已取牌{card_list}")
    print("##############################################")
    # 每 1 輪人手發牌 - 指定點數
    temp = input("請輸入1-13：")
    
    # 輸入 bye 遊戲結束
    if(temp == "bye"):
        print(f"遊戲結束! 目前手牌：{user_input}，點數為：{sum}")
        break
    
    user_input = int(temp)
    
    # 假用戶不會輸入除了數字之外的東西
    if(user_input < 1 or user_input > 13):
        print("輸入錯誤! 請重新輸入")
        continue
    
    ###  輸入正確  ####
    # 在card_list 中 + 1
    if(card_list[user_input-1] == 4):
        print(f"已經沒有 {user_input} 了，再重新選擇！")
        continue
    else:
        # 若還有空的牌，則在對應index位置記錄 扣1張
        card_list[user_input-1] = card_list[user_input-1] - 1
    
    # 記錄點數
    user_input_list.append(user_input)
    sum = sum + user_input
    print(f"目前已輸入{user_input_list}, 目前的點數：{sum}")
    
    # 判斷
    # 若剛好等於 21 點，贏了，遊戲結束
    if(sum == 21):
        print("恭喜你贏得遊戲!")
        break
    
    # 若大於 21 點，輸了，遊戲結束
    elif(sum > 21):
        print("爆炸了，")
        break
```
