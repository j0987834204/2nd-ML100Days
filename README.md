# 2nd-ML100Days

－ 從基礎重新訓練自己，填補不足、穩固基底。

#### [Part I] 資料清理數據前處理 `Day1 to Day16`

* 第十六天為總整理，對於檢查`資料型態`與`尋找遺失值`的方法更為了解。除了練習python語法外，最重要的還是了解資料想解決的問題及相關領域背景，如何用有限的資料發揮最大效益。

* EDA（Exploratory Data Analysis）探索式資料分析與敘述統計做差不多的事，只是換了更炫砲的名字。

  [KDE（Kernel Density Estimation）](http://rightthewaygeek.blogspot.com/2015/09/kernel-density-estimation.html)以無母數方法看樣本密度函數。

  －[核密度估計](<https://blog.csdn.net/unixtch/article/details/78556499>)

  

#### [Part II] 資料科學特徵工程技術 `Day17 to Day`

##### 數值型

* 處理遺失值

  1. 統計值

     －平均值：數值型，偏態不明顯

     －中位數：數值型，偏態明顯

     －眾數：類別型

  2. 指定值：具有相關`domain knowledge`

  3. 預測值：建模預測所需欄位

     e.g. R's [mice包](<http://rpubs.com/skydome20/R-Note10-Missing_Value>)

* 特徵縮放

  1. 標準化（Standard Scaler）：假定數值為常態分佈，適合本⽅方式平衡特徵
     －不易受離群值影響

  2. 最小最大化（MinMax Scaler）： 假定數值為均勻分佈，適合本⽅方式平衡特徵

     －易受離群值影響

  ※ 樹狀模型不會因為特徵縮放影響結果

* 離群值：若不處理離群值會對特徵所放產生問題

  刪除：只要離群值數量夠少，除去離群值，將可使得模型預測較為準確，但需要了解產生此離群值原因，再決定使否刪除

* 去偏態：當離群資料比例例太高，或者平均值沒有代表性時，可以考慮去除偏態

  1. 自然對數（$ln$）

     可能會有0值出現導致無法使用，故使用`np.log1p`（先+1再取對數）及`np.expm1`（先取指數再-1）

  2. 方根去偏（sqrt）

     將數值減去最小值後開根號，最大值有限時適用

  3. 分布去偏（[box-cox]([https://en.wikipedia.org/wiki/Power_transform#Box%E2%80%93Cox_transformation](https://en.wikipedia.org/wiki/Power_transform#Box–Cox_transformation))）
  
     [資料轉換](<http://www.hmwu.idv.tw/web/R/B01-3-hmwu_R-DataTransformation.pdf>)
  
     ※ 注意 λ 參數要介於 0 到 0.5 之間，並且要注意轉換前的數值不可⼩小於等於0

##### 類別型

* 標籤編碼（Label Encoding）
* 獨熱編碼（One Hot Encoding）

|                          | ⼤⼩有無意義 | 儲存空間/計算時間 | 適⽤模型   |
| ------------------------ | ------------ | ----------------- | ---------- |
| 標籤編碼Label Encoding   | 無           | ⼩                | 樹狀模型   |
| 獨熱編碼One Hot Encoding | 有           | 較⼤              | 非樹狀模型 |

* 均值編碼（Mean Encoding）：`類別特徵`與`目標`明顯相關時可使用

  使用目標值的平均值，取代原本的類別型特徵，但較容易過度配適（overfitting），須利用平滑化修正

* 計數編碼（Counting）

  別的目標均價與類別筆數呈正相關（或負相關），也可以將筆數本身當成特徵

  ※ 自然語言處理時，字詞的計數編碼又稱詞頻，本身就是一個很重要的特徵

* 特徵雜湊 / [特徵哈希](<https://blog.csdn.net/laolu1573/article/details/79410187>)（Feature Hash）

  當相異類別數量量相當大時，其他編碼方式效果更差，可以考慮雜湊編碼以節省時間

  註 : 雜湊編碼效果也不佳，這類問題更更好的解法是嵌入式編碼(Embedding)，但是需要深度學習並有其前提

* 嵌入式編碼（Embedding）

