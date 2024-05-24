# Lesson_5_Homework

## 21點遊戲

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

# 生成一個有13個零的列表
count_card = []
for i in range(0,13):
    count_card.append(int(0))

# count_card = [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]

user_input_list = []
sum = 0

while(True):
    print(f"目前已取牌{count_card}")
    print("##############################################")
    # 每 1 輪人手發牌 - 指定點數
    temp = input("請輸入1-13：")
    
    # 輸入 bye 遊戲結束
    if(temp == "bye"):
        print(f"遊戲結束! 目前手牌：{user_input}，點數為：{sum}")
        break
    
    user_input = int(temp)
    
    if(user_input < 1 or user_input > 13):
        print("輸入錯誤!")
        continue
    
    ###  輸入正確  ####
    # 在count_card 中 + 1
    if(count_card[user_input-1] == 4):
        print(f"已經沒有 {user_input} 了，再重新選擇！")
        continue
    else:
        count_card[user_input-1] = count_card[user_input-1] + 1
    
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
    if(sum > 21):
        print("爆炸了，")
        break
```
