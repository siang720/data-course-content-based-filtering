# Data course - Content based project

### 專案目的
建立一個推薦系統，推薦商品給曾經在Mimi Beauty網站上購買過美妝商品的客戶。

### 執行方式
透過分析美妝產品資料(product data)、用戶評分資料(review data)，設計推薦邏輯，推薦商品給客戶。

### 資料切割方式
* Training data：日期在2018-09-01之前的用戶評分資料。
* Testing data：日期介於2018-09-01及2018-09-30的用戶評分資料。

### 推薦邏輯
本次專案共設計兩層推薦邏輯，說明如下列：
#### 第一層： Content-based推薦法
邏輯：根據目標使用者曾經購買的商品，推薦相似的商品給他。
演算法：
* 將product data中，重複的商品移除，並篩選2016-12-31之後有被評論過的商品
* 合併title與description欄位為新的欄位title_desc
* 將title_desc欄位文字做資料清洗，包含：將文字轉小寫、移除標點符號、數字轉為"num"表示、移除stopwords
* 將處理好的title_desc放入TF-IDF演算法計算矩陣
* 根據使用者曾經購買的商品，透過上述矩陣計算相關性，找出較高的前k名做為推薦商品
#### 第二層：如果content-based無法推薦，就改用Rule-based推薦
##### Recommend Top 10 review number in past 180 days
邏輯：根據Training data，找出過去180天內，前10個評分數量最多的商品，將這10個商品推薦給每位目標用戶。

### 使用工具及平台
Python, Colab

### 推薦結果
跟單純Rule-based演算法的recall完全相同，表示content-based沒有效果。

### Content-based無效之原因
本次要推薦的目標用戶共有584位，其中只有38位在training data中有留下評論，因此只能針對這38位用戶評論過的商品去找相似的商品做推薦，可能推薦的商品剛好都沒有打到這38位使用者的需求。

而其他546用戶則是完全無法使用過去的評論資料作為推薦依據，需要在使用者瀏覽網頁的資訊或是其他cookies中的資料，找看看有什麼樣的商品資訊，並推薦其相似的商品。
