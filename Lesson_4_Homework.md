# Lesson 4 - 作業答案 1 題

## Lesson4 作業 詳解(共 1 題)

## 21 點遊戲單人版

繳交網址：[https://hamster.cpttm.org.mo/spaces/NPbwFIxKFYNAvVYHnq9Sxg/upload](https://hamster.cpttm.org.mo/spaces/NPbwFIxKFYNAvVYHnq9Sxg/upload)

***

* 扑克牌(52張) ：1 - 13 表示(暫不分開花色)
* 每個數字最多 4 隻

我們要做的：

* 每 1 輪人手發牌 - 指定點數
* 若輸入超過 4 張牌，請玩家重新輸入
* 記錄點數，點數是累加的
* 記錄點數必須引導玩家繼續發牌
* 若剛好等於 21 點，贏了，遊戲結束
* 若大於 21 點，輸了，遊戲結束
* 輸入 "bye" 遊戲結束

## 解法

1. 透過 list 中的順序特性，透過index辨識目前屬於什麼牌。
2. 由使用者輸入指定點數，這個點數可以對應 list 中 index+1 的位置
3. 判決該index位置的數字，便可知道對應的點數目前還有沒有牌

<details>

<summary>Code</summary>

```python
# 1.  定義變數 #
# 1.1 以list生成牌組，其中包含1-13點數的牌，每種牌4張
# 1.2 定義一個空的list用來記錄玩家的手牌
# 1.3 定義一個變數用來記錄玩家的總點數

# 2. 迴圈開始遊戲 #
# 2.1 使用者輸入1-13的數字來取牌
# 2.2 若輸入"bye"，則結束遊戲
# 2.3 檢查輸入是否在1-13之間，若不在則提示錯誤並重新輸入
# 2.4 若輸入正確，則檢查牌組中是否還有該點數的牌(index+1)，若沒有則提示並重新輸入
# 2.5 若有，則從牌組中扣除一張該點數的牌，並將該點數加入玩家的手牌和總點數
# 2.6 將該點數加入記錄玩家的手牌、以及累加總點數

# 3. 判斷遊戲結束條件 #
# 3.1 若總點數等於21，則顯示贏得遊戲的訊息並結束遊戲
# 3.2 若總點數大於21，則顯示爆炸的訊息並結束遊戲
# 3.3 若總點數小於21，則繼續遊戲


# 1. 定義變數
# 1.1 以list生成牌組，其中包含1-13點數的牌，每種牌4張
card_list = [4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4]
# 1.2 定義一個空的list用來記錄玩家的手牌
user_input_list = []
# 1.3 定義一個變數用來記錄玩家的總點數
sum = 0

# 2. 迴圈開始遊戲 
while(True):
    print(f"目前已取牌{card_list}") # 顯示目前牌組
    print("##############################################")
    
    # 2.1 使用者輸入1-13的數字來取牌
    temp = input("請輸入1-13：") # 使用者輸入1-13的數字來取牌，或輸入bye結束遊戲
    
    # 2.2 若輸入"bye"，則結束遊戲
    if(temp == "bye"): # 若輸入bye，則結束遊戲     
        print(f"遊戲結束! 目前手牌：{user_input}，點數為：{sum}")
        break
    
    user_input = int(temp) # 若不是輸入bye，將輸入轉換為整數

    # 2.3 檢查輸入是否在1-13之間，若不在則提示錯誤並重新輸入
    if(user_input < 1 or user_input > 13):
        print("輸入錯誤! 請重新輸入")
        continue
    
    # 2.4 若輸入正確，則檢查牌組中是否還有該點數的牌(index-1)
    if(card_list[user_input-1] == 0):
        print(f"已經沒有 {user_input} 了，再重新選擇！")
        continue # 若沒有則提示並重新輸入
    
    else:
        # 2.5 若有，則從牌組中扣除一張該點數的牌
        card_list[user_input-1] = card_list[user_input-1] - 1

    # 2.6 將該點數加入記錄玩家的手牌、以及累加總點數
    user_input_list.append(user_input)
    sum = sum + user_input
    print(f"目前已輸入{user_input_list}, 目前的點數：{sum}")
    

    # 3. 判斷遊戲結束條件
    # 3.1 若總點數等於21，則顯示贏得遊戲的訊息並結束遊戲
    if(sum == 21):
        print("恭喜你贏得遊戲!")
        break

    # 3.2 若總點數大於21，則顯示爆炸的訊息並結束遊戲
    elif(sum > 21):
        print("爆炸了，")
        break
```

</details>
