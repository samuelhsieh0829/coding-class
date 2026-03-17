# 進階程式設計課堂計畫&進度
最喜歡打扣了:D

## 學期目標
### 維護:
- p2p_vc
  - 整理架構:將伺服器程式改為物件導向✅
  - 修正部分場景(如學校網路)無法使用的問題
  - 確保LAN模式可以正常運作
- samuelhsieh機器人
  - ~~優化Prompt~~太雜了需要重構✅
- Youtube Music Bot
  - 把它修好

### 新增功能:
- p2p_vc
  - 增加安全性:引入端對端加密
  - 優化介面:前端網頁啟動、客戶端介面美化
- 捷運大富翁
  - 完善CI/CD:製作完整的unittest流程
  - 剩下是學弟的事:D
- ~~samuelhsieh機器人~~把架構升級做成新的專案
  - 更改回覆機制:不僅限於mention✅
  - 增加功能，讓它從chat bot變成agent👀

### 新專案:
- samuelhsieh agent
  - 繼承samuelhsieh機器人的大部分功能✅
  - 將模型選擇機制(GPT物件)改成依照模型名稱找到適用的提供商(OpenAI、Gemini...)，分成不同的物件分別撰寫請求調用✅
  - 更改Prompt機制，改成類OpenClaw的SOUL.md、IDENTITY.md，遷移舊的base_prompt中描述@人及表符使用的方式✅
  - 從回應改成Agent，固定時間喚醒(heartbeat)
  - on_message 可以先決定是否需要回應訊息✅
  - 可以使用tools


## 每日進度小日記
### 3/3課堂
今天把p2p_vc的伺服器架構大改了一次，用上了flask的blueprint，然後把客戶端的連線機制等包成了一個物件(core)，真的覺得之前寫捷運大富翁的程式學到了好多，那裡面的架構放在這個非常適合，未來也會更方便維護
同時也增加了客戶端的一個錯誤處理，讓執行序沒有順利跑起來時可以正常把程式結束而不噴錯
[整理架構:將伺服器程式改為物件導向✅](https://github.com/samuelhsieh0829/p2p_vc/commit/bbf9bb302720a84e436f27927c0c8a40c0b4cb2e)

### 3/3晚上
剛剛又再研究了一下，發現客戶端無法正常運行是因為上次改模組化後並沒有改完整，像是connecting_list沒有共用到所有物件，總之大致上修好了，但需要再優化速度，目前延遲非常高@@
[客戶端Debug](https://github.com/samuelhsieh0829/p2p_vc/commit/01283051b7e2ed677d64d72b6926956372222fee)

### 3/10課堂
今天原本想搞unittest，但是去參考別人的專案發現要整合進原本的專案有點困難，去問了一下Github Copilot Agent，他好像直接幫我寫好了，之後找時間審查一下他提的PR，再決定要嘗試重寫還是怎樣，然後我決定接下來就做AI機器人，延伸原本的samuelhsieh機器人，把它做成類Agent
[捷大CI(AI版)](https://github.com/yingOuOb/izcc2025MRT/pull/1)

### 3/11晚上
今天開始修改samuelhsieh機器人，原本機器人程式全部寫在同個檔案看了真的很頭痛，所以今天把所有的功能作了區分，也把AI模型的部分改好了，跟朋友們討論了一下，因為讓機器人完全有agent的功能有可能會造成亂回應，擾亂原本的聊天室秩序，因此決定把agent功能設定成在.env中設定的特定頻道可使用，可以在裡面主動發話、回應任何非mention訊息，計畫可以再給與使用tools的能力。然後prompts設計成可以有多個profile，用檔案夾做區分，程式運行時隨時可以作切換。但這兩個都還沒做，下次一定。
[samuelhsieh agent第一次commit](https://github.com/samuelhsieh0829/samuelhsieh_agent/commit/82be354495fd2cf2a0a4103d75e276608b70a7dc)

### 3/17(差不多啦 +-一天)
寫了好多東西，反正是把回覆決策、多prompt那些的都弄好了，接下來就是記憶功能跟toolsㄌ，喔對還有固定時間喚醒(heartbeat)
[samuelhsieh agent第一階段完成](https://github.com/samuelhsieh0829/samuelhsieh_agent/commit/171dda286b8070a3a688d7216dacd17cfee8bff4) 前面還有好幾個commit都是差不多這幾天弄得