### 2021 Database Final Project
# 交大學餐營養管理系統
> 讓交大肥宅省掉煩惱一日三餐的時間又可以吃得健康!

整合交大校園內學餐營業時間、品項營養成分、熱量等資訊，根據使用者需求推薦餐點，解決每日煩惱三餐的困擾
同時建立使用者資料庫，透過註冊帳號及資料，記錄個人飲食記錄。統計使用者每日攝取的營養成分，給予建議的運動項目，幫助師生控管飲食及健康。

### Spotlight video
[![IMAGE ALT TEXT](https://github.com/Tristaaaa/NCTU_StudentCafeteria_ManageSystem/blob/main/demo/homepage.png)](https://www.youtube.com/watch?v=OZ9mM3XkSYU)

## Data
### Data Source
- [國立陽明交大餐廳營養分析表](https://www.ga.nctu.edu.tw/general-division/rest/c-5Njh/g-1?fbclid=IwAR3r5uhtZhqKuAVFKHUEmMeB8wUh0QHyWEpm83xjcoMc8XinOFto4SBSjdk)
- [國立陽明交通大學各餐廳營業時間表](https://www.ga.nctu.edu.tw/general-division/rest/v-TmrI)
- 運動消耗卡路里資料表([衛生福利部國民健康署](https://www.hpa.gov.tw/Pages/Detail.aspxnodeid=571&pid=9738&fbclid=IwAR18CmmzxVKvd77PrhkZFdz37agEJ1kIXW16m3V3OlP_K1jGDMsp67rd-Lo)):


## Application
### Interface
![image](https://github.com/Tristaaaa/NCTU_StudentCafeteria_ManageSystem/blob/main/demo/interface.png)

### Functions
**1. 登入/註冊頁面：**
- 此頁面會要求使用者輸入帳號及密碼，若帳號跟密碼輸入正確，將前往主頁面
- 若輸入錯誤，則會顯示"帳號/密碼錯誤"
- 未註冊的使用者，則可按下"註冊帳號"，將前往註冊頁面

**2. 註冊頁面：**
- 此頁面會要求使用者輸入帳號、密碼、名字、身高、體重
- 設有防呆機制，若少輸入任一項資料、資料不符合格式、或是輸入了一個已註冊的帳號，則會出現對應的的提醒
- 在成功註冊後，會導往主頁面

**3. 主頁面：**
- 主頁面會透過使用者的體重，計算出使用者一天建議攝取的熱量，及今天已攝取的熱量，並顯示過往的飲食紀錄
- 透過輸入指定日期，使用者可查詢特定日期所攝取的總熱量
- 按下"登出帳號"，可回到登入/註冊頁面
- 主頁面上方有我們的四大主要功能: 修改資料、推薦餐點、紀錄飲食、運動身體好，按下任一功能便會跳往特定頁面

**4. 修改資料頁面：**
- 此頁面將提供更改使用者資料的功能
- 使用者必須輸入帳號(帳號不可修改)，使用者可自由選擇是否填寫新密碼、新名字、新身高、新體重
- 若輸入格式/內容不符，則會出現對應提醒
![image](https://github.com/Tristaaaa/NCTU_StudentCafeteria_ManageSystem/blob/main/demo/application.gif)

**5. 推薦餐廳頁面：**
- 透過三種問題選擇，推薦使用者最適合的餐點排序，分別為：
1. 你想吃哪間學餐？（女二、研三、二餐 )
2. 你想吃哪種類型？（正餐、飲料/點心、早餐）
3. 排序依據？（價錢低到高、熱量低到高、依熱門程度）
- 另外會根據使用者此刻查詢的時間，列出此時正在營業的店家，若是此時皆無店家營業，我們將顯示"抱歉，目前時間沒有可供應的餐點"
- 若使用者查詢餐點完畢，則可按下"回首頁"，回到主頁面
![image](https://github.com/Tristaaaa/NCTU_StudentCafeteria_ManageSystem/blob/main/demo/recommendation.gif)

**6. 記錄飲食頁面：**
- 此頁面提供使用者記錄飲食
- 在選擇完餐廳後，將列出該餐廳所有的商品、售價、熱量，使用者在餐點下方按下新增，就會將該品項添加到飲食紀錄中

**7. 運動身體好頁面：**
- 此頁面將根據使用者今天攝取的熱量，顯示建議的運動時間
- 使用者在選擇運動後，將會顯示若是從事該運動，必須持續運動幾個小時，才能消耗對應的熱量

## Database
### ER Model of Schema
![image](https://github.com/Tristaaaa/NCTU_StudentCafeteria_ManageSystem/blob/main/demo/ERModel.png)
- user_eat: 紀錄各品項被消費的次數，推薦菜單建立並算出熱門選項
- user_info: 紀錄每個註冊的使用者的資料，包括帳號/ 密碼/ 名字/ 身高/ 體重
- 營業時間: 紀錄各餐廳的營業時間，因為各家餐廳都有不同的營業時間，所以只會提供在使用者查詢的時後有營業的餐廳做為查詢
- 消耗熱量: 紀錄各項運消耗熱量，利用熱量換算並推薦使用者進行運動
- 各餐廳品項: 紀錄餐點名稱/ 售價/ 一份(g)/ 蛋白質(g)/ 脂肪(g)/ 醣類(g)/ 熱量(大卡)

## Connect Database to Application
![image](https://github.com/Tristaaaa/NCTU_StudentCafeteria_ManageSystem/blob/main/demo/dbtoweb.png)
- 利用php來獲取user的request，並抓取資料庫中的data，再透過html將結果呈現於網頁
- 使用XAMPP作為網頁伺服器架站的工具，其整合了Apache+MariaDB+PHP+Perl，安裝連線後，將php檔放進相應的根目錄中後，就能在本機進行測試和操作



